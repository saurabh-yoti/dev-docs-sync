---
type: page
title: Search envelope
listed: true
slug: search-envelope
description: 
index_title: Search envelope
hidden: 
keywords: 
tags: 
---

The Yoti Sign API has an ‘search’ function. This allows you to search for envelopes with filters to only retrieve  envelopes with specific attributes.

{% code %}
{% tab language="http" %}
Sandbox: 
GET https://demo.api.yotisign.com/v2/organisations/envelopes/search
{% /tab %}
{% /code %}

{% code %}
{% tab language="http" %}
Production: 
GET https://api.yotisign.com/v2/organisations/envelopes/search
{% /tab %}
{% /code %}

---

## Headers explained

The following elements are needed:

{% table %}
| Headers | Content | 
| ---- | ---- | 
| Authorization | API Key to call the Yoti Sign API. This should be sent as a bearer token. | 
{% /table %}

---

## Example code

{% code %}
{% tab language="javascript" %}
const rp = require("request-promise");
const searchEnvelope = () => {
  const request = {
    method: "GET",
    uri: "<BASE_URL>/v2/organisations/envelopes/search",
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


        HttpGet httpGet = new HttpGet();
        httpGet.setHeader("Authorization", "Bearer " + YOTI_SIGN_AUTH_TOKEN);

      // add request body
        URI uri = URI.create(YOTI_SIGN_BASE_URL + "/organisations/envelopes/search");
        httpGet.setURI(uri);

        try {
            HttpResponse response = client.execute(httpGet);
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
    'GET',
    API_BASE_URL . "/organisations/envelopes/search",
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
        Method = new HttpMethod("GET"),
        RequestUri = new Uri("https://api.yotisign.com/v2/organisations/envelopes/search")
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
req, err := http.NewRequest("GET", "<BASE_URL>/v2/organisations/envelopes/search", nil)

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

### Query Parameters

With the search request you have the option to add the below query parameters to filter which envelopes are returned.

{% table widths="120,0" %}
| Parameter | Description | Example | 
| ---- | ---- | ---- | 
| **from_date** | the start position in the list sorted by created_at limited to YYYY-MM-DD. If this property isn't present in the request the default value of 3 months in the past will be used | /v2/organisation/envelopes/search?from_date=2021-01-01 | 
| **to_date** | the end position in the list sorted by created_at limited to YYYY-MM-DD.  If this property isn’t present in the request the default value of tomorrow’s date at 00:00 will be used | /v2/organisation/envelopes/search?to_date=2021-02-02 | 
| **status** | the statuses of the envelopes. If this property isn’t present in the request all status types will exist in the search | /v2/organisation/envelopes/search?status[]=active&status[]=complete | 
| **offset** | the starting position in the list of all sorted envelopes, default value is 1 | /v2/organisation/envelopes/search?offset=1 | 
| **limit** | the number of results to return, default value is 10 | /v2/organisation/envelopes/search?limit=50 | 
{% /table %}

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
  ],
  "total": number
}
{% /tab %}
{% /code %}

## Error codes

If the request is unsuccessful a response code and a message will be sent