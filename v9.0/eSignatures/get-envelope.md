---
type: page
title: Get envelope
listed: true
slug: get-envelope
description: 
index_title: Get envelope
hidden: 
keywords: 
tags: 
---

This endpoint allows you to query the Yoti Sign API for the current state of an envelope request:

{% code %}
{% tab language="http" %}
Sandbox:
GET https://demo.api.yotisign.com/v2/envelopes/<envelopeId>
{% /tab %}
{% /code %}

{% code %}
{% tab language="http" %}
Production: 
GET https://api.yotisign.com/v2/envelopes/<envelopeId>
{% /tab %}
{% /code %}

---

### Header explained

The following elements are needed:

{% table %}
| Header | Description | 
| ---- | ---- | 
| Authorization (header) | API Key to call the Yoti Sign API. This should be sent as a bearer token. | 
| Content-Type (header) | application/json | 
{% /table %}

---

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
  "envelope_id": "<envelopeId>",
  "status": "ACTIVE",
  "details": {
    "recipients": [
      {
        "id": "uuid",
        "sign_status": "UNSIGNED",
        "name": "name1",
        "email": "email1@email.com",
        "auth_type": "sign-auth",
        "role": "Signee"
      }
    ]
  }
}
{% /tab %}
{% tab language="json" title="Archived" %}
{
  "envelope_id": "<env id>",
  "status": "ARCHIVED",
  "details": {
    "recipients": [
      {
        "sign_status": "UNSIGNED",
        "name": "name1",
        "email": "email1@email.com",
        "auth_type": "sign-auth",
        "role": "Signee"
      }
    ],
    "archived_at": "YYYY-MM-DD Thh:mm:ss.ssssZ"
  }
}
{% /tab %}
{% tab language="json" title="Completed" %}
{
  "envelope_id": "<envelopeId>",
  "status": "COMPLETE",
  "details": {
    "recipients": [
      {
        "id": "uuid"
        "sign_status": "SIGNED",
        "name": "name1",
        "email": "email1@gmail.com",
        "auth_type": "no-auth",
        "role": "Signee",
        "signed_at": "YYYY-MM-DD Thh:mm:ss.ssssZ",
        "invitation_email_queued_at": "YYYY-MM-DD Thh:mm:ss.ssssZ",
        "sign_group_order": 1,
        "ip_address": "1.2.3.4",
        "last_email_status": "SENT",
        "tags": [
          {
            "name": "first1",
            "tag_group_name": "",
            "was_optional": "<true/false>",
            "value": "true"
          }
        ]
      }
    ],
    "completed_at": "YYYY-MM-DD Thh:mm:ss.ssssZ"
  }
}
{% /tab %}
{% tab language="json" title="Errored" %}
{
  "envelope_id": "<envelopeId>,
  "status": "ERRORED",
  "details": {
    "errors": [
      {
        "file_name": "sample.pdf",
        "code": "<ERROR MESSAGE>"
      }
    ]
  }
}
{% /tab %}
{% /code %}

For a completed envelope, and extra details which are included in the response will appear as 'tags' in the response body.

---

### Status

This is the status of the envelope.

{% table %}
| Status | Description | 
| ---- | ---- | 
| QUEUED | The envelope is being processed, before being sent to the recipients. | 
| ACTIVE | The envelope has been successfully sent to recipients. | 
| ARCHIVED | The envelope has been archived. | 
| COMPLETE | The envelope has been signed by all the recipients. | 
| ERRORED | There has been an error in the creation of the envelope | 
{% /table %}

---

### Details

This will contain all the relevant details for the envelope including recipients or errors.

---

### Sign_Status

This is the status of the envelope.

{% table widths="110" %}
| Status | Description | 
| ---- | ---- | 
| SIGNED | The envelope has been signed.\n\n\n\n- An additional **signed_at** field is populated on the recipient object with the ISO string timestamp of the signing time. | 
| UNSIGNED | The envelope has not been signed. | 
{% /table %}

---

### Additional

These fields will appear in certain scenarios:

{% table %}
| Attribute | Description | 
| ---- | ---- | 
| errors | If an error occurs then you will be provided with the file name causing the error if applicable and an error message (see below for a list of error messages) | 
| signed_at | UTC Timestamp for when the recipient has signed the document | 
| archived_at | UTC Timestamp for when the envelope has been Archived | 
{% /table %}

---

### Example code

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
{% /code %}

---

### Error codes

If the request is unsuccessful a response code and a message will be sent:

{% table %}
| Response | Description | 
| ---- | ---- | 
| 400 | Bad Request, example: id provided not a UUID | 
| 401 | Unauthorised request, example: requesting the status on an envelope you are not authorized to view | 
| 403 | Forbidden, requesting user did not create the envelope | 
| 404 | The envelope ID couldn’t be found | 
{% /table %}