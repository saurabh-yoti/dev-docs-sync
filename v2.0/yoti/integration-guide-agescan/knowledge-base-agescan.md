---
type: page
title: Knowledge base
listed: true
slug: knowledge-base-agescan
description: 
index_title: Knowledge base
hidden: 
keywords: 
tags: 
---

This is your online library of information about Yoti Age Scan.

---

## Antispoofing - Background Image

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know... 
    </div>
    <div class="alert-text">
       This section is only relevant to retailers with a POS Terminal
    </div>
</div>
{% /html %}

This anti-spoofing method is useful for fixed camera installations (for example at an electronic point-of-sale terminal). It captures the empty background view from the camera, which can then be compared against all subsequent captured images for age estimation requests.  Yoti runs a check to confirm that the original background is still present in each subsequent capture, rejecting images where it does not.  

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1570456610/-1/eybzhrsonmevz3ubvcgu.jpg" caption="Background image technical process" mode="responsive" height="1200" width="1600" %}
{% /image %}

There are 2 steps required to perform background image checks:

1. Submit a background image, this will be used in each age estimation request to ensure the backgrounds match.
2. Submit the photo for age estimation, with the associated background ID.

Both of these steps can be achieved using the SDK, the following assumes you have already installed the SDK as per the steps detailed in the [auto$](/yoti/integration-steps-agescan).

### Get the background image

Please note the `withEndpoint` should be set to `/backgrounds.`

{% code %}
{% tab language="javascript" %}
const { RequestBuilder, Payload } = require('yoti');
const request = new RequestBuilder()
    .withBaseUrl('https://api.yoti.com/api/v1/age-verification')
    .withPemFilePath('<YOTI_KEY_FILE_PATH>')
    .withEndpoint('/backgrounds')
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
$request = (new RequestBuilder())
    ->withBaseUrl('https://api.yoti.com/api/v1/age-verification')
    ->withPemFilePath('<YOTI_KEY_FILE_PATH>')
    ->withEndpoint('/backgrounds')
    ->withPayload(new Payload(data))
    ->withMethod('POST')
    ->withQueryParam('X-Yoti-Auth-Id', '<YOTI_CLIENT_SDK_ID>')
    ->build()
    //get Yoti Response
	->execute();
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
        .with_endpoint("/backgrounds")
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
        .withEndpoint("/backgrounds")
        .withPayload(payload)
        .withHttpMethod("POST")
		.withHeader("X-Yoti-Auth-Id", "<YOTI_CLIENT_SDK_ID>")
        .build();

    YourPojo yourPojo = signedRequest.execute(YourPojo.class);
} catch (GeneralSecurityException | URISyntaxException | IOException | ResourceException ex) {
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

    request, _ := requests.SignedRequest{

        HTTPMethod: http.MethodPost,
        BaseURL:    "https://api.yoti.com/api/v1/age-verification",
        Endpoint:   "/backgrounds",
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
// Click to edit code
{% /tab %}
{% tab language="ruby" %}
# Click to edit code
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

The response will be as follows:

{% code %}
{% tab language="json" %}
{
  "id": "4e08364e-a55a-4794-a93b-8f4d70d432ba"
}
{% /tab %}
{% /code %}

### Get Age Estimation with anti-spoofing

Please note the `withEndpoint` should be set to `/checks`

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
$request = (new RequestBuilder())
    ->withBaseUrl('https://api.yoti.com/api/v1/age-verification')
    ->withPemFilePath('<YOTI_KEY_FILE_PATH>')
    ->withEndpoint('/checks')
    ->withPayload(new Payload(data))
    ->withMethod('POST')
    ->withQueryParam('X-Yoti-Auth-Id', '<YOTI_CLIENT_SDK_ID>')
    ->build()
    //get Yoti Response
	->execute();
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
        .withBaseUrl(https://api.yoti.com/api/v1/age-verification)
        .withEndpoint("/checks")
        .withPayload(payload)
        .withHttpMethod("POST")
		.withHeader("X-Yoti-Auth-Id", "<YOTI_CLIENT_SDK_ID>")
        .build();

    YourPojo yourPojo = signedRequest.execute(YourPojo.class);
} catch (GeneralSecurityException | URISyntaxException | IOException | ResourceException ex) {
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

    request, _ := requests.SignedRequest{

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
// Click to edit code
{% /tab %}
{% tab language="ruby" %}
# Click to edit code
{% /tab %}
{% /code %}

The request payload should be in the following format: This JSON string will be the `data` parameter in the `withPayload` above code snippet. Notice the addition of the `background_id` which would be obtained from step 1. 

{% code %}
{% tab language="json" %}
{
  "data": "/9j/4AAQSkZJRgABAgAAAQABAAD/2wAcHNXCKigjEaYH51Me1Zy1Za0P/Z....",
  "background_id": "4e08364e-a55a-4794-a93b-8f4d70d432ba"
}
{% /tab %}
{% /code %}

The response received from the API will be as follows:

{% code %}
{% tab language="json" %}
{
  "pred_age": 29.7475,
  "uncertainty": 2.04677
}
{% /tab %}
{% /code %}

For more details see the API references [here](https://yoti.com/api-reference/#yoti-age-scan-anti-spoofing).