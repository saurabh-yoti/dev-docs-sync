---
type: page
title: Quick Start
listed: true
slug: quick-start
description: 
index_title: Quick Start
hidden: 
keywords: 
tags: 
---

We suggest you read through the step by step integration guide to understand the integration in detail. Please see below for example code snippets, examples projects and a demo. 

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      You will need to download the Yoti app on your phone and register your business with Yoti.
   </div>
   <div class="alert-links"> 
      <a  target="_self" href="https://developers.yoti.com/yoti/getting-started"> Onboarding with Yoti </a>
      <a  target="_self" href="https://developers.yoti.com/yoti/production-keys"> Generate API Keys </a> 
   </div>
</div>
{% /html %}

Please ensure you have a verified organisation and generate Age estimation keys. 

---

## Example code

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
      We strongly recommend you use the Face capture module. 
    </div>
    <div class="alert-links"> 

   </div>
</div>
{% /html %}

First you need to install the SDK:

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

There are three endpoints which can be used with this API:

{% table %}
| Endpoint | Description | 
| ---- | ---- | 
| [https://api.yoti.com/ai/v1/age](https://api.yoti.com/ai/v1/age) | Use Yoti's age estimation service. | 
| [https://api.yoti.com/ai/v1/age-antispoofing](https://api.yoti.com/ai/v1/age-antispoofing) | Use Yoti's age estimation service and the Anti-spoofing check. | 
| [https://api.yoti.com/ai/v1/antispoofing](https://api.yoti.com/ai/v1/antispoofing) | Use Yoti's anti-spoofing check as a standalone product. | 
{% /table %}

{% code %}
{% tab language="javascript" %}
const PATHS = {
    AGE: '/age',
    LIVENESS: '/antispoofing',
    AGE_LIVENESS: '/age-antispoofing',
};

const data = {
    img: 'base64img',
};

const request = new RequestBuilder()
    .withBaseUrl('https://api.yoti.com/ai/v1')
    .withPemFilePath('<YOTI_KEY_FILE_PATH>')
    .withEndpoint(PATHS.AGE_LIVENESS) // optionally PATHS.AGE or PATHS.LIVENESS
    .withPayload(new Payload(data))
    .withMethod('POST')
    .withHeader('X-Yoti-Auth-Id', '<YOTI_CLIENT_SDK_ID>')
    .build();
{% /tab %}
{% tab language="java" %}
String AGE = "/age";
String LIVENESS = "/antispoofing";
String AGE_LIVENESS = "/age-antispoofing";

JsonObject body = new JsonObject();
body.put("img", imageBytes);
byte[] payload = body.encode().getBytes();

try {
    SignedRequest signedRequest = new SignedRequestBuilder()
        .withKeyPair(<YOTI_KEY_FILE_PATH>)
        .withBaseUrl("https://api.yoti.com/ai/v1")
        .withEndpoint(AGE_LIVENESS) // optionally AGE or LIVENESS
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

$img = [ "img" => "base64Image" ];

$request = (new RequestBuilder())
    ->withBaseUrl('https://api.yoti.com/ai/v1')
    ->withPemFilePath('<YOTI_KEY_FILE_PATH>')
    ->withEndpoint('/age-antispoofing')
    ->withPayload(Payload::fromJsonData($img)) // For version < 3, use ->withPayload(new Payload($img))
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
        url=request.url, img=request.img, headers=request.headers, method=request.method)
    return response.content

def generate_session():

    payload_string = json.dumps(img).encode()

    signed_request = (
        SignedRequest
        .builder()
        .with_pem_file("<YOTI_KEY_FILE_PATH>")
        .with_base_url("https://api.yoti.com/ai/v1")
        .with_endpoint("/age-antispoofing")
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
	img = _base64Face
});

byte[] byteContent = Encoding.UTF8.GetBytes(serializedRequest);

Uri _baseUrl = new UriBuilder("https", "api.yoti.com", 443, "ai/v1").Uri;

Yoti.Auth.Web.Request ageScanRequest = new RequestBuilder()
  .WithStreamReader(privateKeyStream)
  .WithBaseUri(_baseUrl)
  .WithEndpoint("/age-antispoofing")
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
        BaseURL:    "https://api.yoti.com/ai/v1/",
        Endpoint:   "/age-antispoofing",
        Headers: map[string][]string{
            "Content-Type": {"application/img"},
            "Accept":       {"application/img"},
			"X-Yoti-Auth-Id":{"<YOTI_CLIENT_SDK_ID>"},
        },

        Body: func(img []byte, _ error) []byte {
            return img
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
          .with_base_url('https://api.yoti.com/api/v1')
          .with_http_method('POST')
          .with_endpoint('/age-antispoofing')
          .with_payload(img: 'base64Image')
          .with_header('X-Yoti-Auth-Id', Yoti.configuration.client_sdk_id)
          .build
response = request.execute
body = response.body
puts body
{% /tab %}
{% /code %}

### Demos

We've created a suite of live demos in Yoti World to show you how the Anti-spoofing API can best serve your business when integrated:

- [
Liveness demo](https://yoti.world/liveness-demo)

---

## Face capture example

- [Face capture web example](https://github.com/getyoti/web-fcm-demo/)
- [Android example](https://github.com/getyoti/yoti-face-capture-android)
- [iOS example](https://github.com/getyoti/yoti-face-capture-ios)