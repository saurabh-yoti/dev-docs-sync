---
type: page
title: Integration steps Dev
listed: true
slug: integration-steps-agescan
description: 
index_title: Integration steps Dev
hidden: 
keywords: 
tags: 
---

Below are the end points and integration configuration you need to integrate.

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

## Get Age Estimation

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

go get "github.com/getyoti/yoti-go-sdk/v2"
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
    .withBaseUrl('<YOTI_BASE_URL>/api/v1/age-verification')
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
    ->withBaseUrl('<YOTI_BASE_URL>/api/v1/age-verification')
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
        .with_base_url("<YOTI_BASE_URL>/api/v1/age-verification")
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
        .withBaseUrl("<YOTI_BASE_URL>/api/v1/age-verification")
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
    request, _ := requests.SignedRequest{
        HTTPMethod: http.MethodPost,
        BaseURL:    "<YOTI_BASE_URL>/api/v1/age-verification",
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
// COMING SOON
{% /tab %}
{% tab language="ruby" %}
// Coming Soon
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

### Example responses

The response received from the API will be below:

{% code %}
{% tab language="json" %}
{
  "pred_age": 29.7475,
  "uncertainty": 2.04677
}
{% /tab %}
{% /code %}