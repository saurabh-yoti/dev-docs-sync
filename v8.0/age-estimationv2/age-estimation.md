---
type: page
title: Age estimation v2
listed: true
slug: age-estimation
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
         <a target="_self" href="https://developers.yoti.com/anti-spoofing/image-requirements">Image requirements
    </a>
   </div>
</div>
{% /html %}

There is one step to follow to integrate the Age estimation and anti-spoofing API:

1. Create a request

---

## Face Capture

For optimal results, Yoti provides and recommends to use the [Yoti Face Capture](https://www.npmjs.com/package/@getyoti/react-face-capture) modules, which are designed to capture optimal images meeting the requirements of the API. This is available as a Native package, and Web implementation.

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

## Create a request

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

You can create two types of requests using the API:

{% table %}
| Endpoint | Description | 
| ---- | ---- | 
| [https://api.yoti.com/ai/v1/age](https://api.yoti.com/ai/v1/age) | Use Yoti's age estimation service. | 
| [https://api.yoti.com/ai/v1/age-antispoofing](https://api.yoti.com/ai/v1/age-antispoofing) | Use Yoti's age estimation service and the Anti-spoofing check. | 
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
        BaseURL:    "https://api.yoti.com/ai/v1",
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

This endpoint will return an anti-spoofing result alongside an Age Estimation.

This JSON string must be sent in the `img` parameter in `withPayload`.

{% code %}
{% tab language="json" %}
{
    "img": "/9j/4AAQSkZJRgABAgAAAQABAAD/2wAcHNXCKigjEaYH51Me1Zy1Za0P/Z...."
}
{% /tab %}
{% /code %}

{% code %}
{% tab language="json" %}
{
   "antispoofing": {
       "prediction": "real|fake|undetermined"
   },
   "age": {
       "st_dev": float,
       "age": float
   }
}
{% /tab %}
{% /code %}

If integrating into a non-browser client, we recommend contacting [clientsupport@yoti.com](mailto:clientsupport@yoti.com) for additional support.

### Terminal integrations

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

### Example response

The response received from the API will be below:

{% code %}
{% tab language="json" %}
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

{% table widths="225" %}
| Response | Explained | 
| ---- | ---- | 
| Prediction - real | Yoti has detected a real user. | 
| Prediction - fake | Yoti has detected a spoof attempt. | 
| Prediction - undetermined | Yoti is unable to determine if the user is real or not. | 
| Age - age | The age estimation of the user. | 
| Age - st_dev | The st_dev value is a confidence score. Yoti recommends rejecting any response with an uncertainty greater than 6.0. Typically this indicates a problem with image capture. This should **only** be treated as a quality score. | 
{% /table %}

## Error codes

{% table %}
| Error code | Error | Description | 
| ---- | ---- | ---- | 
| 404 | APP_NOT_FOUND | Application app_id not found. | 
| 401 | INVALID_X_YOTI_AUTH_ID | - X-Yoti-Auth-Id__header not provided.\n- auth id is not a valid uuid. | 
| 400 | INVALID_APP_ID | Application id cannot be empty. | 
| 400 | INVALID_PUBLIC_KEY | Application public key cannot be empty. | 
| 403 | DISABLED_APP_STATE | Application must be enabled. | 
| 400 | INVALID_ORG_ID | Organisation id cannot be empty. | 
| 400 | INVALID_BILLING_SOURCE_ID | Application billing source id cannot be empty. | 
| 404 | ORG_NOT_FOUND | Organisation org_id not found. | 
| 401 | INVALID_YOTI_AUTH_DIGEST | - X-Yoti-Auth-Digest header is missing.\n- X-Yoti-Auth-Digest is not base64 encoded. | 
| 401 | INVALID_NONCE | - Nonce is missing. nonce parameter is mandatory\n- Provided nonce is not a valid uuid. | 
| 401 | INVALID_TIMESTAMP | - Timestamp is missing. timestamp parameter is mandatory.\n- Provided timestamp is not a valid unix timestamp. | 
| 401 | INVALID_PUBLIC_KEY_ENCODING | Failed to load public key. key is not der encoded. | 
| 401 | UNSUPPORTED_ALGORITHM | Serialised key is of a type that is not supported by the backend. | 
| 401 | INVALID_SIGNATURE | Failed to verify signature. | 
| 403 | INVALID_ORG_STATUS | Organisation has an invalid status. | 
| 404 | INVALID_METADATA_DEVICE | Invalid device metadata provided. | 
| 400 | INVALID_BODY_ENCODING | Request body should be a valid JSON. | 
| 404 | INVALID_ENDPOINT | The endpoint request is invalid. | 
| 413 | PAYLOAD_TOO_LARGE | Payload too large. | 
| 400 | IMAGE_NOT_PROVIDED | Image has not been provided. | 
| 400 | INVALID_B64_IMAGE | - Base64 image is incorrectly padded.\n- Cannot create image from base64 decoded bytes | 
| 400 | UNSUPPORTED_IMAGE_FORMAT | Image format not supported. Please use JPEGs (95 to 100 quality) and PNGs. | 
| 400 | IMAGE_SIZE_TOO_BIG | Image size too big, the maximum size is 2MB. | 
| 400 | IMAGE_SIZE_TOO_SMALL | Image size too small, the minimum size is 50KB. | 
| 400 | MIN_HEIGHT | The image height is incorrect. Image minimum height required is 300 pixels. | 
| 400 | MAX_HEIGHT | The image height is incorrect. Image maximum height required is 2000 pixels. | 
| 400 | MIN_WIDTH | The image width is incorrect. Image minimum width required is 300 pixels. | 
| 400 | MAX_WIDTH | The image width is incorrect. Image maximum width required is 2000 pixels. | 
| 400 | MIN_PIXELS | To process the image the minimum number of pixels required is 90,000 pixels. | 
| 400 | MAX_PIXELS | To process the image the maximum number of pixels required is 2,100,000 pixels. | 
| 400 | IMAGE_WRONG_CHANNELS | Missing colour channel, the input image must be RGB or RGBA. | 
| 400 | IMAGE_GRAYSCALE_NOT_SUPPORTED | Grayscale images not supported. | 
| 503 | SERVICE_UNAVAILABLE | The service is temporarily unavailable. | 
| 400 | FACE_NOT_FOUND | Face not found. | 
| 400 | MULTIPLE_FACES | Multiple faces in the image provided. | 
| 400 | FACE_BOX_TOO_SMALL | The face in the image provided is too small. | 
| 400 | FACE_TO_IMAGE_RATIO_TOO_LOW | Face ratio is lower than the minimum ratio. | 
| 400 | FACE_TO_IMAGE_RATIO_TOO_HIGH | Face ratio is bigger than the maximum ratio. | 
| 400 | INSUFFICIENT_AREA_AROUND_THE_FACE | Insufficient area around the face in the image provided. | 
| 400 | IMAGE_TOO_BRIGHT | Image too bright.. | 
| 400 | IMAGE_TOO_DARK | Image too dark. | 
| 500 | FAIL_PREDICTION | - Age distribution is empty.\n- Standard deviation is empty.\n- Cannot build model result.\n- Antispoofing prediction failed. | 
| 500 | UNSPECIFIED_ERROR | An internal server error occurred. | 
{% /table %}