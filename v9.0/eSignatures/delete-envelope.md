---
type: page
title: Delete Envelope
listed: true
slug: delete-envelope
description: 
index_title: Delete Envelope
hidden: 
keywords: 
tags: 
---

The Yoti sign API has the functionality to delete envelopes on demand.

{% code %}
{% tab language="http" %}
Sandbox: 
DELETE https://demo.api.yotisign.com/v2/envelopes/{envelope_id}
{% /tab %}
{% /code %}

{% code %}
{% tab language="http" %}
Production: 
DELETE https://api.yotisign.com/v2/envelopes/{envelope_id}
{% /tab %}
{% /code %}

---

### Headers Explained

The following elements are needed:

{% table %}
| Headers | Content | 
| ---- | ---- | 
| Authorization | API Key to call the Yoti Sign API. This should be sent as a bearer token. | 
{% /table %}

---

### Example code

{% code %}
{% tab language="javascript" %}
const rp = require("request-promise");
const deleteEnvelope = () => {
  const request = {
    method: "DELETE",
    uri: "<BASE_URL>/v2/envelopes/{envelope_id}",
    headers: {
      authorization: "Bearer <API_KEY>",
    },
  };

  return rp(request)
    .then((body) => body)
    .catch((err) => err);
};

//send request
let result = await deleteEnvelope();
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

public class MainDeleteEnvelope {

    private static final String YOTI_SIGN_AUTH_TOKEN = "<YOUR_AUTH_TOKEN>";
    private static final String YOTI_SIGN_BASE_URL = "https://api.yotisign.com/v2";

    public static void main(String[] args) {
        CloseableHttpClient client = HttpClients.createDefault();


        HttpDelete httpDelete = new HttpDelete();
        httpDelete.setHeader("Authorization", "Bearer " + YOTI_SIGN_AUTH_TOKEN);

      // add request body
        URI uri = URI.create(YOTI_SIGN_BASE_URL + "/envelopes/{envelope_id}");
        httpPost.setURI(uri);

        try {
            HttpResponse response = client.execute(httpDelete);
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
    'DELETE',
    API_BASE_URL . "/envelopes/{envelope_id}",
    [
        'headers' => [
          'Authorization' => 'Bearer ' . YOUR_API_KEY
         ],
    ]
);

$client = new Client();
$response = $client->send($request);

$json = json_decode($response->getBody());
{% /tab %}
{% /code %}

---

### Error codes

If the request is unsuccessful a response code and a message will be sent