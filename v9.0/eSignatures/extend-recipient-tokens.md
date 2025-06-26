---
type: page
title: Extend recipient tokens
listed: true
slug: extend-recipient-tokens
description: 
index_title: Extend recipient tokens
hidden: 
keywords: 
tags: 
---

The Yoti sign API has an endpoint that refreshes the expiry of the recipient token. An array of tokens is passed in the body of the request. If refreshing multiple tokens, the tokens must belong to the same envelope, and this can be done for any envelope regardless of whether it is an embedded one or not.

{% code %}
{% tab language="http" %}
Sandbox: 
POST https://demo.api.yotisign.com/v2/envelopes/:envelopeId/extend-tokens
{% /tab %}
{% /code %}

{% code %}
{% tab language="http" %}
Production: 
POST https://api.yotisign.com/v2/envelopes/:envelopeId/extend-tokens
{% /tab %}
{% /code %}

---

## Headers Explained

The following elements are needed:

{% table %}
| Headers | Content | 
| ---- | ---- | 
| Authorization | API Key to call the Yoti Sign API. This should be sent as a bearer token. | 
| Content-Type | application/json | 
{% /table %}

---

## Request Body

{% code %}
{% tab language="json" %}
{ 
  recipient_tokens: ["<recipient_token_uuid>", "<recipient_token_uuid>"] 
}
{% /tab %}
{% /code %}

---

## Example Code

{% code %}
{% tab language="javascript" %}
const rp = require("request-promise");
const extendToken = () => {
  const request = {
    method: "POST",
    uri: "<BASE_URL>/v2/envelopes/:envelopeId/extend-tokens",
    body: JSON.stringify({
      "recipient_tokens": [
    		<id>,
    		<id>
 		 ]
    }),
    headers: {
      authorization: "Bearer <API_KEY>",
    },
  };

  return rp(request)
    .then((body) => body)
    .catch((err) => err);
};

//send request
let result = await extendToken();
{% /tab %}
{% tab language="java" %}
package com.yoti.sign;

import java.io.IOException;
import java.net.URI;

import javax.json.Json;
import javax.json.JsonObject;
import javax.json.JsonReader;

import org.apache.http.HttpResponse;
import org.apache.http.client.methods.HttpGet;
import org.apache.http.impl.client.CloseableHttpClient;
import org.apache.http.impl.client.HttpClients;

public class MainExtendToken {

    private static final String YOTI_SIGN_AUTH_TOKEN = "<YOUR_AUTH_TOKEN>";
    private static final String YOTI_SIGN_BASE_URL = "https://api.yotisign.com/v2";

    public static void main(String[] args) {
        CloseableHttpClient client = HttpClients.createDefault();

        final String envelopeId = "<YOUR_ENVELOPE_ID>";

        HttpPost httpPost = new HttpPost();
        httpPost.setHeader("Authorization", "Bearer " + YOTI_SIGN_AUTH_TOKEN);

      // add request body
      StringBuilder json = new StringBuilder();
        json.append("{");
        json.append("\"recipient_tokens\":\"[<id>, <id>]\",");
        json.append("}");
      
      httpPost.setEntity(new StringEntity(json.toString()));
      
        URI uri = URI.create(YOTI_SIGN_BASE_URL + "/envelopes/:envelopeId/extend-tokens");
        httpPost.setURI(uri);

        try {
            HttpResponse response = client.execute(httpPost);
            JsonReader reader = Json.createReader(response.getEntity().getContent());

            JsonObject envelopeInfo = reader.readObject(); // Access envelopeInfoHere
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
{% /tab %}
{% tab language="php" %}
<?php

use GuzzleHttp\Client;
use GuzzleHttp\Psr7\Request;

$request = new Request(
    'POST',
    API_BASE_URL . "/envelopes/:envelopeId/extend-tokens",
    [
        'headers' => [
          'Authorization' => 'Bearer ' . YOUR_API_KEY,
          'Content-Type'  => 'application/json',
         ],
        'body' => [
        	"recipient_tokens" => [
          	<id>,
    				<id>
          ],
    		],
    ]
);

$client = new Client();
$response = $client->send($request);

$json = json_decode($response->getBody());
{% /tab %}
{% tab language="csharp" %}
using (HttpRequestMessage request = new HttpRequestMessage
    {
        Method = new HttpMethod("POST"),
        RequestUri = new Uri("https://api.yotisign.com/v2/envelopes/:envelopeId/extend-tokens")
    })
    {
        request.Headers.Add("Authorization", "Bearer " + "<API_KEY>");
        // add request body

        using (HttpClient httpClient = new HttpClient())
        {
            HttpResponseMessage response = httpClient.SendAsync(request).Result;

            string responseContent = response.Content.ReadAsStringAsync().Result;

            return new JsonResult(
                responseContent,
                new JsonSerializerOptions
                {
                    WriteIndented = true,
                    Encoder = JavaScriptEncoder.UnsafeRelaxedJsonEscaping
                });
        }
    }
{% /tab %}
{% tab language="go" %}
options := `{}`

	payload := &bytes.Buffer{}
	writer := multipart.NewWriter(payload)
	_ = writer.WriteField("options", options)
		
	req, err := http.NewRequest("POST", "<BASE_URL>/envelopes/:envelopeId/extend-tokens", payload)
	req.Header.Add("Authorization", "Bearer <API_KEY>")
	req.Header.Add("Content-Type", "application/json")
	
	
	client := &http.Client{}
	response, err := client.Do(req)

	if err != nil {
		fmt.Println(err)
	} else {
		result, _ := ioutil.ReadAll(response.Body)
	}
{% /tab %}
{% /code %}