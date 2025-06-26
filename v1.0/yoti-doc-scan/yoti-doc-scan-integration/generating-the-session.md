---
type: page
title: Generating the session
listed: true
slug: generating-the-session
description: 
index_title: Generating the session
hidden: 
keywords: 
tags: 
---

You will need to create a session with Yoti to perform the ID checks by using the following endpoint. A session represents one end-to-end use of the ID verification service. Each time the ID verification service is initiated (regardless of which specific tasks/checks are required) a unique session identifier is assigned. You will need the SDK ID from your Yoti Hub.

**Base URL**: Please contact Yoti for the base URL: [sdksupport@yoti.com](mailto:sdksupport@yoti.com)

Request authentication will be required. You can use the Yoti SDKs to automatically build the relevant request. Examples and instructions of this can be found [below](/yoti-doc-scan/generating-the-session#authentication-and-headers). 

Yoti will ask you to set all of the following:

1. [Session and data retention configuration](/yoti-doc-scan/generating-the-session#1-session-and-data-retention-configuration)
2. [Requested checks configuration](/yoti-doc-scan/generating-the-session#2-requested-checks-configuration) - Which verification steps are required for the user.
3. [Tasks](/yoti-doc-scan/generating-the-session#3-tasks) - What tasks should be performed. Example: `ID_DOCUMENT_TEXT_DATA_EXTRACTION` returns the set of fields representing the information on the document in a structured and normalised format.
4. [Client SDK configuration](/yoti-doc-scan/generating-the-session#4-sdk-config) allowing:

- Camera and country options
- Indicate where the user should be directed after the user journey (success/error redirect url).
- Select the language to be displayed (this will override the locale detected on the device).

Below is a full example payload and further explanations of the components in more detail.

## Example of full payload request

{% code %}
{% tab language="json" %}
{
  "client_session_token_ttl": 600,
  "resources_ttl": 604800,
  "user_tracking_id": "<uuid>",
  "notifications": {
    "endpoint": "https://yourdomain.com/idverify/updates",
    "topics": [
      "resource_update",
      "task_completion",
      "check_completion",
      "session_completion"
    ],
    "auth_token": "XXX"
  },
  "requested_checks": [
    {
      "type": "ID_DOCUMENT_AUTHENTICITY",
      "config": {}
    },
    {
      "type": "LIVENESS",
      "config": {
        "liveness_type": "ZOOM", // Required
        "max_retries": 3 // Required, must be greater than 1
      }
    },
    {
      "type": "ID_DOCUMENT_FACE_MATCH",
      "config": {
        "manual_check": "FALLBACK" // | "NEVER" | "ALWAYS"
      }
    }
  ],
  "requested_tasks": [
    {
      "type": "ID_DOCUMENT_TEXT_DATA_EXTRACTION",
      "config": {
        "manual_check": "FALLBACK"
      }
    }
  ],
  "sdk_config": {
    "allowed_capture_methods": "CAMERA_AND_UPLOAD"
    "primary_colour": "#2d9fff",
    "preset_issuing_country": "USA",
    "success_url": "https://yourdomain.com/success",
    "error_url": "https://yourdomain.com/error"
  }
}
{% /tab %}
{% /code %}

## Payload Component Breakdown

### 1. Session and data retention configuration

Below explains the parameters for the session and data retention configuration.

{% table %}
| Parameters | Description | Metrics | Mandatory | 
| ---- | ---- | ---- | ---- | 
| client_session&lt;i&gt;_&lt;/i&gt;token_ttl | This is how long the full Yoti Doc Scan session is open for. This must be longer than 5 minutes.&nbsp; | Seconds | No | 
| resources_ttl | Retention period for uploaded documents/images in number of seconds. Default is one week (60*60* 24*7=604800). This can be a minimum of 24 hours from the client session token ttl. | Seconds | No | 
| user_tracking_id" : "&lt;uuid&gt; | Allows to track the same user across multiple sessions. Note: Should not contain any personal identifiable information | UUID | No | 
| notifications{} | &lt;p&gt;If provided Yoti Docs posts (POST endpoint required) an update notification every time the session state changes, based on the selected subscription topics "endpoint" : "https://yourdomain.com/idverify/updates". &lt;/p&gt;&lt;p&gt;Notifications on: resource update, task completion, check completion, session completion. &lt;/p&gt;&lt;p&gt;If not provided, only session completion notifications are sent.&lt;/p&gt; | N/A | No | 
| auth_token | Allows an integrator to define an authorisation token, if they have secured API endpoints, allowing Yoti to call endpoints.&nbsp; | N/A | No | 
{% /table %}

{% code %}
{% tab language="json" %}
"client_session_token_ttl": 600,
  "resources_ttl": 604800,
  "user_tracking_id": "<uuid>",
  "notifications": {
    "endpoint": "https://yourdomain.com/idverify/updates",
    "topics": [
      "resource_update",
      "task_completion",
      "check_completion",
      "session_completion"
    ],
    "auth_token": "XXX"
  },
{% /tab %}
{% /code %}

### 2. Requested checks configuration

Yoti can complete the following check, if requested:

1) **DOCUMENT_AUTHENTICITY_ID**

A requested check to assess the characteristics of a document, to determine the credibility of the ID document.

This requires image media attached to the resource (images of the front and back of the document -the back of the document is not always required).

On successful completion, the check outputs a report in the form of a structured JSON object, which can be found in the ‘checks retrieval’ section of the session retrieval [here](/yoti-doc-scan/session-retrieval#checks-retrieval). Updates are sent to the updates URL (if subscribed to notifications). Please see the [document fields](/yoti-doc-scan/session-retrieval#document-fields-retrieval) section for more information.

{% code %}
{% tab language="json" %}
"requested_checks": [
    {
      "type": "ID_DOCUMENT_AUTHENTICITY",
      "config": {}
    },
  ],
{% /tab %}
{% /code %}

2) **LIVENESS**

A requested check to assess whether the document scan is being performed by a real person and not someone wearing a mask or an automated system.

You must provide the max number of retries your users can have before the liveness is failed. This must be greater than 1. An "attempt" is a completed liveness check that is either rejected or approved. If the user does not complete the liveness check this does not count as an attempt and the user will be prompted to try again.

This will produce a liveness_capture resource in the session as well as a report in the form of a structured JSON object for each attempted liveness check. More details can be found [here](/yoti-doc-scan/session-retrieval#liveness) and [here](/yoti-doc-scan/session-retrieval#resources-retrieval).

{% code %}
{% tab language="json" %}
"requested_checks": [
    {
      "type": "LIVENESS",
      "config": {
        "liveness_type": "ZOOM", // Required
        "max_retries": 3 // Required, must be greater than 1
      }
    }
  ],
{% /tab %}
{% /code %}

3) **ID_DOCUMENT_FACE_MATCH**

A request to assess whether the user's face matches the face on the ID document. You need to perform a liveness check to perform this face match check. 

This is performed as an automated check, however you can configure whether the check is passed on to our security centre for a manual check. This can be set to always, fallback or never.

On successful completion, the check outputs a report in the form of a structured JSON object, which can be found in the ‘checks retrieval’ section of the session retrieval [here](/yoti-doc-scan/session-retrieval#checks-retrieval). 

{% table %}
| Manual check | Explanation | 
| ---- | ---- | 
| ALWAYS | The requested check will always go to the security centre regardless of the success of the machine check | 
| NEVER | The requested check will never go to the security centre&lt;br&gt; | 
| FALLBACK | The requested check will only go the security centre if the machine check fails | 
{% /table %}

{% code %}
{% tab language="json" %}
"requested_checks": [
    {
      "type": "ID_DOCUMENT_FACE_MATCH",
      "config": {
        "manual_check": "FALLBACK" // | "NEVER" | "ALWAYS"
      }
    }
  ],
{% /tab %}
{% /code %}

### 3. Tasks

Yoti can complete the following tasks, if requested:

1) **ID_DOCUMENT_TEXT_DATA_EXTRACTION**

There are two methods of extracting structured data from documents:

- Machine data extraction, using a suitable extraction method for that document type.
- Manual review and data entry

Machine data extraction will always be used in place of human data entry, if possible for that document type. Generally there are two main reasons machine data extraction is not successful:

1) The images used as an input are not of a high enough quality.

2) There are no available machine extraction methods for the document type submitted. For more information on the documents where machine data extraction is available, ​please contact us.​

If machine data extraction is not successful, there is an option (selected at session creation) to fallback to manual data extraction. This generates a ‘text data check’ automatically, and the document is reviewed by one of our document processing experts. 

{% table %}
| Parameter setting for&nbsp;ID_DOCUMENT_TEXT_DATA_EXTRACTION | Description | 
| ---- | ---- | 
| FALLBACK | This will initiate manual data extraction after attempted to do automatically. (OCR). We strongly recommend this option. | 
| NEVER | If the ID fails on automatic extraction, Yoti will not attempt manual extraction. | 
| ALWAYS | Always go for manual data extraction and automatic.&nbsp; | 
{% /table %}

{% code %}
{% tab language="json" %}
"requested_tasks": [
    {
      "type": "ID_DOCUMENT_TEXT_DATA_EXTRACTION",
      "config": {
        "manual_check": "FALLBACK"
      }
    }
  ],
{% /tab %}
{% /code %}

---

### 4. SDK Config

The method sdk_config is explained below:

{% table %}
| Type | Parameters (examples) | Description | 
| ---- | ---- | ---- | 
| allowed_capture_methods | CAMERA_AND_UPLOAD, CAMERA&nbsp; | If the user uses a camera to take a photo of their ID document, or take a photo and option to upload the document. | 
| primary_colour | #2d9fff | Colour of the button provided in the frontend client. | 
| preset_issuing_country | USA | Country you intend on presenting in the front end client as a default | 
| success_url | https://yourdomain.com/success | If the upload/photo is successfully captured redirect your users here. | 
| error_url | https:/yourdomain.com/error | If the upload/photo&nbsp;is unsuccessfully captured redirect your users here. | 
{% /table %}

{% code %}
{% tab language="json" %}
"sdk_config": {
    "allowed_capture_methods": "CAMERA_AND_UPLOAD"
    "primary_colour": "#2d9fff",
    "preset_issuing_country": "USA",
    "success_url": "https://yourdomain.com/success",
    "error_url": "https://yourdomain.com/error"
  }
{% /tab %}
{% /code %}

## Authentication and Headers

You can use the Yoti SDK to simplify the authentication process for requests to Yoti. The Yoti SDKs are available via popular dependency management systems. Further details can be found on the pages of the specific projects. 

If you wish to build these yourself, instructions and further details on authentication and headers [here](/yoti-doc-scan/authentication-and-headers).

**Endpoint**

{% code %}
{% tab language="http" %}
POST <YOTI_BASE_URL>/sessions/{session_id}?sdkId={sdkId}&nonce={nonce}&timestamp={timestamp}`
{% /tab %}
{% /code %}

{% code %}
{% tab language="javascript" %}
npm install -S -E yoti
{% /tab %}
{% tab language="ruby" %}
gem install yoti

# The gem provides a configuration generator for Ruby on Rails:

rails generate yoti:install
{% /tab %}
{% tab language="php" %}
// Get the Yoti PHP SDK library via a Composer package
composer require yoti/yoti-php-sdk

// Or the following Composer dependency:
"require": {
    "yoti/yoti-php-sdk" : "2.4"
}
{% /tab %}
{% tab language="python" %}
pip install yoti
{% /tab %}
{% tab language="java" %}
// If you are using Maven, add the following dependency:
<dependency>
    <groupId>com.yoti</groupId>
    <artifactId>yoti-sdk-impl</artifactId>
    <version>2.0.0</version>
</dependency>

// If you are using Gradle, add the following dependency:

compile group: 'com.yoti', name: 'yoti-sdk-impl', version: '2.0.0'
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
{% /code %}

Once you have added the Yoti SDK dependency to your project, you can use it to authenticate your session generation request. See the code snippets below for examples.

{% code %}
{% tab language="javascript" %}
const { RequestBuilder, Payload } = require('yoti');

const request = new RequestBuilder()
    .withBaseUrl('YOTI_BASE_URL')
    .withPemFilePath('YOTI_KEY_FILE_PATH')
    .withEndpoint('/sessions')
    .withPayload(new Payload(SESSION_OBJ))
    .withMethod('POST')
    .withQueryParam('sdkId', 'YOTI_CLIENT_SDK_ID')
    .build();

//get Yoti response
const response = request.execute();
{% /tab %}
{% tab language="ruby" %}
# COMING SOON
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\Http\RequestBuilder;
use Yoti\Http\Payload;

$request = (new RequestBuilder())
    ->withBaseUrl('YOTI_BASE_URL')
    ->withPemFilePath('YOTI_KEY_FILE_PATH')
    ->withEndpoint('/sessions')
    ->withPayload(new Payload(SESSION_OBJ))
    ->withMethod('POST')
    ->withQueryParam('sdkId', 'YOTI_CLIENT_SDK_ID')
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

    payload_string = json.dumps(SESSION_OBJ).encode()

    signed_request = (
        SignedRequest
        .builder()
        .with_pem_file("YOTI_KEY_FILE_PATH")
        .with_base_url("YOTI_BASE_URL")
        .with_endpoint("/sessions")
        .with_http_method("POST")
        .with_param("sdkId", "YOTI_CLIENT_SDK_ID")
        .with_payload(payload_string)
        .build()
    )

    response = signed_request.execute()
    response_payload = json.loads(response.text)

//get Yoti response
print(generate_session())
{% /tab %}
{% tab language="java" %}
// COMING SOON
{% /tab %}
{% tab language="go" %}
import (
    "io/ioutil"
    "net/http"
    "github.com/getyoti/yoti-go-sdk/v2/requests"
)

    sdkID := "YOTI_CLIENT_SDK_ID";
    key, _ := ioutil.ReadFile("YOTI_KEY_FILE_PATH")
    // Create session
    sessionRequest, _ := requests.SignedRequest{
        HTTPMethod: http.MethodPost,
        BaseURL:    YOTI_API_BASEURL,
        Endpoint:   "/sessions",
        Params: map[string]string{
            "sdkId": sdkID,
        },
        Headers: map[string][]string{
            "Content-Type": {"application/json"},
            "Accept":       {"application/json"},
        },
        Body: func(data []byte, _ error) []byte {
            return data
        }(json.Marshal(jsonobj{ SESSION_OBJ
            },
        })),
    }.WithPemFile(key).Request()

	//get Yoti response
	sessionResponse, _ := http.DefaultClient.Do(sessionRequest)
{% /tab %}
{% tab language="csharp" %}
// COMING SOON
{% /tab %}
{% /code %}

## Example payload response

{% code %}
{% tab language="json" %}
{
  "client_session_token_ttl" : 599,
  "client_session_token" : "<uuid>",
  "session_id" : "<uuid>"
}
{% /tab %}
{% /code %}

## Other response codes

{% table %}
| Code | Description | 
| ---- | ---- | 
| 201 | Session created | 
| 400 | Bad request&lt;br&gt; | 
| 401 | Unauthorised request (wrong key or signature) | 
{% /table %}