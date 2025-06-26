---
type: page
title: Age estimation v2
listed: true
slug: integration-guide
description: 
index_title: Age estimation v2
hidden: 
keywords: 
tags: 
---

Once you've set up your organisation account on the [Yoti Hub](https://hub.yoti.com/logout), you’re ready to start integrating with the Age estimation and anti-spoofing API.

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
Please have a read of our image requirements.   </div>
   <div class="alert-links"> 
         <a target="_self" href="https://developers.yoti.com/age-estimation/image-requirements">Image requirements
    </a>
   </div>
</div>
{% /html %}

---

## Face Capture

For optimal results, Yoti provides and recommends to use the [Yoti Face Capture modules,](https://www.npmjs.com/package/@getyoti/react-face-capture) which are designed to capture optimal images meeting the requirements of the API. This is available as a Native package, and Web implementation.

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Strongly recommend
    </div>
    <div class="alert-text">
      Get better results by using our Face capture module. 
    </div>
    <div class="alert-links"> 

   </div>
</div>
{% /html %}

---

## Integration

### Install the SDK

After completing the Yoti onboarding, you will need to complete authentication for the API by using the Yoti SDK to simplify the process. The Yoti SDKs are available via popular dependency management systems.

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

### Create a request

You can create three types of requests using the API:

{% table widths="360" %}
| Endpoint | Description | 
| ---- | ---- | 
| [https://api.yoti.com/ai/v1/age](https://api.yoti.com/ai/v1/age) | Use Yoti's Age estimation service. | 
| [https://api.yoti.com/ai/v1/antispoofing](https://api.yoti.com/ai/v1/antispoofing) | Use Yoti's Anti-spoofing check. | 
| [https://api.yoti.com/ai/v1/age-antispoofing](https://api.yoti.com/ai/v1/age-antispoofing) | Use Yoti's Age estimation service and the Anti-spoofing check. | 
{% /table %}

Once you have added the Yoti SDK dependency to your project, you can use it to build and send your request. See the code snippets below for examples.

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

const response = request.execute();
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

def generate_session():

    data = {"img": "base64encodedstring"}
    payload_string = json.dumps(data).encode()

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
        BaseURL:    "https://api.yoti.com/ai/v1",
        Endpoint:   "/age-antispoofing",
        Headers: map[string][]string{
            "Content-Type": {"application/json"},
            "Accept":       {"application/json"},
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
          .with_base_url('https://api.yoti.com/ai/v1')
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

The JSON string for the payload must be in the following format. This is sent with the `withPayload` method provided in the SDK.

{% code %}
{% tab language="json" %}
{
    "img": "/9j/4AAQSkZJRgABAgAAAQABAAD/2wAcHNXCKigjEaYH51Me1Zy1Za0P/Z....",
    "metadata"(Optional): {
          "device": "mobile" or "laptop" // Either value
    }
}
{% /tab %}
{% /code %}

`img` is the mandatory parameter that contains the captured image in Base64 Encoded format.

`metadata` is an optional parameter but is strongly recommended for better results. It is used to specify what type of device is being used. You can choose between mobile or laptop.

### Retrieve the results

The endpoint will return the Anti-spoofing result alongside Age estimation.

{% code %}
{% tab language="json" title="" %}
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

If requesting age only, the response will look as follows:

{% code %}
{% tab language="json" %}
{
    "age": float,
    "st_dev": float
}
{% /tab %}
{% /code %}

If integrating into a non-browser client, we recommend contacting [clientsupport@yoti.com](mailto:clientsupport@yoti.com) for additional support.

### Relaxed image requirements

When using the Age only endpoint, it is possible to lower the threshold for face detection and image validation on images. A reason for this might be that images are not being captured live through Yoti's Face Capture module, or you may want to age estimate images where there is no case to perform a liveness check.

This feature is utilised by setting the image validation level to low, as shown in the example payload. 

Note that this may only be used with the age endpoint.

See [this page](/age-estimation/image-requirements) for more details on the image requirements.

{% code %}
{% tab language="json" %}
{
    "img": "/9j/4AAQSkZJRgABAgAAAQABAAD/2wAcHNXCKigjEaYH51Me1Zy1Za0P/Z....",
    "img_validation_level": "low"
}
{% /tab %}
{% /code %}

## Terminal integrations

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
      This is not live yet but will be going live soon. Please contact us if this interests you. 
    </div>
    <div class="alert-links"> 

   </div>
</div>
{% /html %}

Optionally, additional headers may be provided to the request to allow Yoti to track error responses coming from a particular machine. This would typically be used in a non-browser client scenario, such as an ePOS terminal where each individual machine must be registered by the business.

In order to do this, the following headers should be applied:

{% table widths="187" %}
| Header | Description | 
| ---- | ---- | 
| Terminal-Id | Unique ID per machine. Mandatory for non-browser integrations. | 
| Session-Id | May be provided to demonstrate multiple attempts are from a single user transaction. | 
{% /table %}

## Example responses

The response received from the API will be below, depending on the endpoint used.

{% code %}
{% tab language="json" title="/age-antispoofing" %}
{
    "antispoofing": {
        "prediction": "real"
    },
    "age": {
        "age": 25.1,
        "st_dev": 3.5
    }
}
{% /tab %}
{% /code %}

{% code %}
{% tab language="json" title="/age" %}
{
    "age": 43.2, 
    "st_dev": 4.4
}
{% /tab %}
{% /code %}

{% code %}
{% tab language="json" title="/antispoofing" %}
{
    "prediction": "real"
}
{% /tab %}
{% /code %}

{% table widths="225" %}
| Response | Explained | 
| ---- | ---- | 
| Prediction - real | Yoti has detected a real user. | 
| Prediction - fake | Yoti has detected a spoof attempt. | 
| Age - age | The age estimation of the user. | 
| Age - st_dev | The st_dev value is a confidence score. Yoti recommends rejecting any response with an uncertainty greater than 6.0. Typically this indicates a problem with image capture. This should **only** be treated as a quality score. | 
{% /table %}

{% synced id="ae-error-codes" %}
{% /synced %}