---
type: page
title: Find envelope
listed: true
slug: find-envelope
description: 
index_title: Find envelope
hidden: 
keywords: 
tags: 
---

The Yoti Sign API has a ‘find’ function. This allows you to find the envelope details for specified envelopes.

{% code %}
{% tab language="http" %}
Sandbox: 
POST https://demo.api.yotisign.com/v2/organisations/envelopes/find
{% /tab %}
{% /code %}

{% code %}
{% tab language="http" %}
Production: 
POST https://api.yotisign.com/v2/organisations/envelopes/find
{% /tab %}
{% /code %}

---

## Header explained

The following elements are needed:

{% table %}
| Headers | Content | 
| ---- | ---- | 
| Content-Type | application/json | 
| Authorization | API Key to call the Yoti Sign API. This should be sent as a bearer token. | 
{% /table %}

---

### Request body

{% code %}
{% tab language="json" %}
{
      "envelope_ids": [
    		<id>,
    		<id>
 		 ]
    }
{% /tab %}
{% /code %}

---

## Example code

{% code %}
{% tab language="javascript" %}
const rp = require("request-promise");
const findEnvelope = () => {
  const request = {
    method: "POST",
    uri: "<BASE_URL>/v2/organisations/envelopes/find",
    body: JSON.stringify({
      "envelope_ids": [
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
let result = await findEnvelope();
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

public class MainFindEnvelope {

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
        json.append("\"envelope_ids\":\"[<id>, <id>]\",");
        json.append("}");
      
      httpPost.setEntity(new StringEntity(json.toString()));
      
        URI uri = URI.create(YOTI_SIGN_BASE_URL + "/organisations/envelopes/find");
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
    API_BASE_URL . "/organisations/envelopes/find",
    [
        'headers' => [
          'Authorization' => 'Bearer ' . YOUR_API_KEY,
          'Content-Type'  => 'application/json',
         ],
        'body' => [
        	"envelope_ids" => [
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
        RequestUri = new Uri("https://api.yotisign.com/v2/organisations/envelopes/find")
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
		
	req, err := http.NewRequest("POST", "<BASE_URL>/organisations/envelopes/find", payload)
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

---

## Example Response

{% code %}
{% tab language="json" %}
{
  "envelopes": [
    {
      "envelope_id": string,
      "envelope": string,
      "status": string,
      "created_at": string
    }
  ]
}
{% /tab %}
{% /code %}

---

## Error codes

If the request is unsuccessful a response code and a message will be sent