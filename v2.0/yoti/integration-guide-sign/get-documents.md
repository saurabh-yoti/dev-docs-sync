---
type: page
title: Get documents
listed: true
slug: get-documents
description: 
index_title: Get documents
hidden: 
keywords: 
tags: 
---

Once signed, a full copy of the completed document can be obtained in a zip file by calling the 'completed document' endpoint.

## Endpoint

{% code %}
{% tab language="http" %}
Sandbox GET https://demo.api.yotisign.com/v2/envelopes/<envelopeId>/completed-documents 

Production GET https://api.yotisign.com/v2/envelopes/<envelopeId>/completed-documents
{% /tab %}
{% /code %}

Where envelopeID is the ID generated when creating the envelope request. this will be in the response body of the [create envelope request.](https://developers.yoti.com/yoti/create-an-envelope-request)

## Headers

The following elements are needed:

{% table %}
| Headers | Content | 
| ---- | ---- | 
| Content-Type | application/json | 
| Authorization | API Key to call the Yoti Sign API. This should be sent as a bearer token. | 
{% /table %}

## Example code

{% code %}
{% tab language="javascript" %}
const rp = require("request-promise");
const fs = require("fs");

const getDocuments = () => {
  const documents = {
    method: "GET",
    uri: "<BASE_URL>/v2/envelopes/<envelopeId>/completed-documents",
    headers: {
      authorization: "Bearer <API_KEY>",
    },
    encoding: null,
  };

  return rp(documents)
    .then((body) => fs.writeFileSync("example.zip", body))
    .catch((err) => err);
};

//send request
let results = await getDocuments();
{% /tab %}
{% tab language="php" %}
<?php

use GuzzleHttp\Client;
use GuzzleHttp\Psr7\Request;

$request = new Request(
    'GET',
    API_BASE_URL . "/envelopes/{$envelope_id}/completed-documents",
    [
        'Authorization' => 'Bearer ' . YOUR_API_KEY,
    ]
);

$client = new Client();
$response = $client->send($request);

$zip_file = $response->getBody();
{% /tab %}
{% tab language="java" %}
package com.yoti.sign;

import java.io.IOException;
import java.net.URI;

import org.apache.http.HttpResponse;
import org.apache.http.client.methods.HttpGet;
import org.apache.http.impl.client.CloseableHttpClient;
import org.apache.http.impl.client.HttpClients;

public class MainGetDocument {

    private static final String YOTI_SIGN_AUTH_TOKEN = "<YOUR_AUTH_TOKEN>";
    private static final String YOTI_SIGN_BASE_URL = "https://api.yotisign.com/v2";

    public static void main(String[] args) {
        CloseableHttpClient client = HttpClients.createDefault();

        final String envelopeId = "<YOUR_ENVELOPE_ID>";

        HttpGet httpGet = new HttpGet();
        httpGet.setHeader("Authorization", "Bearer " + YOTI_SIGN_AUTH_TOKEN);

        URI uri = URI.create(YOTI_SIGN_BASE_URL + "/envelopes/" + envelopeId + "/completed-documents");
        httpGet.setURI(uri);

        try {
            HttpResponse response = client.execute(httpGet);
            InputStream fileContents = response.getEntity().getContent();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
{% /tab %}
{% /code %}

If your GET request is successful, you will receive a zip file with the documents inside.

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
You will need to wait for all recipients to sign the documents before you can make this request
    </div>
</div>
{% /html %}

---

## Error codes

{% table %}
| Error Code | Description | 
| ---- | ---- | 
| 400 | Bad Request or invalid payload | 
| 401 | Unauthorised request, example: invalid API key | 
| 403 | Forbidden, requesting user did not create the envelope | 
| 404 | The envelope ID couldn’t be found | 
{% /table %}