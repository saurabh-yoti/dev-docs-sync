---
type: page
title: Envelope status
listed: true
slug: recipients
description: 
index_title: Envelope status
hidden: 
keywords: 
tags: 
---

## Get envelope request

This endpoint allows you to query the Yoti Sign service for the current state of an envelope request:

{% code %}
{% tab language="http" %}
Sandbox GET https://demo.api.yotisign.com/v2/envelopes/<envelopeId>

Production GET https://api.yotisign.com/v2/envelopes/<envelopeId>
{% /tab %}
{% /code %}

---

## Header explained

The following elements are needed:

{% table %}
| Header | Description | 
| ---- | ---- | 
| Authorization (header) | API Key to call the Yoti Sign API. This should be sent as a bearer token. | 
| Content-Type (header) | multipart/form-data | 
{% /table %}

### Response

On success, we return a 200 with a JSON body matching the following schema. The response seen whilst the files are being processed and the envelope is being sealed is shown below:

{% code %}
{% tab language="json" %}
{
    "envelope_id": "<envelopeId>",
    "status": "QUEUED"
}
{% /tab %}
{% /code %}

Click the tabs for different status responses:

{% code %}
{% tab language="json" title="Active" %}
{
   "envelope_id":"<envelopeId>",
   "status":"ACTIVE",
   "details":{
      "recipients":[
         {
            "sign_status":"UNSIGNED",
            "name":"name1",
            "email":"email1@email.com",
            "auth_type":"sign-auth",
            "role":"Signee"
         }
      ]
   }
}
{% /tab %}
{% tab language="json" title="Archived" %}
{
   "envelope_id":"<env id>",
   "status":"ARCHIVED",
   "details":{
      "recipients":[
         {
            "sign_status":"UNSIGNED",
            "name":"name1",
            "email":"email1@email.com",
            "auth_type":"sign-auth",
            "role":"Signee"
         }
      ],
      "archived_at":"YYYY-MM-DD Thh:mm:ss.ssssZ"
   }
}
{% /tab %}
{% tab language="json" title="Completed" %}
{
   "envelope_id":"<envelopeId>",
   "status":"COMPLETE",
   "details":{
      "recipients":[
         {
            "sign_status":"SIGNED",
            "name":"name1",
            "email":"email1@gmail.com",
            "auth_type":"no-auth",
            "role":"Signee",
            "signed_at":"YYYY-MM-DD Thh:mm:ss.ssssZ"
         }
      ],
      "completed_at":"YYYY-MM-DD Thh:mm:ss.ssssZ"
   }
}
{% /tab %}
{% tab language="json" title="Errored" %}
{
	"envelope_id": "<envelopeId>",
	"status": "FILE_UPLOAD_ERROR",
	"details": {
		"errors":[
			{
				"code": "<error code>",
				"message": "The human readable error message"
			}
		]
	}
}
{% /tab %}
{% /code %}

{% table %}
| Attribute | Description/Example | 
| ---- | ---- | 
| Status | QUEUED - The envelope is being processed, before being sent to the recipients\n\n\nACTIVE - The envelope has been successfully sent to recipients\n\n\nARCHIVED- The envelope has been archived\nCOMPLETE - The envelope has been signed by all the recipients\n\n\nERRORED - There has been an error in the creation of the envelope | 
| details | This will contain all the relevant details for the envelope including recipients or errors. Read below for further explanation | 
| sign_status | SIGNED, UNSIGNED | 
| errors | If an error occurs then you will be provided with the file name causing the error if applicable and an error message (see below for a list of error messages) | 
| signed_at | Timestamp for when the recipient has signed the document | 
| archived_at | Timestamp for when the envelope has been Archived | 
{% /table %}

## Example code

{% code %}
{% tab language="javascript" %}
const rp = require("request-promise");

const getEnvelope = () => {
  const request = {
    method: "GET",
    uri: "https://api.yotisign.com/v2/envelopes/<envelopeId>",
    headers: {
      authorization: "Bearer <API_KEY>",
    },
  };

  return rp(request)
    .then((body) => body)
    .catch((err) => err);
};

//send request
let result = await getEnvelope();
{% /tab %}
{% tab language="php" %}
<?php

use GuzzleHttp\Client;
use GuzzleHttp\Psr7\Request;

$request = new Request(
    'GET',
    API_BASE_URL . "/envelopes/{$envelope_id}",
    [
        'Authorization' => 'Bearer ' . YOUR_API_KEY,
    ]
);

$client = new Client();
$response = $client->send($request);

$json = json_decode($response->getBody());
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

public class MainGetEnvelope {

    private static final String YOTI_SIGN_AUTH_TOKEN = "<YOUR_AUTH_TOKEN>";
    private static final String YOTI_SIGN_BASE_URL = "https://api.yotisign.com/v2";

    public static void main(String[] args) {
        CloseableHttpClient client = HttpClients.createDefault();

        final String envelopeId = "<YOUR_ENVELOPE_ID>";

        HttpGet httpGet = new HttpGet();
        httpGet.setHeader("Authorization", "Bearer " + YOTI_SIGN_AUTH_TOKEN);

        URI uri = URI.create(YOTI_SIGN_BASE_URL + "/envelopes/" + envelopeId);
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
{% tab language="go" %}
type EnvelopeStatus struct {
		EnvelopeID string `json:"envelope_id"`
		Status     string `json:"status"`
		Details    struct {
			Recipients []struct {
				SignStatus string `json:"sign_status"`
				Name       string `json:"name"`
				Email      string `json:"email"`
				AuthType   string `json:"auth_type"`
				Role       string `json:"role"`
				SignedAt   string `json:"signed_at"`
			} `json:"recipients"`
			CompletedAt string `json:"completed_at"`
			ArchivedAt string `json:"archived_at"`
		} `json:"details"`
	}


	req, err := http.NewRequest("GET", "https://api.yotisign.com/v2/envelopes" + envId.EnvelopeID, nil)
	req.Header.Add("Authorization", "Bearer <API_KEY>")

	client := &http.Client{}
	response, err := client.Do(req)

	if err != nil {
		fmt.Println(err)
	} else {
		resBytes, _ := ioutil.ReadAll(response.Body)
		var envelopeStatus EnvelopeStatus
		err = json.Unmarshal(resBytes, &envelopeStatus)
	}
{% /tab %}
{% tab language="csharp" %}
using (HttpRequestMessage request = new HttpRequestMessage
    {
        Method = HttpMethod.Get,
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
{% /code %}

## Error codes

If the request is unsuccessful a response code and a message will be sent

{% table %}
| Response | Description | 
| ---- | ---- | 
| 400 | Bad Request, example: id provided not a UUID | 
| 401 | Unauthorised request, example: requesting the status on an envelope you are not authorized to view | 
| 403 | Forbidden, requesting user did not create the envelope | 
| 404 | The envelope ID couldn’t be found | 
{% /table %}

---

## Archive Envelope

Yoti Sign has an ‘archive’ function. This allows senders to cancel an envelope that has been sent for signing, but has not yet been signed by all recipients. The envelope will then no longer be available for signing.

{% code %}
{% tab language="http" %}
Sandbox PATCH https://demo.api.yotisign.com/v2/envelopes/<envelopeId>

Production PATCH https://api.yotisign.com/v2/envelopes/<envelopeId>
{% /tab %}
{% /code %}

The Archive Envelope endpoint returns a status code of 204 if successful.

### Example code

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
{% /code %}

## Error codes

If the request is unsuccessful a response code and a message will be sent

{% table %}
| Response | Description | 
| ---- | ---- | 
| 400 | Bad Request, example: id provided not a UUID | 
| 401 | Unauthorised request, example: invalid API key | 
| 403 | Forbidden, requesting user did not create the envelope | 
| 404 | The envelope ID couldn’t be found | 
| 409 | The envelope has already been archived | 
{% /table %}