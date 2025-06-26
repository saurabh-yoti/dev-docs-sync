---
type: page
title: Send Reminders
listed: true
slug: send-reminders
description: 
index_title: Send Reminders
hidden: 
keywords: 
tags: 
---

The Yoti Sign API has an ‘send-reminder’ function. This allows you to send recipients a reminder to sign an envelope.

{% code %}
{% tab language="http" %}
Sandbox: 
POST https://demo.api.yotisign.com/v2/envelopes/{envelope_id}/recipients/{recipient_id}/send-reminder
{% /tab %}
{% /code %}

{% code %}
{% tab language="http" %}
Production: 
POST https://api.yotisign.com/v2/envelopes/{envelope_id}/recipients/{recipient_id}/send-reminder
{% /tab %}
{% /code %}

---

## Headers explained

The following elements are needed:

{% table %}
| Headers | Content | 
| ---- | ---- | 
| Authorization | API Key to call the Yoti Sign API. This should be sent as a bearer token. | 
| Content-Type | application/json | 
{% /table %}

---

## Example code

{% code %}
{% tab language="javascript" %}
const rp = require("request-promise");
const searchEnvelope = () => {
  const request = {
    method: "POST",
    uri: "<BASE_URL>/v2/envelopes/{envelope_id}/recipients/{recipient_id}/send-reminder",
    headers: {
      authorization: "Bearer <API_KEY>",
    },
  };

  return rp(request)
    .then((body) => body)
    .catch((err) => err);
};

//send request
let result = await searchEnvelope();
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

public class MainSearchEnvelope {

    private static final String YOTI_SIGN_AUTH_TOKEN = "<YOUR_AUTH_TOKEN>";
    private static final String YOTI_SIGN_BASE_URL = "https://api.yotisign.com/v2";

    public static void main(String[] args) {
        CloseableHttpClient client = HttpClients.createDefault();


        HttpPost httpPost = new HttpGet();
        httpPost.setHeader("Authorization", "Bearer " + YOTI_SIGN_AUTH_TOKEN);

      // add request body
        URI uri = URI.create(YOTI_SIGN_BASE_URL + "/envelopes/{envelope_id}/recipients/{recipient_id}/send-reminder");
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
    API_BASE_URL . "/envelopes/{envelope_id}/recipients/{recipient_id}/send-reminder",
    [
        'headers' => [
          'Authorization' => 'Bearer ' . YOUR_API_KEY,
          'Content-Type'  => 'application/json',
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
        RequestUri = new Uri("https://api.yotisign.com/v2/envelopes/{envelope_id}/recipients/{recipient_id}/send-reminder")
    })
    {
        request.Headers.Add("Authorization", "Bearer " + "<API_KEY>");
        

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
req, err := http.NewRequest("POST", "<BASE_URL>/v2/envelopes/{envelope_id}/recipients/{recipient_id}/send-reminder", nil)

req.Header.Add("Authorization", "Bearer <API_KEY>")

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
  "recipient_id": {{ recipient_id }}
}
{% /tab %}
{% /code %}

## Error codes

If the request is unsuccessful a response code and a message will be sent