---
type: page
title: Signature Validation
listed: true
slug: signature-validation
description: 
index_title: Signature Validation
hidden: 
keywords: 
tags: 
---

The Identity Profile Report JSON contains a `proof` object that can be used to verify the integrity of the data. To keep the JSON structure in human-readable form, we use a variation of [JSON Web Signature (JWS)](https://datatracker.ietf.org/doc/html/rfc7515) with detached payload format. This means that instead of carrying the JSON payload in the JWS, it can be attached to the payload as the `proof.jws` field value, while keeping the payload as it was signed.

Below is the proof object structure:

{% code %}
{% tab language="json" %}
"proof": {
    "jws": "<encoded_signature>",
    "public_key_url": "<url_for_public_key>"
}
{% /tab %}
{% /code %}

## Verification process

Verifying the signature and data integrity can be achieved by the following:

1. Retain the `proof.jws` value from the Identity Profile Report.
2. Change the `proof.jws` value to an empty string (““) in the Report JSON.
3. Canonicalise the report according to [RFC 8785](https://datatracker.ietf.org/doc/html/rfc8785).
4. Verify the signature against the key that’s obtained by resolving `proof.public_key_url` .

### Example code

{% code %}
{% tab language="javascript" %}
const fs = require('fs');
const axios = require('axios');
const jose = require('jose');
const { canonicalize } = require('json-canonicalize');

// Load the JSON data from the file
const report = JSON.parse(fs.readFileSync('identity_profile_report.json', 'utf8'));

// Extract the proof.jws value and the proof.public_key_url
const jwsToken = report.proof.jws;
const publicKeyUrl = report.proof.public_key_url;

// Set the proof.jws value to an empty string
report.proof.jws = "";

// Canonicalize the JSON data according to RFC 8785
const canonicalizedReport = canonicalize(report);

// Base64url encode the canonicalized JSON data
const encodedPayload = Buffer.from(canonicalizedReport, 'utf8').toString('base64url');

// Decode the JWS token
const [protectedHeader, , signature] = jwsToken.split('.');

// Fetch the public key from the proof.public_key_url
axios.get(publicKeyUrl)
  .then(async response => {
    const publicKeyJwk = response.data.keys[0];

    // Import the public key using jose.importJWK
    const key = await jose.importJWK(publicKeyJwk, 'EdDSA');

    // Construct the JWS object
    const jws = {
      protected: protectedHeader,
      payload: encodedPayload,
      signature: signature
    };

    // Verify the JWS signature using the flattenedVerify method
    try {
      await jose.flattenedVerify(jws, key, {
        algorithms: ['EdDSA']
      });

      console.log("Signature is valid.");
    } catch (err) {
      console.error("Signature verification failed:", err);
    }
  })
  .catch(err => {
    console.error("Failed to fetch public key:", err);
  });
{% /tab %}
{% tab language="python" %}
import json
import requests
from jwcrypto import jwk, jws
import rfc8785

# Load the JSON data from the file
with open('identity_profile_report.json', 'r') as file:
    report = json.load(file)

# Extract the proof.jws value and the proof.public_key_url
jws_token = report['proof']['jws']
public_key_url = report['proof']['public_key_url']

# Set the proof.jws value to an empty string
report['proof']['jws'] = ""

# Canonicalize the JSON data according to RFC 8785
canonicalized_report = rfc8785.dumps(report)

# Fetch the public key from the proof.public_key_url
response = requests.get(public_key_url)
public_key_jwk_set = response.json()

# Extract the first key from the keys array
public_key_jwk = public_key_jwk_set['keys'][0]

# Verify the JWS signature using the detached payload method
key = jwk.JWK(**public_key_jwk)
jws_token_obj = jws.JWS()
jws_token_obj.deserialize(jws_token)

try:
    jws_token_obj.verify(key, detached_payload=canonicalized_report)
    print("Signature is valid.")
except Exception as e:
    print(f"Signature verification failed: {e}")
{% /tab %}
{% tab language="go" %}
package main

import (
	"encoding/json"
	"fmt"
	"io"
	"net/http"
	"os"

	"github.com/go-jose/go-jose/v4"
	"github.com/gowebpki/jcs"
)

func main() {
	jsonFile := "identity_profile_report.json"

	b, err := os.ReadFile(jsonFile)
	if err != nil {
		fmt.Printf("Failed to read input report file (%v): %v\n", jsonFile, err)
		os.Exit(1)
	}

	// Unmarshal the Identity Profile Report into a map.
	var report map[string]interface{}
	err = json.Unmarshal(b, &report)
	if err != nil {
		fmt.Printf("Failed to unmarshal JSON: %v\n", err)
		os.Exit(1)
	}

	// Capture the original jws proof value.
	proof, ok := report["proof"].(map[string]interface{})
	if !ok {
		fmt.Printf("Failed to get proof from report\n")
		os.Exit(1)
	}
	jws, ok := proof["jws"].(string)
	if !ok {
		fmt.Printf("Failed to get jws from proof\n")
		os.Exit(1)
	}
	// Change the jws value in the original report to an empty string.
	proof["jws"] = ""

	// Marshal the modified report back to JSON.
	modifiedJson, err := json.Marshal(report)
	if err != nil {
		fmt.Printf("Failed to marshal modified report: %v\n", err)
		os.Exit(1)
	}

	// Canonicalize the JSON.
	canonicalJson, err := jcs.Transform(modifiedJson)
	if err != nil {
		fmt.Printf("Failed to canonicalize the JSON: %v\n", err)
		os.Exit(1)
	}

	// Verify the original signature against the canonicalized payload and the public key.
	js, err := jose.ParseDetached(jws, canonicalJson, []jose.SignatureAlgorithm{jose.EdDSA})
	if err != nil {
		fmt.Printf("Failed to parse detached signature: %v\n", err)
		os.Exit(1)
	}

	keyID := js.Signatures[0].Header.KeyID
	pk, err := getPublicKey(proof["public_key_url"].(string), keyID)
	if err != nil {
		fmt.Printf("Failed to get the public key: %v\n", err)
		os.Exit(1)
	}

	_, err = js.Verify(pk)
	if err != nil {
		fmt.Printf("Signature verification failed: %v\n", err)
		os.Exit(1)
	}

	fmt.Printf("Signature is valid.\n")
}

func getPublicKey(keyUrl, keyID string) (*jose.JSONWebKey, error) {
	resp, err := http.Get(keyUrl)
	if err != nil {
		return nil, fmt.Errorf("failed to GET key: %v", err)
	}
	defer resp.Body.Close()
	if resp.StatusCode != 200 {
		return nil, fmt.Errorf("unexpected HTTP code %d", resp.StatusCode)
	}
	body, err := io.ReadAll(resp.Body)
	if err != nil {
		return nil, fmt.Errorf("failed to read response body: %v", err)
	}
	var keySet jose.JSONWebKeySet
	err = json.Unmarshal(body, &keySet)
	if err != nil {
		return nil, fmt.Errorf("failed to unmarshal (%T): %v", keySet, err)
	}
	for _, k := range keySet.Keys {
		if k.KeyID == keyID {
			return &k, nil
		}
	}
	return nil, fmt.Errorf("key with keyID %q not found", keyID)
}
{% /tab %}
{% tab language="php" %}
<?php
require 'vendor/autoload.php';

use Jose\Component\Core\JWK;
use Jose\Component\Core\AlgorithmManager;
use Jose\Component\Signature\JWSVerifier;
use Jose\Component\Signature\Serializer\CompactSerializer;
use Jose\Component\Signature\Algorithm\EdDSA;
use GuzzleHttp\Client;
use Root23\JsonCanonicalizer\JsonCanonicalizer;

// Load the JSON data from the file
$report = json_decode(file_get_contents('identity_profile_report.json'), true);

// Extract the proof.jws value and the proof.public_key_url
$jws_token = $report['proof']['jws'];
$public_key_url = $report['proof']['public_key_url'];

// Set the proof.jws value to an empty string
$report['proof']['jws'] = "";

// Canonicalize the JSON data according to RFC 8785
$canonicalizer = new JsonCanonicalizer();
$canonicalized_report = $canonicalizer->canonicalize($report);

// Fetch the public key from the proof.public_key_url
$client = new Client();
$response = $client->get($public_key_url);
$public_key_jwk_set = json_decode($response->getBody(), true);

// Extract the first key from the keys array
$public_key_jwk = $public_key_jwk_set['keys'][0];

// Verify the JWS signature using the detached payload method
$jwk = new JWK($public_key_jwk);
$algorithmManager = new AlgorithmManager([new EdDSA()]);
$jwsVerifier = new JWSVerifier($algorithmManager);
$serializer = new CompactSerializer();
$jws = $serializer->unserialize($jws_token);

try {
    $isValid = $jwsVerifier->verifyWithKey($jws, $jwk, 0, $canonicalized_report);
    if ($isValid) {
        echo "Signature is valid.";
    } else {
        echo "Signature verification failed.";
    }
} catch (Exception $e) {
    echo "Signature verification failed: " . $e->getMessage();
}
{% /tab %}
{% tab language="java" %}
package com.example;

import com.fasterxml.jackson.databind.JsonNode;
import com.fasterxml.jackson.databind.ObjectMapper;
import com.fasterxml.jackson.databind.node.ObjectNode;
import okhttp3.OkHttpClient;
import okhttp3.Request;
import okhttp3.Response;
import org.jose4j.jws.JsonWebSignature;
import org.jose4j.jwk.JsonWebKey;
import org.jose4j.lang.JoseException;
import org.erdtman.jcs.JsonCanonicalizer;

import java.io.File;
import java.io.IOException;

public class SignatureVerification {
  public static void main(String[] args) {
    try {
      // Load the JSON data from the file
      ObjectMapper mapper = new ObjectMapper();
      JsonNode report = mapper.readTree(new File("identity_profile_report.json"));

      // Extract the proof.jws value and the proof.public_key_url
      String jwsToken = report.get("proof").get("jws").asText();
      String publicKeyUrl = report.get("proof").get("public_key_url").asText();

      // Set the proof.jws value to an empty string
      ((ObjectNode) report.get("proof")).put("jws", "");

      // Canonicalize the JSON data according to RFC 8785
      JsonCanonicalizer canonicalizer = new JsonCanonicalizer(mapper.writeValueAsString(report));
      String canonicalizedReport = canonicalizer.getEncodedString();

      // Fetch the public key from the proof.public_key_url
      OkHttpClient client = new OkHttpClient();
      Request request = new Request.Builder().url(publicKeyUrl).build();
      Response response = client.newCall(request).execute();
      String publicKeyJson = response.body().string();

      // Parse the JWK set and extract the first key
      JsonNode keysNode = mapper.readTree(publicKeyJson).get("keys");
      JsonNode publicKeyNode = keysNode.get(0);
      JsonWebKey publicKeyJwk = JsonWebKey.Factory.newJwk(publicKeyNode.toString());

      // Construct the JWS object with detached payload
      JsonWebSignature jws = new JsonWebSignature();
      jws.setAlgorithmHeaderValue("EdDSA");
      jws.setKey(publicKeyJwk.getKey());
      jws.setCompactSerialization(jwsToken);
      jws.setPayload(canonicalizedReport);

      // Verify the JWS signature
      if (jws.verifySignature()) {
        System.out.println("Signature is valid.");
      } else {
        System.out.println("Signature verification failed.");
      }
    } catch (IOException | JoseException e) {
      e.printStackTrace();
    }
  }
}
{% /tab %}
{% tab language="csharp" %}
using System.Text;
using Newtonsoft.Json.Linq;
using Org.Webpki.JsonCanonicalizer;
using NSec.Cryptography;

class Program
{
    static void Main()
    {
        string jsonReport = File.ReadAllText("payload/identity_profile_report.json");
        JObject report = JObject.Parse(jsonReport);

        string jws = report["proof"]?["jws"]?.ToString() ?? throw new InvalidOperationException("JWS is missing");
        string publicKeyUrl = report["proof"]?["public_key_url"]?.ToString() ?? throw new InvalidOperationException("Public key URL is missing");

        report["proof"]!["jws"] = "";

        string canonicalizedReport = new JsonCanonicalizer(report.ToString()).GetEncodedString();

        string publicKey = FetchPublicKey(publicKeyUrl);

        bool isValid = VerifySignature(publicKey, jws, canonicalizedReport);
        Console.WriteLine($"Signature is valid: {isValid}");
    }

    static string FetchPublicKey(string url)
    {
        using (HttpClient client = new HttpClient())
        {
            HttpResponseMessage response = client.GetAsync(url).Result;
            response.EnsureSuccessStatusCode();
            string responseBody = response.Content.ReadAsStringAsync().Result;
            JObject keyData = JObject.Parse(responseBody);
            return keyData["keys"]?[0]?["x"]?.ToString() ?? throw new InvalidOperationException("Public key is missing");
        }
    }

    static bool VerifySignature(string publicKey, string jws, string payload)
    {
        string[] jwsParts = jws.Split('.');
        if (jwsParts.Length != 3)
        {
            throw new ArgumentException("Invalid JWS format");
        }

        string header = jwsParts[0];
        string signature = jwsParts[2];

        byte[] signatureBytes = Base64UrlDecode(signature);
        byte[] payloadBytes = Encoding.UTF8.GetBytes(payload);

        var publicKeyBytes = Base64UrlDecode(publicKey);
        var key = PublicKey.Import(SignatureAlgorithm.Ed25519, publicKeyBytes, KeyBlobFormat.RawPublicKey);

        // Create the data to verify (header + "." + payload)
        string dataToVerify = $"{header}.{Base64UrlEncode(payloadBytes)}";
        byte[] dataToVerifyBytes = Encoding.UTF8.GetBytes(dataToVerify);

        return SignatureAlgorithm.Ed25519.Verify(key, dataToVerifyBytes, signatureBytes);
    }

    static byte[] Base64UrlDecode(string input)
    {
        string base64 = input.Replace('-', '+').Replace('_', '/');
        switch (base64.Length % 4)
        {
            case 2: base64 += "=="; break;
            case 3: base64 += "="; break;
        }
        return Convert.FromBase64String(base64);
    }

    static string Base64UrlEncode(byte[] input)
    {
        string base64 = Convert.ToBase64String(input);
        return base64.Replace('+', '-').Replace('/', '_').TrimEnd('=');
    }
}
{% /tab %}
{% /code %}

### Reference

- JWS Detached Payload - [https://tools.ietf.org/html/rfc7515#appendix-F](https://tools.ietf.org/html/rfc7515#appendix-F)
- RFC 8785: JSON Canonicalization Scheme (JCS) - [https://datatracker.ietf.org/doc/html/rfc8785](https://datatracker.ietf.org/doc/html/rfc8785)
- RFC 7517: JSON Web Key (JWK) - [https://datatracker.ietf.org/doc/html/rfc7517](https://datatracker.ietf.org/doc/html/rfc7517)