---
type: page
title: Digital ID Match
listed: true
slug: digital-id-match
description: 
index_title: Digital ID Match
hidden: 
keywords: 
tags: 
---

Digital ID Match is a service that allows your business to check whether one of their users (new or existing) has a Yoti account by sending the user’s email address or mobile number to our API. 

Yoti will respond with the result as to whether the user has a Yoti Digital ID app account with a verified ID and if so, will enable the relying party to request that information securely via a Yoti QR share.

Users will receive a push notification on their phone that a search has been carried out. We will also send a POST notification to an endpoint that you specify in your request.

{% callout type="info" title="Important" %}
You must inform the user that you are carrying out this search. Users are able to opt out of the search from within their Digital ID account.
{% /callout %}

## Search

To perform the search you must have an active Yoti service generated through the Hub, see [here](/digital-id/production-keys) for details on how to generate the keys for this.

{% callout type="warning" title="Request Access" %}
To use Digital ID Match, the service needs to be enabled for your organisation by the Yoti team. Please contact your account manager or our [support team](https://support.yoti.com/yotisupport/s/contactsupport) to request access.
{% /callout %}

{% code %}
{% tab language="http" %}
POST https://api.yoti.com/did
{% /tab %}
{% /code %}

### SDK integration

You will need to ensure the latest version of the Yoti backend SDK is installed.

{% code %}
{% tab language="javascript" title="Node.js" %}
// Get the Yoti Node SDK library via the NPM registry
npm install yoti
{% /tab %}
{% tab language="java" %}
// If you are using Maven, add the following dependency:
<dependency>
    <groupId>com.yoti</groupId>
    <artifactId>yoti-sdk-api</artifactId>
    <version>3.11.0</version>
</dependency>

// If you are using Gradle, add the following dependency:
compile group: 'com.yoti', name: 'yoti-sdk-api', version: '3.11.0'
{% /tab %}
{% tab language="php" %}
// Get the Yoti PHP SDK library via a Composer package
composer require yoti/yoti-php-sdk
{% /tab %}
{% tab language="python" %}
# Get the Yoti Python SDK library
pip install yoti
{% /tab %}
{% tab language="csharp" %}
// To install the Yoti NuGet package, you need to install NuGet Package Manager. After that, enter the following command in the console:

Install-Package Yoti

// For other installation methods, see https://www.nuget.org/packages/Yoti
{% /tab %}
{% tab language="go" %}
// Simply add this as an import:
import "github.com/getyoti/yoti-go-sdk/v3"

// Or add the following line to your go.mod file
require github.com/getyoti/yoti-go-sdk/v3 v3.14.0
{% /tab %}
{% /code %}

Once you have added the Yoti SDK to your project, the check can be performed as shown in the code snippet below:

{% code %}
{% tab language="javascript" title="Node.js" %}
const yoti = require("yoti");
const fs = require("fs");

const sdkId = "YOUR_SDK_ID";
const pem = fs.readFileSync("path-to-pem-file");

const body = {JSON_BODY}; //see below

const request = new yoti.RequestBuilder()
  .withBaseUrl("https://api.yoti.com/did")
  .withPemString(pem)
  .withEndpoint("/v1/matches")
  .withPayload(new yoti.Payload(body))
  .withMethod("POST")
  .withHeader("X-Yoti-Auth-Id", sdkId)
  .build();
{% /tab %}
{% tab language="java" %}
byte[] JSON_BODY = ... //see below

try {
		SignedRequest signedRequest = SignedRequestBuilder.newInstance()
        .withKeyPair("<YOTI_KEY_FILE_PATH>")
        .withBaseUrl("https://api.yoti.com/did")
        .withEndpoint("/v1/matches")
        .withPayload(JSON_BODY)
        .withHttpMethod("POST")
        .withHeader("X-Yoti-Auth-Id", "<YOTI_CLIENT_SDK_ID>")
        .build();

  	YourPojo yourPojo = signedRequest.execute(YourPojo.class);

}	catch (GeneralSecurityException | URISyntaxException | IOException | ResourceException ex) {
  	ex.printStackTrace();
}
{% /tab %}
{% tab language="php" %}
<?php
use Yoti\Http\RequestBuilder;
use Yoti\Http\Payload;

$JSON_BODY = [
    ... //see below
];

$request = (new RequestBuilder())
    ->withBaseUrl('https://api.yoti.com/did')
    ->withPemFilePath('<YOTI_KEY_FILE_PATH>')
    ->withEndpoint('/v1/matches')
    ->withPayload(Payload::fromJsonData(JSON_BODY))
    ->withHeader('X-Yoti-Auth-Id', '<YOTI_CLIENT_SDK_ID>')
    ->build()
    //get Yoti Response
    ->execute();

// * For JSON data in Version >3 please use Payload::fromJsonData(JSON_BODY)
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

    payload = {} # see below
    payload_string = json.dumps(payload).encode()
    
    signed_request = (
        SignedRequest
        .builder()
        .with_pem_file("<YOTI_KEY_FILE_PATH>")
        .with_base_url("https://api.yoti.com/did")
        .with_endpoint("/v1/matches")
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
	JSON_BODY // See below
});

byte[] byteContent = Encoding.UTF8.GetBytes(serializedRequest);

Uri _baseUrl = new UriBuilder("https", "api.yoti.com", 443, "did").Uri;

Yoti.Auth.Web.Request DIDMatchRequest = new RequestBuilder()
  .WithStreamReader(privateKeyStream)
  .WithBaseUri(_baseUrl)
  .WithEndpoint("/v1/matches")
  .WithHttpMethod(HttpMethod.Post)
  .WithContent(byteContent)
  .WithHeader("X-Yoti-Auth-Id", "<YOTI_CLIENT_SDK_ID>")
  .WithQueryParam("secure", true")
  .Build();            

// Send Request
HttpResponseMessage response = DIDMatchRequest.Execute(httpClient).Result;
{% /tab %}
{% tab language="go" %}
import (
    "io/ioutil"
    "net/http"
    "github.com/getyoti/yoti-go-sdk/v2/requests"
)

key, _ := ioutil.ReadFile("<YOTI_KEY_FILE_PATH>")
// Create request
request, _ := requests.SignedRequest{
  HTTPMethod: http.MethodPost,
  BaseURL:    "https://api.yoti.com/did",
  Endpoint:   "/v1/matches",
  Headers: map[string][]string{
    "Content-Type": {"application/json"},
    "Accept":       {"application/json"}
    "X-Yoti-Auth-Key": {"<YOTI_CLIENT_SDK_ID>"},
  },
  Body: func(data []byte, _ error) []byte {
    return data
  }(json.Marshal(jsonobj{ data }, // see below
                 })),
}.WithPemFile(key).Request()
//get Yoti response
response, _ := http.DefaultClient.Do(request)
{% /tab %}
{% /code %}

### Request body

{% code %}
{% tab language="json" %}
{
  value: "someone@mail.com", // +447444 444 444 - Must be an email address or phone number
  notification: {
    url: "https:/example.com/notification?example=query-param",
    method: "POST",
    verifyTls: true,
    headers: {
      "ANY-HTTP-HEADER": "the-header-value",
      "ANOTHER-HTTP-HEADER": "another-header-value",
    },
  },
};
{% /tab %}
{% /code %}

{% table widths="" %}
| Key | Description | Example Value | 
| ---- | ---- | ---- | 
| value | This can either be the user's email address or phone number. Phone numbers must include the country code. | [melissa.peterson@yoti.com](mailto:melissa.peterson@yoti.com)  +447444 444 444 | 
| notification | Yoti will send a notification with the results to an endpoint. You can specify any headers needed. |  | 
| url | The URL of your notification endpoint. Include any query parameters here. | [https://yoti.com](https://yoti.com) | 
| method | The API method for the notification. | POST | 
| verifyTls | Confirms that your notification endpoint needs TLS verification. | true | 
| headers | Any HTTP headers for your notification endpoint. |  | 
{% /table %}

### Response

A successful search will return a transaction ID and the result:

{% code %}
{% tab language="json" title="201" %}
{
"id": "a-unique-transaction-id",
"result": "NO_ACCOUNT_FOUND"
}
{% /tab %}
{% tab language="json" title="400" %}
{
"id": "Yzt0sbVOSauDWPwMQvumjQ",
"status": 400,
"error": "INVALID_PAYLOAD",
"message": "An error message from the server"
}
{% /tab %}
{% tab language="json" title="401" %}
{
"id": "Yzt0sbVOSauDWPwMQvumjQ",
"status": 401,
"error": "INVALID_REQUEST_SIGNATURE",
"message": "Invalid request signature"
}
{% /tab %}
{% tab language="json" title="403" %}
{
"id": "Yzt0sbVOSauDWPwMQvumjQ",
"status": 403,
"error": "DISABLED_APP",
"message": "An error message from the server"
}
{% /tab %}
{% tab language="json" title="500" %}
{
"id": "Yzt0sbVOSauDWPwMQvumjQ",
"status": 500,
"error": "INTERNAL_SERVER_ERROR",
"message": "An error message from the server"
}
{% /tab %}
{% /code %}

{% callout type="warning" title="Transaction ID" %}
You should record this ID and securely store it together with the searched email address or phone number. If a user reports on their Digital ID app that the search was not triggered by them, you can cross-reference this information with the webhook notification (detailed below).
{% /callout %}

{% table widths="" %}
| Result | Description | 
| ---- | ---- | 
| NO_ACCOUNT_FOUND | An account could not be found matching the provided email or phone number. | 
| UNVERIFIED_ACCOUNT_FOUND | An account was found linked to the email or phone number, however the account does not have a verified ID added. | 
| VERIFIED_ACCOUNT_FOUND | An account was found linked to the email or phone number, and the account has a verified ID added. | 
{% /table %}

{% table widths="" %}
| Status | Response | 
| ---- | ---- | 
| 201 | Created | 
| 400 | Bad Request | 
| 401 | Unauthorized | 
| 403 | Forbidden | 
| 500 | Server Error | 
{% /table %}

## Notifications

### Push Notification

When performing the search, if the user has a Yoti Digital ID account, they will receive a push notification informing them that the search has taken place. This will also appear in their Activity tab. They will then have the option to confirm whether or not they agree to this.

Example:

{% image url="https://uploads.developerhub.io/prod/kvAX/odrikvlswb3xra83cdblqu6pk4v8n9lvtnt7ftu7enjws1rgbd5ch96sj3aq0p6l.jpg" mode="set" height="553" width="306" %}
{% /image %}

{% image url="https://uploads.developerhub.io/prod/kvAX/rxrkn2dfexmp4py7hw6uk2k5dusvndt35eux6ifk2slb4521tcvh7pdxl459wayx.png" mode="set" height="778" width="306" %}
{% /image %}

The **Company name** will be the external name of your Yoti application used for performing the match. The **Company URL** will be the URL in the application settings. See [here](/digital-id/production-keys) for information on the application set up.

### Webhook Notification

Within the body you must specify an endpoint for a POST notification. This notification is sent to your backend when a user receives the push notification to their app account and actions that it is not them.

{% code %}
{% tab language="json" title="Notification" %}
{
  "specversion": "1.0",
  "id": "Y2el8YXnCTN6d2xa8ENADdKkE21EdNK-_CuSZrkmdHA4UdqsSD2mAXuCwLlZmZDw",
  "type": "com.yoti.connect.event.did.not-me",
  "source": "urn:yoti:connect:did",
  "time": "2025-05-27T12:55:04.199Z"
}
{% /tab %}
{% /code %}

Any webhook notification sent via our Digital ID service will have the same payload as defined by [Cloud Events](https://cloudevents.io/) specification.

{% table widths="" %}
| Value | Details | 
| ---- | ---- | 
| specversion | Version number of the Events Spec | 
| id | The unique transaction ID from the initial response | 
| type | Yoti notification type | 
| source | Yoti service sending the notification | 
| time | The time the user confirmed it wasn't them in UTC. | 
{% /table %}