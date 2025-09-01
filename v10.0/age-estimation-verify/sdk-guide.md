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

## Face Capture

For optimal face capture, Yoti provides the [auto$](/age-estimation-verify/face-capture-module-fcm) which is designed to capture optimal images meeting the requirements of the API. This is available as a Native .Net package.

{% callout type="info" title="Native face capture" %}
Capture your images by using our [auto$](/age-estimation-verify/face-capture-module-fcm).
{% /callout %}

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

{% code %}
{% tab language="javascript" %}
const PATHS = {
    AGE: "/age-verify",
    AGE_LIVENESS: "/age-antispoofing-verify",
};

const data = {
    img: "base64img",
    threshold: 25,
    operator: "OVER",
    metadata: {        
        "device": "mobile"
    }
};

const request = new RequestBuilder()
    .withBaseUrl('https://api.yoti.com/ai/v1')
    .withPemFilePath('<YOTI_KEY_FILE_PATH>')
    .withEndpoint(PATHS.AGE_LIVENESS)
    .withPayload(new Payload(data))
    .withMethod('POST')
    .withHeader('X-Yoti-Auth-Id', '<YOTI_CLIENT_SDK_ID>')
    .build();

const response = request.execute();
{% /tab %}
{% tab language="java" %}
String AGE = "/age-verify";
String AGE_LIVENESS = "/age-antispoofing-verify";

JsonObject metadata = new JsonObject();
metadata.put("device", "mobile");

JsonObject body = new JsonObject();
body.put("img", imageBytes);
body.put("threshold", 25);
body.put("operator", "OVER");
body.put("metadata", metadata);

byte[] payload = body.encode().getBytes();

try {
    SignedRequest signedRequest = new SignedRequestBuilder()
        .withKeyPair(<YOTI_KEY_FILE_PATH>)
        .withBaseUrl("https://api.yoti.com/ai/v1")
        .withEndpoint(AGE_LIVENESS)
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

define("AGE_", "/age-verify");
define("AGE_LIVENESS", "/age-antispoofing-verify");

$data = (object)[
  "img" => "base64Image",
  "threshold" => 25,
  "operator" => "OVER",
  "metadata" => (object)[
    "device" => "mobile",
  ]
];

$request = (new RequestBuilder())
    ->withBaseUrl('https://api.yoti.com/ai/v1')
    ->withPemFilePath('<YOTI_KEY_FILE_PATH>')
    ->withEndpoint(AGE_LIVENESS)
    ->withPayload(Payload::fromJsonData($data)) // For version < 3, use ->withPayload(new Payload($data))
    ->withMethod('POST')
    ->withHeader('X-Yoti-Auth-Id', '<YOTI_CLIENT_SDK_ID>')
    ->build();

// Execute request
$response = $request->execute();

// Get response body
$body = $response->getBody();
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

string serializedData = Newtonsoft.Json.JsonConvert.SerializeObject(new
{
	img = "base64Image",
	threshold = 25,
	operator = "OVER",
  metadata = {        
    device: "mobile"
  }
});

byte[] byteContent = Encoding.UTF8.GetBytes(serializedData);

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
    "github.com/getyoti/yoti-go-sdk/v3/requests"
)

  data := []byte(`{
    "img": "base64img",
    "threshold": 25,
    "operator": "OVER",
    "metadata": {
      "device": "mobile",
    }
  }`)

  key, _ := ioutil.ReadFile("<YOTI_KEY_FILE_PATH>")

  // Create session
  request,_ := requests.SignedRequest{
    HTTPMethod: http.MethodPost,
    BaseURL:    "https://api.yoti.com/ai/v1",
    Endpoint:   "/age-antispoofing",
    Headers: map[string][]string{
      "Content-Type": {"application/json"},
      "Accept":       {"application/json"},
      "X-Yoti-Auth-Id":{"<YOTI_CLIENT_SDK_ID>"},
    },
    Body: data,
  }.WithPemFile(key).Request()

	//get Yoti response
	response, _ := http.DefaultClient.Do(request)
{% /tab %}
{% tab language="ruby" %}
require 'json'
require 'yoti'

Yoti.configure do |config|
  config.client_sdk_id = '<YOTI_CLIENT_SDK_ID>'
  config.key_file_path = '<YOTI_KEY_FILE_PATH>'
end

data = '{
  "img":"base64Image",
  "threshold":25,
  "operator":"OVER",
  "metadata":{
    "device":"mobile",
   }
}'

request = Yoti::Request
          .builder
          .with_base_url('https://api.yoti.com/ai/v1')
          .with_http_method('POST')
          .with_endpoint('/age-antispoofing')
          .with_payload(data)
          .with_header('X-Yoti-Auth-Id', Yoti.configuration.client_sdk_id)
          .build
response = request.execute
body = response.body
puts body
{% /tab %}
{% /code %}

### Retrieve Results

The endpoint will return the Anti-spoofing result alongside Age threshold check.

{% code %}
{% tab language="json" %}
{
    "age": {
        "age_check": "pass"
    },
    "antispoofing": {
        "prediction": "real"
    }
}
{% /tab %}
{% /code %}