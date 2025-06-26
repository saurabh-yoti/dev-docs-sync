---
type: page
title: SDK guide
listed: true
slug: sdk-guide
description: 
index_title: SDK guide
hidden: 
keywords: 
tags: 
---

Once you've set up a verified organisation account on the [Yoti Hub](https://hub.yoti.com/), you’re ready to start integrating with the Age estimation and Anti-spoofing API.

{% badge type="success" text="Note:" /%} After you successfully onboard your organisation and generate the SDK ID for **'Age estimation'** application, please [contact us](https://yoti.force.com/yotisupport/s/contactsupport) to have it whitelisted. This is necessary for use with our dedicated endpoint for this integration.

## Face Capture

For optimal face capture, Yoti provides the [auto$](/ai-services-terminals/face-capture-module-fcm) which is designed to capture optimal images meeting the requirements of the API. This is available as a Native .Net package.

{% callout type="info" title="Native face capture" %}
Capture your images by using our [auto$](/ai-services-terminals/face-capture-module-fcm).
{% /callout %}

{% badge type="warning" text="Info:" /%} We also provide React & JavaScript [Face capture module](https://www.npmjs.com/package/@getyoti/react-face-capture) for Web-based clients.

---

## Integration

### Install the SDK

To simply the integration process, Yoti provides SDKs to integrate with our API. These are available via popular dependency management systems.

{% code %}
{% tab language="javascript" %}
npm install -S -E yoti
{% /tab %}
{% tab language="java" %}
// If you are using Maven, add the following dependency:
<dependency>
    <groupId>com.yoti</groupId>
    <artifactId>yoti-sdk-api</artifactId>
    <version>3.5.1</version>
</dependency>

// If you are using Gradle, add the following dependency:
compile group: 'com.yoti', name: 'yoti-sdk-api', version: '3.5.1'
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

### Create a request

Once you have added the Yoti SDK dependency to your project, you can use it to build and send your request. See the code snippets below for examples.

{% code %}
{% tab language="javascript" %}
const PATHS = {
    AGE_LIVENESS: '/age-antispoofing',
};

const data = {
    img: 'base64img',
};

const request = new RequestBuilder()
    .withBaseUrl('https://api.yoti.com/ai/v1/self-checkout')
    .withPemFilePath('<YOTI_KEY_FILE_PATH>')
    .withEndpoint(PATHS.AGE_LIVENESS)
    .withPayload(new Payload(data))
    .withMethod('POST')
    .withHeader('X-Yoti-Auth-Id', '<YOTI_CLIENT_SDK_ID>')
    .withHeader('Terminal-Id', '<TERMINAL_ID>')
    .withHeader('Session-Id', '<SESSION_ID>') // Optional
    .build();

const response = request.execute();
{% /tab %}
{% tab language="java" %}
String AGE_LIVENESS = "/age-antispoofing";

JsonObject body = new JsonObject();
body.put("img", imageBytes);
byte[] payload = body.encode().getBytes();

try {
    SignedRequest signedRequest = new SignedRequestBuilder()
        .withKeyPair(<YOTI_KEY_FILE_PATH>)
        .withBaseUrl("https://api.yoti.com/ai/v1/self-checkout")
        .withEndpoint(AGE_LIVENESS)
        .withPayload(payload)
        .withHttpMethod("POST")
				.withHeader("X-Yoti-Auth-Id", "<YOTI_CLIENT_SDK_ID>")
				.withHeader('Terminal-Id', '<TERMINAL_ID>')
    		.withHeader('Session-Id', '<SESSION_ID>') // Optional
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

define("AGE_LIVENESS", "/age-antispoofing");

$img = [ "img" => "base64Image" ];

$request = (new RequestBuilder())
    ->withBaseUrl('https://api.yoti.com/ai/v1/self-checkout')
    ->withPemFilePath('<YOTI_KEY_FILE_PATH>')
    ->withEndpoint(AGE_LIVENESS)
    ->withPayload(Payload::fromJsonData($img)) // For version < 3, use ->withPayload(new Payload($img))
    ->withMethod('POST')
    ->withHeader('X-Yoti-Auth-Id', '<YOTI_CLIENT_SDK_ID>')
  	->withHeader('Terminal-Id', '<TERMINAL_ID>')
    ->withHeader('Session-Id', '<SESSION_ID>') // Optional
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
        url=request.url, img=request.img, headers=request.headers, method=request.method)
    return response.content

def generate_session():

    payload_string = json.dumps(img).encode()

    signed_request = (
        SignedRequest
        .builder()
        .with_pem_file("<YOTI_KEY_FILE_PATH>")
        .with_base_url("https://api.yoti.com/ai/v1/self-checkout")
        .with_endpoint("/age-antispoofing")
        .with_http_method("POST")
        .with_header("X-Yoti-Auth-Id", "<YOTI_CLIENT_SDK_ID>")
      	.with_header("Terminal-Id", "<TERMINAL_ID>")
    		.with_header("Session-Id", "<SESSION_ID>") // Optional
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
	img = _base64Face
});

byte[] byteContent = Encoding.UTF8.GetBytes(serializedRequest);

Uri _baseUrl = new UriBuilder("https", "api.yoti.com", 443, "ai/v1/self-checkout").Uri;

Yoti.Auth.Web.Request ageScanRequest = new RequestBuilder()
  .WithStreamReader(privateKeyStream)
  .WithBaseUri(_baseUrl)
  .WithEndpoint("/age-antispoofing")
  .WithHttpMethod(HttpMethod.Post)
  .WithContent(byteContent)
  .WithHeader("X-Yoti-Auth-Id", _clientSdkId)
  .withHeader("Terminal-Id", "<TERMINAL_ID>")
  .withHeader("Session-Id", "<SESSION_ID>") // Optional
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

// Create request
request,_ := requests.SignedRequest{
    HTTPMethod: http.MethodPost,
    BaseURL:    "https://api.yoti.com/ai/v1/self-checkout",
    Endpoint:   "/age-antispoofing",
    Headers: map[string][]string{
        "Content-Type": {"application/img"},
        "Accept":       {"application/img"},
        "X-Yoti-Auth-Id": {"<YOTI_CLIENT_SDK_ID>"},
        "Terminal-Id": {"<TERMINAL_ID>"},
        "Session-Id": {"<SESSION_ID>"}, // Optional
    },

    Body: func(img []byte, _ error) []byte {
        return img
    }(json.Marshal(jsonobj{ data })),
}.WithPemFile(key).Request()

// Get Yoti response
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
          .with_base_url('https://api.yoti.com/ai/v1/self-checkout')
          .with_http_method('POST')
          .with_endpoint('/age-antispoofing')
          .with_payload(img: 'base64Image')
          .with_header('X-Yoti-Auth-Id', Yoti.configuration.client_sdk_id)
          .with_header('Terminal-Id', '<TERMINAL_ID>')
          .with_header('Session-Id', '<SESSION_ID>') // Optional
          .build
response = request.execute
body = response.body
puts body
{% /tab %}
{% /code %}

### Retrieve Results

The endpoint will return the Anti-spoofing result alongside Age estimation.

{% code %}
{% tab language="json" %}
{
   "antispoofing": {
       "prediction": "real | fake"
   },
   "age": {
       "st_dev": float,
       "age": float
   }
}
{% /tab %}
{% /code %}