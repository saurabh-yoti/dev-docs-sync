---
type: page
title: Re-send completion pack
listed: true
slug: re-send-completion-pack
description: 
index_title: Re-send completion pack
hidden: 
keywords: 
tags: 
---

The re-send completion pack feature allows you to re-send the completion pack for the specified recipient.

{% code %}
{% tab language="http" %}
PATCH https://api.yotisign.com/v2/envelopes/<envelopeId>/recipients/<recipient_id>/resend-completion-pack
{% /tab %}
{% /code %}

## Example code

{% code %}
{% tab language="javascript" %}
const rp = require("request-promise");
const resendPack = () => {
  const request = {
    method: "PATCH",
    uri: "<BASE_URL>/v2/envelopes/<envelopeId>/recipients/<recipient_id>/resend-completion-pack",
    headers: {
      authorization: "Bearer <API_KEY>",
    },
  };

  return rp(request)
    .then((body) => body)
    .catch((err) => err);
};

//send request
let result = await resendPack();
{% /tab %}
{% tab language="php" %}
// Cli<?php

use GuzzleHttp\Client;
use GuzzleHttp\Psr7\Request;

$request = new Request(
    'PATCH',
    API_BASE_URL . "/envelopes/{$envelope_id}/recipients/{$recipient_id}/resend-completion-pack",
    [
        'Authorization' => 'Bearer ' . YOUR_API_KEY,
    ]
);

$client = new Client();
$response = $client->send($request);

$json = json_decode($response->getBody());ck to edit code
{% /tab %}
{% tab language="csharp" %}
// Click to edit codeusing (HttpRequestMessage request = new HttpRequestMessage
    {
        Method = new HttpMethod("PATCH"),
        RequestUri = new Uri("https://api.yotisign.com/v2/envelopes/<envelopeId>/recipients/<recipient_id>/resend-completion-pack")
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
req, err := http.NewRequest("PATCH", "<BASE_URL>/v2/envelopes/<envelopeId>/recipients/<recipient_id>/resend-completion-pack", nil)
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

{% table widths="115" %}
| Error Code | Description | 
| ---- | ---- | 
| 400 | Bad request or invalid payload | 
| 409 | The envelope is not completed | 
| 410 | The total number of requests to resend the recipient completion pack has exceeded the limit | 
| 429 | Please wait 5 minutes before retrying | 
| 404 | The recipient couldn't be found | 
{% /table %}