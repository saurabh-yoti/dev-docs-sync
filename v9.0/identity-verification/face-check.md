---
type: page
title: Face Check
listed: true
slug: face-check
description: 
index_title: Face Check
hidden: 1
keywords: 
tags: 
---

## Overview

Yoti offers the ability to add your own pool of applicants/faces to our API, which can then be searched against by running face check against this pool and the user undergoing the identity verification check. If a match is found, you will be notified about this in the session response.

There are a few steps to use this service:

1. Create the applicants
2. Add a face for each applicant
3. Create an applicant pool
4. Add applicants to the applicant pool
5. Create a Face check when configuring an identity verification session

## Authentication

From here on, each endpoint requires an RSA-signed request for Authentication. This can  be constructed via one of our backend SDKs. The Yoti SDK exposes a simple request builder class to support the authentication process, and the examples provide snippets of this usage in each endpoint code snippet. You will need your Yoti SDK ID and application key pair for this process.

Please use our Yoti SDKs to automatically build the relevant request. The Yoti SDKs are available via popular dependency management systems.

{% code %}
{% tab language="javascript" %}
npm install yoti
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
    <version>3.6.0</version>
</dependency>

// If you are using Gradle, add the following dependency:
compile group: 'com.yoti', name: 'yoti-sdk-impl', version: '3.6.0'
{% /tab %}
{% tab language="go" %}
// As of version 2.4.0, modules are used. This means it's not necessary to get a copy or fetch all dependencies 
// as instructed below, as the Go toolchain will fetch them as necessary. 
// You can simply add a `require github.com/getyoti/yoti-go-sdk/v3` to go.mod.
// To download and install the Yoti SDK and its dependencies, run the following command from your terminal:

go get "github.com/getyoti/yoti-go-sdk/v3"
{% /tab %}
{% /code %}

{% code %}
{% tab language="javascript" %}
const { RequestBuilder, Payload } = require("yoti");

const payload = {}; // JSON payload

const request = new RequestBuilder()
  .withBaseUrl("https://api.yoti.com/idverify/v1")
  .withPemFilePath("<YOTI_KEY_FILE_PATH>") // file path to PEM file
  .withEndpoint("/")
  .withPayload(new Payload(payload))
  .withMethod("POST")
  .withQueryParam("sdkId", "<YOTI_CLIENT_SDK_ID>")
  .build();

// get Yoti response
const response = await request.execute();
{% /tab %}
{% tab language="php" %}
<?php
use Yoti\Http\RequestBuilder;
use Yoti\Http\Payload;

$payload = []; // JSON payload

$request = (new RequestBuilder())
    ->withBaseUrl('https://api.yoti.com/idverify/v1')
    ->withPemFilePath('<YOTI_KEY_FILE_PATH>')
    ->withEndpoint('/')
    ->withPayload(Payload::fromJsonData($payload)) 
    ->withMethod('POST')
    ->withQueryParam('sdkId', '<YOTI_CLIENT_SDK_ID>')
    ->build()
    // get Yoti Response
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

    payload = {} # JSON payload
    payload_string = json.dumps(payload).encode()
    
    signed_request = (
        SignedRequest
        .builder()
        .with_pem_file("<YOTI_KEY_FILE_PATH>")
        .with_base_url("https://api.yoti.com/idverify/v1")
        .with_endpoint("/")
        .with_http_method("POST")
        .with_param("sdkId", "<YOTI_CLIENT_SDK_ID>")
				.with_payload(payload_string)
        .build()
    )

	# get Yoti response
    response = signed_request.execute()
    response_payload = json.loads(response.text)
{% /tab %}
{% tab language="java" %}
byte[] PAYLOAD = ... // JSON payload

try {
    SignedRequest signedRequest = SignedRequestBuilder.newInstance()
        .withKeyPair(<YOTI_KEY_FILE_PATH>)
        .withBaseUrl("https://api.yoti.com/idverify/v1")
        .withEndpoint("/")
        .withPayload(PAYLOAD)
        .withHttpMethod("POST")
        .withQueryParameter("sdkId", "<YOTI_CLIENT_SDK_ID>")
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
data := map[string]interface{}{} // JSON payload

request, _ := requests.SignedRequest{
    HTTPMethod: http.MethodPost,
    BaseURL:    "https://api.yoti.com/idverify/v1",
    Endpoint:   "/",
    Params: map[string]string{
        "sdkId": "<YOTI_CLIENT_SDK_ID>"
    },
    Headers: map[string][]string{
        "Content-Type": {"application/json"},
        "Accept":       {"application/json"}
    },
    Body: func(data []byte, _ error) []byte {
        return data
    }(json.Marshal(jsonobj{ data })),
}.WithPemFile(key).Request()

//  get Yoti response
response, _ := http.DefaultClient.Do(request)
{% /tab %}
{% /code %}