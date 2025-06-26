---
type: page
title: Embedded envelope request
listed: true
slug: embedded-envelope
description: 
index_title: Embedded envelope request
hidden: 
keywords: 
tags: 
---

To see the flow of a standard envelope request please try out our demo [here](https://yoti.world/yoti-sign/) and switch our toggle on for embedded signing. We break down each section throughout the documentation so do continue reading.

{% badge type="error" text="Important" /%} Authentication is important. Please ensure that any user signing through the embedded version are authenticated. You can do this by validating the email address or doing an IDV check on the user.

These endpoint allows you to create an envelope request by sending one or more documents:

#### Sandbox

{% code %}
{% tab language="http" title="" %}
POST https://demo.api.yotisign.com/v2/embedded-envelopes
POST https://demo.www.yotisign.com/embedded/sign/{your_token}
{% /tab %}
{% /code %}

#### Production

{% code %}
{% tab language="http" %}
POST https://api.yotisign.com/v2/embedded-envelopes
POST https://www.yotisign.com/embedded/sign/{your_token}
{% /tab %}
{% /code %}

Below is an example of the full request for creating an envelope.

{% code %}
{% tab language="json" %}
{
    "name": "envelope name",
    "emails": {
        "invitation": {
            "body": {
                "message": "Please sign this document"
            }
        }
    },
    "recipients": [
        {
            "name": "User 1",
            "email": "user1@gtest.com",
            "role": "Signee",
            "auth_type": "no-auth", 
            "sign_group": 1,
            "tags": [
                {
                    "page_number": 1,
                    "x": 0.1,
                    "y": 0.1,
                    "type": "signature",
                    "optional": false,
                    "file_name": "myfile.pdf"
                }
            ],
            "event_notifications": []
        }
    ],
    "notifications": {
        "destination": "https://mysite.com/events",
        "subscriptions": [
            "envelope_completion"
        ]
    },
      "branding":
    {
        "logo_options":
        {
            "logo_choice": "brand_powered_by_yoti",
            "logo_base64": "base64-encoded-PNG-image"
        },
        "primary_color": "#000",
        "primary_color_hover": "#c0c0c0",
        "on_primary_color": "#fff",
        "secondary_color": "#00ffff",
        "secondary_color_hover": "#d2691e"
    },
    "parent_redirect_urls":{
        "success":"https://someurl.com/success",
        "failure":"https://someurl.com/failure"
    }
}
{% /tab %}
{% /code %}

Recipient signers and witnesses can be assigned tags but they are not required. To assign a witness with no tags to a signer, add "witness": {} to the recipient JSON object.

Through embedded signing, any required signing order should be controlled entirely by the integrator. It is recommended to utilise webhook notifications to understand when recipients have signed.

---

## Example code

{% code %}
{% tab language="javascript" %}
const rp = require("request-promise");
const fs = require("fs");

const options = {}; //options object

const createEnvelope = () => {
  const request = {
    method: "POST",
    uri: `<BASE_URL>/v2/embedded-envelopes`,
    formData: {
      file: fs.createReadStream("path/to.pdf"),
      options: JSON.stringify(options),
    },
    headers: {
      authorization: "Bearer <API_KEY>",
    },
  };

  return rp(request)
    .then((body) => body)
    .catch((err) => err);
};

//send request
let result = await createEnvelope();
{% /tab %}
{% tab language="java" %}
package com.yoti.sign;

import java.io.File;
import java.io.IOException;
import java.net.URI;

import javax.json.Json;
import javax.json.JsonObject;
import javax.json.JsonReader;

import org.apache.http.HttpResponse;
import org.apache.http.client.methods.HttpPost;
import org.apache.http.entity.ContentType;
import org.apache.http.entity.mime.MultipartEntityBuilder;
import org.apache.http.impl.client.CloseableHttpClient;
import org.apache.http.impl.client.HttpClients;

public class Example {

    private static final String YOTI_SIGN_AUTH_TOKEN = "<YOUR_AUTH_TOKEN>";
    private static final String YOTI_SIGN_BASE_URL = "https://api.yotisign.com/v2";

    public static void main(String[] args) {
        
        // Create the client and HttpRequest
        CloseableHttpClient client = HttpClients.createDefault();
        HttpPost httpPost = new HttpPost();
        
        URI uri = URI.create(YOTI_SIGN_BASE_URL + "/embedded-envelopes");
        httpPost.setURI(uri);
        
        // Set the 'Authorization' header
        httpPost.setHeader("Authorization", "Bearer " + YOTI_SIGN_AUTH_TOKEN);

        // Create a Multipart request entity, and add the file to send
        // along with the options
        MultipartEntityBuilder formDataBuilder = MultipartEntityBuilder.create();

        File file = new File("/path/to/your/file.pdf");
        formDataBuilder.addBinaryBody("file", file);

        String jsonPayload = ...; // JSON string containing the options
        formDataBuilder.addTextBody("options", jsonPayload, ContentType.APPLICATION_JSON);
        
        // Add the Multipart request entity to the Http request
        httpPost.setEntity(formDataBuilder.build());        

        try {
            // Perform the POST request and read the created envelope ID
            HttpResponse response = client.execute(httpPost);

            JsonReader reader = Json.createReader(response.getEntity().getContent());
            JsonObject responseObject = reader.readObject();

            String envelopeId = responseObject.getString("envelope_id");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

}
{% /tab %}
{% tab language="php" %}
<?php

use GuzzleHttp\Client;
use GuzzleHttp\Psr7\MultipartStream;
use GuzzleHttp\Psr7\Request;

use function GuzzleHttp\Psr7\stream_for;

$options = [
    'file_name' => 'example-document.pdf',
    'name' => 'Sign your request for..',
    'emails' => [
        'invitation' => [
            'body' => [
                'message' => 'Please sign the example document',
            ],
        ],
    ],
    'recipients' => [
        [
            'name' => 'John Smith',
            'email' => 'example@example.com',
            'role' => 'Signee',
            'auth_type' => 'no-auth',
            'sign_group' => 1,
            'tags' => [
                [
                    'page_number' => 1,
                    'x' => 0.3,
                    'y' => 0.4,
                    'type' => 'signature',
                    'optional' => false,
                    'file_name' => 'example-document.pdf',
                ],
            ],
            'event-notifications' => [],
        ],
    ],
    'custom_webhook_uri' => YOUR_WEBHOOK_URL,
];

$request = new Request(
    'POST',
    API_BASE_URL . '/embedded-envelopes',
    [
        'Authorization' => 'Bearer ' . YOUR_API_KEY,
    ],
    new MultipartStream([
        [
            'name' => 'file',
            'contents' => stream_for(fopen('./example-document.pdf', 'r')),
        ],
        [
            'name' => 'options',
            'contents' => stream_for(json_encode($options)),
        ],
    ])
);

$client = new Client();
$response = $client->send($request);
$json = json_decode($response->getBody());
$envelope_id = $json->envelope_id;
{% /tab %}
{% tab language="csharp" %}
using (var pdfFileContent = new StreamContent(
    new FileStream(
        "test.pdf",
        FileMode.Open,
        FileAccess.Read)))
{
    using (var optionsJsonContent = new StringContent(
        optionsJson,
        Encoding.UTF8))
    {
        MultipartFormDataContent multiPartContent = new MultipartFormDataContent
        {
            { pdfFileContent, "file", "test.pdf" },
            { optionsJsonContent, "options" }
        };

        using (HttpRequestMessage request = new HttpRequestMessage
        {
            Method = HttpMethod.Post,
            RequestUri = new Uri("https://api.yotisign.com/v2/embedded-envelopes"),
            Content = multiPartContent
        })
        {
            request.Headers.Add("Authorization", "Bearer " + yotiAuthenticationToken);

            using (HttpClient httpClient = new HttpClient())
            {
                HttpResponseMessage response = httpClient.SendAsync(request).Result;
            }
        }
    }
}
{% /tab %}
{% tab language="go" %}
options := `{}`

	payload := &bytes.Buffer{}
	writer := multipart.NewWriter(payload)
	_ = writer.WriteField("options", options)
	
	file, err := os.Open("path/to.pdf")
	defer file.Close()
	formFile, err := writer.CreateFormFile("file",filepath.Base("path/to.pdf"))
	_, err = io.Copy(formFile, file)
	err = writer.Close()
	
	req, err := http.NewRequest("POST", "<BASE_URL>/v2/embedded-envelopes", payload)
	req.Header.Add("Authorization", "Bearer <API_KEY>")
	req.Header.Add("Content-Type", "multipart/form-data")
	req.Header.Set("Content-Type", writer.FormDataContentType())
	
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

## Expected response

On success Yoti returns a 200 and a JSON object in the following format:

{% code %}
{% tab language="json" %}
{
  "envelope_id": <uuid>,
  "recipients": [
    {
      "token": <uuid>,
      "email": <string>
    }
  ]
}
{% /tab %}
{% /code %}

This envelope ID will be used to launch the embedded envelope, view the envelope status and retrieve the completed signed document.

To launch an embedded envelope, render it using one of the following URLs.

{% code %}
{% tab language="http" %}
Production:
https://www.yotisign.com/embedded/sign/{your_token}
{% /tab %}
{% /code %}

{% code %}
{% tab language="http" %}
Sandbox:
https://demo.www.yotisign.com/embedded/sign/{your_token}
{% /tab %}
{% /code %}

---

## Error codes

{% table %}
| Error code | Description | 
| ---- | ---- | 
| 400 | Bad Request, example: id provided not a UUID | 
| 401 | Unauthorised request, example: requesting the status on an envelope you are not authorised to view | 
| 403 | Forbidden, requesting user did not create the envelope | 
| 413 | The combined file sizes have exceeded the 20MB limit | 
| 422 | The request body did not pass validation | 
{% /table %}