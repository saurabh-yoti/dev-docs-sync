---
type: page
title: Archive envelope
listed: true
slug: archive-envelope
description: 
index_title: Archive envelope
hidden: 
keywords: 
tags: 
---

The Yoti Sign API has an ‘archive’ function. This allows senders to cancel an envelope that has been sent for signing, but has not yet been signed by all recipients. The envelope will then no longer be available for signing.

{% code %}
{% tab language="http" %}
Sandbox PATCH https://demo.api.yotisign.com/v2/envelopes/<envelopeId>

Production PATCH https://api.yotisign.com/v2/envelopes/<envelopeId>
{% /tab %}
{% /code %}

The Archive Envelope endpoint returns a status code of 204 if successful.

## Example code

{% code %}
{% tab language="javascript" %}
const rp = require("request-promise");
const archiveEnvelope = () => {
  const request = {
    method: "PATCH",
    uri: "<BASE_URL>/v2/envelopes/<envelopeId>",
    headers: {
      authorization: "Bearer <API_KEY>",
    },
  };

  return rp(request)
    .then((body) => body)
    .catch((err) => err);
};

//send request
let result = await archiveEnvelope();
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

public class MainArchiveEnvelope {

    private static final String YOTI_SIGN_AUTH_TOKEN = "<YOUR_AUTH_TOKEN>";
    private static final String YOTI_SIGN_BASE_URL = "https://api.yotisign.com/v2";

    public static void main(String[] args) {
        CloseableHttpClient client = HttpClients.createDefault();

        final String envelopeId = "<YOUR_ENVELOPE_ID>";

        HttpPatch httpPatch = new HttpPatch();
        httpPatch.setHeader("Authorization", "Bearer " + YOTI_SIGN_AUTH_TOKEN);

        URI uri = URI.create(YOTI_SIGN_BASE_URL + "/envelopes/" + envelopeId);
        httpPatch.setURI(uri);

        try {
            HttpResponse response = client.execute(httpPatch);
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
    'PATCH',
    API_BASE_URL . "/envelopes/{$envelope_id}",
    [
        'Authorization' => 'Bearer ' . YOUR_API_KEY,
    ]
);

$client = new Client();
$response = $client->send($request);

$json = json_decode($response->getBody());
{% /tab %}
{% tab language="csharp" %}
using (HttpRequestMessage request = new HttpRequestMessage
    {
        Method = new HttpMethod("PATCH"),
        RequestUri = new Uri("https://api.yotisign.com/v2/envelopes/<envelopeId>")
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
req, err := http.NewRequest("PATCH", "<BASE_URL>/v2/envelopes/<envelopeId>", nil)
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

## Error codes

If the request is unsuccessful a response code and a message will be sent