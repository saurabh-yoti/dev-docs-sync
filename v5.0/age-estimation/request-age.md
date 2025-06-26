---
type: page
title: Integration guide
listed: true
slug: request-age
description: 
index_title: Integration guide
hidden: 
keywords: 
tags: 
---

Once you've set up your organisation account on the [Yoti Hub](https://hub.yoti.com/logout), you’re ready to start integrating.

{% badge type="warning" text="Help" /%} Please contact us for any advice on integrating this product: [clientsupport@yoti.com](mailto:clientsupport@yoti.com).

There is one step to follow to integrate the Age estimation service:

1. Create a request

---

## Create a request

{% badge type="info" text="NOTE" /%} This service is with a lower quality image. Please read the [](/age-verification/overview) for more details.

After completing the Yoti onboarding, you will need to complete authentication for the API by using the Yoti SDK to simplify the process for requesting to Yoti. The Yoti SDKs are available via popular dependency management systems. Further details can be found on the pages of the specific projects.

{% code %}
{% tab language="javascript" %}
npm install -S -E yoti
{% /tab %}
{% tab language="java" %}
// If you are using Maven, add the following dependency:
<dependency>
    <groupId>com.yoti</groupId>
    <artifactId>yoti-sdk-api</artifactId>
    <version>3.0.0</version>
</dependency>

// If you are using Gradle, add the following dependency:
compile group: 'com.yoti', name: 'yoti-sdk-api', version: '3.0.0'
{% /tab %}
{% tab language="php" %}
// Get the Yoti PHP SDK library via a Composer package
composer require yoti/yoti-php-sdk
{% /tab %}
{% tab language="python" %}
pip install yoti
{% /tab %}
{% tab language="csharp" %}
// To install the Yoti NuGet package you will need to install NuGet.
// To import the latest Yoti SDK into your project, enter the following
// command from NuGet Package Manager Console in Visual Studio:

Install-Package Yoti

// For other installation methods, see https://www.nuget.org/packages/Yoti
{% /tab %}
{% tab language="go" %}
// As of version 2.4.0, modules are used. This means it's not necessary to get a copy or fetch all dependencies 
// as instructed below, as the Go toolchain will fetch them as necessary. 
// You can simply add a `require github.com/getyoti/yoti-go-sdk/v2` to go.mod.
// To download and install the Yoti SDK and its dependencies, run the following command from your terminal:

go get "github.com/getyoti/yoti-go-sdk/v3"
{% /tab %}
{% tab language="ruby" %}
gem install yoti

# The gem provides a configuration generator for Ruby on Rails:

rails generate yoti:install
{% /tab %}
{% /code %}

Once you have added the Yoti SDK dependency to your project, you can use it to build and send your request. See the code snippets below for examples.

{% table widths="345" %}
| Endpoint | Description | 
| ---- | ---- | 
| [https://api.yoti.com/api/v1/age-verification](https://api.yoti.com/api/v1/age-verification) | Use Age estimation only. | 
{% /table %}

{% code %}
{% tab language="javascript" %}
const { RequestBuilder, Payload } = require('yoti');
const request = new RequestBuilder()
    .withBaseUrl('https://api.yoti.com/api/v1/age-verification')
    .withPemFilePath('<YOTI_KEY_FILE_PATH>')
    .withEndpoint('/checks')
    .withPayload(new Payload(data))
    .withMethod('POST')
    .withHeader('X-Yoti-Auth-Id', '<YOTI_CLIENT_SDK_ID>')
    .build();
//get Yoti response
const response = request.execute();
{% /tab %}
{% tab language="java" %}
JsonObject body = new JsonObject();
body.put("data", imageBytes);
byte[] payload = body.encode().getBytes();

try {
    SignedRequest signedRequest = new SignedRequestBuilder()
        .withKeyPair(<YOTI_KEY_FILE_PATH>)
        .withBaseUrl("https://api.yoti.com/api/v1/age-verification")
        .withEndpoint("/checks")
        .withPayload(payload)
        .withHttpMethod("POST")
.withHeader("X-Yoti-Auth-Id", "<YOTI_CLIENT_SDK_ID>")
        .build();

    YourPojo yourPojo = signedRequest.execute(YourPojo.class);
}  catch (GeneralSecurityException | URISyntaxException | IOException | ResourceException ex) {
    ex.printStackTrace();
}
{% /tab %}
{% tab language="php" %}
<?php
use Yoti\Http\RequestBuilder;
use Yoti\Http\Payload;

$data = [ "data" => "base64Image" ];

$request = (new RequestBuilder())
    ->withBaseUrl('https://api.yoti.com/api/v1/age-verification')
    ->withPemFilePath('<YOTI_KEY_FILE_PATH>')
    ->withEndpoint('/checks')
    ->withPayload(Payload::fromJsonData($data)) // For version < 3, use ->withPayload(new Payload(data))
    ->withMethod('POST')
    ->withHeader('X-Yoti-Auth-Id', '<YOTI_CLIENT_SDK_ID>')
    ->build();

// Execute request
$response = $request->execute();

// Get response body
$body = $response->getBody();
{% /tab %}
{% tab language="python" %}
from yoti_python_sdk.http import SignedRequest, RequestHandler
import json
import requests

def execute(request):
    response = requests.request(
        url=request.url, data=request.data, headers=request.headers, method=request.method)
    return response.content

def generate_session():

    payload_string = json.dumps(data).encode()

    signed_request = (
        SignedRequest
        .builder()
        .with_pem_file("<YOTI_KEY_FILE_PATH>")
        .with_base_url("https://api.yoti.com/api/v1/age-verification")
        .with_endpoint("/checks")
        .with_http_method("POST")
        .with_header("X-Yoti-Auth-Id", "<YOTI_CLIENT_SDK_ID>")
        .with_payload(payload_string)
        .build()

    )

	# get Yoti response
    response = signed_request.execute()
    response_payload = json.loads(response.text)
{% /tab %}
{% tab language="csharp" %}
using System;
using System.IO;
using System.Net.Http;
using System.Text;
using Microsoft.AspNetCore.Mvc;
using Yoti.Auth.Web;

HttpClient httpClient = new HttpClient();
StreamReader privateKeyStream = System.IO.File.OpenText(_pemFilePath);

string serializedRequest = Newtonsoft.Json.JsonConvert.SerializeObject(new
{
	data = _base64Face
});

byte[] byteContent = Encoding.UTF8.GetBytes(serializedRequest);

Uri _baseUrl = new UriBuilder("https", "api.yoti.com", 443, "/api/v1/age-verification").Uri;

Yoti.Auth.Web.Request ageScanRequest = new RequestBuilder()
  .WithStreamReader(privateKeyStream)
  .WithBaseUri(_baseUrl)
  .WithEndpoint("/checks")
  .WithHttpMethod(HttpMethod.Post)
  .WithContent(byteContent)
  .WithHeader("X-Yoti-Auth-Id", _clientSdkId)
  .Build();

HttpResponseMessage response = ageScanRequest.Execute(httpClient).Result;
{% /tab %}
{% tab language="go" %}
import (
    "io/ioutil"
    "net/http"
    "github.com/getyoti/yoti-go-sdk/v2/requests"
)

    key, _ := ioutil.ReadFile("<YOTI_KEY_FILE_PATH>")
    // Create session
    request,_ := requests.SignedRequest{
        HTTPMethod: http.MethodPost,
        BaseURL:    "https://api.yoti.com/api/v1/age-verification",
        Endpoint:   "/checks",
        Headers: map[string][]string{
            "Content-Type": {"application/json"},
            "Accept":       {"application/json"},
			"X-Yoti-Auth-Id":{"<YOTI_CLIENT_SDK_ID>"},
        },

        Body: func(data []byte, _ error) []byte {
            return data
        }(json.Marshal(jsonobj{ data },
        })),
    }.WithPemFile(key).Request()

	//get Yoti response
	response, _ := http.DefaultClient.Do(request)
{% /tab %}
{% tab language="ruby" %}
require 'yoti'
Yoti.configure do |config|
  config.client_sdk_id = '<YOTI_CLIENT_SDK_ID>'
  config.key_file_path = '<YOTI_KEY_FILE_PATH>'
end
request = Yoti::Request
          .builder
          .with_base_url('https://api.yoti.com/api/v1/age-verification')
          .with_http_method('POST')
          .with_endpoint('checks')
          .with_payload(data: 'base64Image')
          .with_header('X-Yoti-Auth-Id', Yoti.configuration.client_sdk_id)
          .build
response = request.execute
body = response.body
puts body
{% /tab %}
{% /code %}

This JSON string will be the `data` parameter in the `withPayload` above code snippet.

{% code %}
{% tab language="json" %}
{
  "data": "/9j/4AAQSkZJRgABAgAAAQABAAD/2wAcHNXCKigjEaYH51Me1Zy1Za0P/Z....",
}
{% /tab %}
{% /code %}

## Example responses

The response received from the API will be below:

The uncertainty value is a confidence score. Yoti recommends rejecting any response with an uncertainty greater than 6.0. Typically this indicates a problem with image capture.

{% code %}
{% tab language="json" %}
{
  "pred_age": 29.7475,
  "uncertainty": 2.04677
}
{% /tab %}
{% /code %}

## Error codes

{% table %}
| Error code | Description | 
| ---- | ---- | 
| 1 | Image too big | 
| 2 | Unable to decode image (not a jpeg or wrong base64 string) | 
| 4 | No face detected | 
| 6 | Image not present | 
| 7 | Generic bad request | 
| 8 | No image detected | 
| 9 | Internal server error | 
{% /table %}