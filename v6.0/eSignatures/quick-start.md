---
type: page
title: Quick start
listed: true
slug: quick-start
description: 
index_title: Quick start
hidden: 
keywords: 
tags: 
---

We suggest you read through the step by step integration guide to understand the integration in detail. Please see below for example code snippets and a postman example.

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      Request your API keys, please let us know if you want to use sandbox or production. 
   </div>
   <div class="alert-links"> 
         <a href="https://www.yotisign.com/app/contact-us/">Get API keys</a>
   </div>
</div>
{% /html %}

---

## Postman example

To run the example in postman please click the below button:

{% html %}
<div class="postman-run-button"
data-postman-action="collection/import"
data-postman-var-1="8a8ca92079c7f6248900"></div>
<script type="text/javascript">
  (function (p,o,s,t,m,a,n) {
    !p[s] && (p[s] = function () { (p[t] || (p[t] = [])).push(arguments); });
    !o.getElementById(s+t) && o.getElementsByTagName("head")[0].appendChild((
      (n = o.createElement("script")),
      (n.id = s+t), (n.async = 1), (n.src = m), n
    ));
  }(window, document, "_pm", "PostmanRunObject", "https://run.pstmn.io/button.js"));
</script>
{% /html %}

---

## Example code

Below is an example of the full request for creating an envelope.

{% badge type="info" text="Hint" /%}We suggest you read through the full documentation first.

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
            "email": "user1@test.com",
            "role": "CEO",
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
							]
						},
						{
            "name": "User 2",
            "email": "user2@test.com",
            "role": "CPO",
            "auth_type": "sign-auth",
            "yoti_attributes": ["full_name"],
            "sign_group": 2,
            "tags": [
                {
                    "page_number": 1,
                    "x": 0.6,
                    "y": 0.3,
                    "type": "signature",
                    "optional": false,
                    "file_name": "myfile.pdf"

                	}
            	]
        		}
    ],
    "notifications": {
        "destination": "https://mysite.example/events",
        "subscriptions": [
            "envelope_completion"
        ]
    }
}
{% /tab %}
{% /code %}

{% code %}
{% tab language="javascript" %}
const rp = require("request-promise");
const fs = require("fs");

const options = {}; //options object

const createEnvelope = () => {
  const request = {
    method: "POST",
    uri: `<BASE_URL>/v2/envelopes`,
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
        
        URI uri = URI.create(YOTI_SIGN_BASE_URL + "/envelopes");
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
        ],
    ],
    'custom_webhook_uri' => YOUR_WEBHOOK_URL,
];

$request = new Request(
    'POST',
    API_BASE_URL . '/envelopes',
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
            RequestUri = new Uri("https://api.yotisign.com/v2/envelopes"),
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
	
	req, err := http.NewRequest("POST", "<BASE_URL>/v2/envelopes", payload)
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

## Web Examples

If you wanna just dive in to hacking this together, click below to see the examples. Otherwise continue with our step by step guide:

- [Javascript](https://github.com/getyoti/yoti-sign-examples/tree/master/api-demos/javascript)
- [.NET](https://github.com/getyoti/yoti-sign-examples/tree/master/api-demos/dotnet)
- [Go](https://github.com/getyoti/yoti-sign-examples/tree/master/api-demos/go)
- [Java](https://github.com/getyoti/yoti-sign-examples/tree/master/api-demos/java)
- [PHP](https://github.com/getyoti/yoti-sign-examples/tree/master/api-demos/php)