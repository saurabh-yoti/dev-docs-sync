---
type: page
title: Yoti Age Scan
listed: true
slug: integration-steps-agescan
description: 
index_title: Yoti Age Scan
hidden: 
keywords: 
tags: 
---

Welcome to the developer documentation for integrating with Yoti Age Scan as a stand alone service. 

The below will guide you through the configuration and implementation steps that are necessary in order to use a secure age-checking service that can estimate a person’s age by looking at their face.

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      You will need the Yoti App on your phone and to have registered your business with Yoti.
   </div>
   <div class="alert-links"> 
         <a target="_self" href="https://developers.yoti.com/yoti/getting-started-hub">View Onboarding with Yoti</a>
      <a target="_self" href="https://developers.yoti.com/yoti/generating-the-api-keys">View Generate API keys</a> 
   </div>
</div>
{% /html %}

The integrations steps are as follows, see below or jump straight to the documentation:

[1) Create an age estimation request](https://developers.yoti.com/yoti/integration-steps-agescan#create-an-age-estimation-request)

---

## Yoti Age Scan live demo

We've created a suite of live demos in Yoti World to show you how Yoti can best serve your business with a Yoti Age Scan integration:

[Launch website live demo](https://yoti.world/age-scan/)

[Launch gaming terminal live demo](https://yoti.world/gambling/)

[Launch self-checkout terminal live demo](https://yoti.world/checkout/)

---

## Web Examples

If you wanna just dive in to hacking this together, click below to see the examples. Otherwise continue below with our step by step guide.

- [Javascript (Node.js)](https://github.com/getyoti/age-scan-examples/tree/master/javascript)
- [Java](https://github.com/getyoti/age-scan-examples/tree/master/java)
- [Python](https://github.com/getyoti/age-scan-examples/tree/master/python)
- [PHP](https://github.com/getyoti/age-scan-examples/tree/master/php)
- [Go](https://github.com/getyoti/age-scan-examples/tree/master/go)
- [.NET](https://github.com/getyoti/age-scan-examples/tree/master/dotnet/CoreExample)

---

## Technical Overview

The user's image is securely transmitted to the Yoti API (hosted in the United Kingdom and secured by TLS 1.2 encryption). After the age estimation is performed, the captured facial image is deleted from Yoti’s servers and Yoti returns a predicted age and uncertainty value.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1602180870/29764/hztzzbcgrvzedien5vsg.png" caption="Yoti Age Scan overview" mode="responsive" height="196" width="794" %}
{% /image %}

Optionally you can use Anti spoofing to add a layer of security to the service and ensure the user is using their own face for estimation. This will help prevent malicious users trying to user a fake image to get a higher or lower age estimation than a legitimate attempt would produce.

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
        To read more, please see our white paper.

    </div>
    <div class="alert-links"> 
        <a href="https://www.yoti.com/blog/yoti-age-scan-whitepaper/">Whitepaper</a>
   </div>
{% /html %}

The image requirements to use Age Scan are:

- Yoti only accepts JPEG’s encoded as a base64 image
- Base64 body must be below 100KB (~70KB JPEG)
- The minimum face dimensions we accept is 96 x 96 pixels

There’s a tradeoff between estimation accuracy and camera quality / light conditions, false-negative errors such as face not detected or spoofing attempt detected may be higher than expected due to one or more of the following factors:

{% table %}
| Condition | Description | 
| ---- | ---- | 
| Lighting | Provide UX and guidance to the user. Jump to this section for more information: [https://developers.yoti.com/yoti/user-experience-agescan#guidance](https://developers.yoti.com/yoti/user-experience-agescan#guidance) | 
| Face positioning | Guide the users to place their face is in the middle of the photo you are capturing. A near frontal pose with no obstruction to the facial features. | 
| Camera angle | Please try to get the users photo from face on to get the best result. The camera’s field of view is too small to provide suitable context around the facial image captured. This can negatively impact the ability of the algorithm to compare to other ‘normal’ images in its learned model. Generally ensuring this field of view is sufficient to fit at least 3 times the face size horizontally and 2 times vertically. | 
| Camera type | Yoti Age Scan does not work on infrared cameras. We are seeing acceptable performance on VGA cameras (640x480) with decent lenses in artificial lighting. For best performance we are happy to provide testing when evaluating camera options. | 
| Image cropping | Further image cropping can also reduce the context around the facial image captured. This can negatively impact the ability of the algorithm to compare to other ‘normal’ images in its learned model. Image scaling is the best approach to avoid this. | 
| Resolution | Resolution is not high enough (ideally a minimum of 800x600) to provide adequate image clarity for the age estimation to work. The configuration in place (threshold age and uncertainty of image value) provides a fail-safe to ensure minors are not being passed (false-positives). | 
| Glare / Blur | Insufficient anti-glare capabilities of either the lens or the glass will make it harder for the anti-spoofing to accurately detect edges around faces. This can negatively impact the ability of the algorithm to compare to other ‘normal’ images in its learned model. | 
| Zoom | Optical zoom effects can reduce the context around the facial image captured. This can negatively impact the ability of the algorithm to compare to other ‘normal’ images in its learned model. A distorted lens structure, such as a ‘fish-eye’ lens which is not how the AI model has been trained. | 
| Image compression | Too much image compression is applied to the captured image which creates ‘artifacts’ and inaccuracies in the image (ideally no more than 90% compression). This can negatively impact the ability of the algorithm to compare to other ‘normal’ images in its learned model. | 
|  |  | 
{% /table %}

### Hardware requirements

When using the Yoti API (Using the Yoti Service for image processing) the hardware requirements are as follows:

- CPU - 1GHz CPU x86 or x64
- 1 GB RAM (4GB RAM Recommended)
- Network connectivity

Yoti Age Scan does not work on infrared cameras. We are seeing acceptable performance on VGA cameras (640x480) with decent lenses in artificial lighting. For best performance we are happy to provide testing when evaluating camera options.

Please consult [Yoti](mailto:sdksupport@yoti,com) on these for hosted solution requirements.

---

## Create an age estimation request

After completing the Yoti onboarding, you will need to complete authentication for the API by using the Yoti SDK to simplify the process for requesting to Yoti. The Yoti SDKs are available via popular dependency management systems. Further details can be found on the pages of the specific projects.

{% code %}
{% tab language="javascript" %}
npm install -S -E yoti
{% /tab %}
{% tab language="php" %}
// Get the Yoti PHP SDK library via a Composer package
composer require yoti/yoti-php-sdk
{% /tab %}
{% tab language="python" %}
pip install yoti
{% /tab %}
{% tab language="java" %}
// If you are using Maven, add the following dependency:
<dependency>
    <groupId>com.yoti</groupId>
    <artifactId>yoti-sdk-impl</artifactId>
    <version>2.6.0</version>
</dependency>

// If you are using Gradle, add the following dependency:
compile group: 'com.yoti', name: 'yoti-sdk-impl', version: '2.6.0'
{% /tab %}
{% tab language="go" %}
// As of version 2.4.0, modules are used. This means it's not necessary to get a copy or fetch all dependencies 
// as instructed below, as the Go toolchain will fetch them as necessary. 
// You can simply add a `require github.com/getyoti/yoti-go-sdk/v2` to go.mod.
// To download and install the Yoti SDK and its dependencies, run the following command from your terminal:

go get "github.com/getyoti/yoti-go-sdk/v3"
{% /tab %}
{% tab language="csharp" %}
// To install the Yoti NuGet package you will need to install NuGet.
// To import the latest Yoti SDK into your project, enter the following
// command from NuGet Package Manager Console in Visual Studio:

Install-Package Yoti

// For other installation methods, see https://www.nuget.org/packages/Yoti
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
{% tab language="java" %}
byte[] payload = ...

try {
    SignedRequest signedRequest = SignedRequestBuilder.newInstance()
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

The request payload should be in the following format: This JSON string will be the `data` parameter in the `withPayload` above code snippet. 

{% code %}
{% tab language="json" %}
{
  "data": "/9j/4AAQSkZJRgABAgAAAQABAAD/2wAcHNXCKigjEaYH51Me1Zy1Za0P/Z....",
}
{% /tab %}
{% /code %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
        Yoti provides you assets to create optimal experiences for your customers and increase conversion.

    </div>
    <div class="alert-links"> 
        <a href="https://developers.yoti.com/yoti/user-experience-agescan">User experience</a>
   </div>
{% /html %}

### Example responses

The response received from the API will be below:

The uncertainty value is a confidence score. Yoti recommends rejecting any response with an uncertainty greater than 6.0.  Typically this indicates a problem with image capture. 

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