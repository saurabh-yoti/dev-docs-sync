---
type: page
title: Create a Session Dev
listed: true
slug: generating-a-session
description: 
index_title: Create a Session Dev
hidden: 
keywords: 
tags: 
---

Every time an end user elects to supply an ID document on the relying party app/website/custom product, you will need to create a  [session](/yoti/terminology) with Yoti to perform the ID checks.

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      You will need the Yoti App on your phone and to have registered your business with Yoti and request the Base URL.
   </div>
   <div class="alert-links"> 
      <a  target="_self" href="https://developers.yoti.com/yoti/getting-started-hub"> Onboarding with Yoti </a>
      <a  target="_self" href="https://developers.yoti.com/yoti/generating-the-api-keys"> View Generate API Keys </a> 
<a  target="_self" href="mailto:sdksupport@yoti.com"> Contact us for Base URL</a> 
   </div>
</div>
{% /html %}

---

## Generate the request using our SDK

Please use our Yoti SDKs to automatically build the relevant request. 

The Yoti SDKs are available via popular dependency management systems.

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

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      Please contact us for the Base URL.
   </div>
   <div class="alert-links"> 
<a  target="_self" href="mailto:sdksupport@yoti.com"> Contact us for Base URL</a> 
   </div>
</div>
{% /html %}

{% code %}
{% tab language="javascript" %}
const { RequestBuilder } = require("yoti");

const request = new RequestBuilder()
  .withBaseUrl("<YOTI_BASE_URL>/idverify/v1")
  .withPemFilePath("<YOTI_KEY_FILE_PATH>")
  .withEndpoint("/supported-docuemnts")
  .withMethod("GET")
  .withQueryParam("sdkId", "<YOTI_CLIENT_SDK_ID>")
  .build();

//get Yoti response
const response = request.execute();
{% /tab %}
{% tab language="php" %}
<?php
use Yoti\Http\RequestBuilder;
$request = (new RequestBuilder())
    ->withBaseUrl('<YOTI_BASE_URL>/idverify/v1')
    ->withPemFilePath('<YOTI_KEY_FILE_PATH>')
    ->withEndpoint('/supported-docuemnts')
    ->withMethod('GET')
    ->withQueryParam('sdkId', '<YOTI_CLIENT_SDK_ID>')
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
   
    signed_request = (
        SignedRequest
        .builder()
        .with_pem_file("<YOTI_KEY_FILE_PATH>")
        .with_base_url("<YOTI_BASE_URL>/idverify/v1")
        .with_endpoint("/sessions")
        .with_http_method("GET")
        .with_param("sdkId", "<YOTI_CLIENT_SDK_ID>")
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
        .withBaseUrl("<YOTI_BASE_URL>/idverify/v1")
        .withEndpoint("/supported-documents")
        .withHttpMethod("GET")
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
    // GET supported documents
    request, _ := requests.SignedRequest{
        HTTPMethod: http.MethodGet,
        BaseURL:    "<YOTI_BASE_URL>/idverify/v1",
        Endpoint:   "/supported-documents",
        Params: map[string]string{
          "sdkId": "<YOTI_CLIENT_SDK_ID>"
        },
        Headers: map[string][]string{
            "Content-Type": {"application/json"},
            "Accept":       {"application/json"}
        },
    }.WithPemFile(key).Request()
	//get Yoti response
	response, _ := http.DefaultClient.Do(request)
{% /tab %}
{% tab language="csharp" %}
// COMING SOON
{% /tab %}
{% tab language="ruby" %}
# COMING SOON
{% /tab %}
{% /code %}

---

## Creating the session example

Below is the full payload example of the request for creating the session. 

You will need to specify the following:

[1) System preferences](https://developers.yoti.com/yoti/generating-a-session#1-system-preferences)

- Yoti Doc scan session length
- User tracking
- Status at certain points in the flow

[2) Required Documents ](https://developers.yoti.com/yoti/generating-a-session#2-required-documents)

- Allows you to request multiple documents
- Apply filters to specify which documents you accept

[3) Checks](https://developers.yoti.com/yoti/generating-a-session#2-checks-configuration)

- ID Document Authenticity
- Liveness
- ID Document Face Match

[4) Tasks](https://developers.yoti.com/yoti/generating-a-session#4-tasks-configuration)

- Document data extraction (OCR technology)

[5) Client preferences](https://developers.yoti.com/yoti/generating-a-session#5-client-preferences)

- Camera and pre set country options and where the user should be directed after the user journey (success/error redirect URL).

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
        The request payload should be in the following format (full details of request parameters are provided in the 'explained' section, below).
This JSON string will be the SESSION_OBJ parameter in the withPayload above code snippet.
    </div>
</div>
{% /html %}

{% code %}
{% tab language="json" %}
{
  "client_session_token_ttl": 600,
  "resources_ttl": 604800,
  "user_tracking_id": "<YOUR_USER_ID>",
  "notifications": {
    "endpoint": "https://yourdomain.com/idverify/updates",
    "topics": [
      "resource_update",
      "task_completion",
      "check_completion",
      "session_completion"
    ],
    "auth_token": "username:password"
  },
  "requested_checks": [
	{
 		"type": "ID_DOCUMENT_AUTHENTICITY",
		"config": {
		}
	},
	{
		"type": "LIVENESS",
		"config": {
			"liveness_type": "ZOOM",
			"max_retries": 3
		}
	},
	{
		"type": "ID_DOCUMENT_FACE_MATCH",
		"config": {
			"manual_check": "FALLBACK"
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
    "allowed_capture_methods": "CAMERA_AND_UPLOAD",
    "primary_colour": "#2d9fff",
    "preset_issuing_country": "USA",
    "success_url": "https://yourdomain.com/success",
    "error_url": "https://yourdomain.com/error"
  }
}
{% /tab %}
{% /code %}

### Example response

If the request is successful and a session is generated the API will send a response in the form:

{% code %}
{% tab language="json" %}
{
  "client_session_token_ttl": 599,
  "client_session_token": "<uuid>",
  "session_id": "<uuid>"
}
{% /tab %}
{% /code %}

{% table %}
| Response | Description | 
| ---- | ---- | 
| client_session_token_ttl | Time in milliseconds until the client session expires | 
| client_session_token | Used to authenticate the session | 
| session_id | ID of the session | 
{% /table %}

---

## Creating Sessions explained

### 1. System preferences

The table below explains the optional parameters for the session and data retention configuration.

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
  }
{% /tab %}
{% /code %}

{% table %}
| Parameters | Description | 
| ---- | ---- | 
| client_session_token_ttl | This is how long the full Yoti Doc Scan session is open for in seconds. This must be longer than 5 minutes. | 
| resources_ttl | Retention period for uploaded documents/images in number of seconds. Default is one week (60_60_24*7=604800). This can be a minimum of 24 hours. Starts once the client_session_token_ttl is completed. | 
| user_tracking_id | Allows the relying business backend to track the same user across multiple sessions. Note: Should not contain any personal identifiable information. | 
| notifications { } | If provided, Yoti Doc Scan posts (POST endpoint required) an update notification every time the session state changes, based on the selected subscription topics "endpoint" : "[https://yourdomain.com/idverify/updates"](https://yourdomain.com/idverify/updates&quot;). \n\n\n\nIf there is no 'topics' array then only session completion notifications are sent. | 
| auth_token | Allows the relying business backend to define an authorisation token, if they have secured API endpoints, allowing Yoti to call endpoints. | 
{% /table %}

{% html %}
<div class="alert-know">
    <div class="alert-title" id="know">
        Knowledge base
    </div>
    <div class="alert-text">
        For more information on notifications please head to our Knowledge Base.
    </div>
    <div class="alert-links"> 
       <a href="https://developers.yoti.com/yoti/knowledge-base-docscan#notifications">Notifications</a>
    </div>
</div>
{% /html %}

---

### 2. Required Documents

You can configure your session to allow users to upload multiple documents. You can also add filters to these documents to configure which countries and document types your users can scan.

{% code %}
{% tab language="json" %}
"required_documents": [ // Optional
    {
      "type": "ID_DOCUMENT", // Required
      "filter": { // Optional
        "type": "ORTHOGONAL_RESTRICTIONS", // Required
        "country_restriction": { // Optional
          "inclusion": "WHITELIST", // Required
          "country_codes": ["GBR"] // Required
        },
        "type_restriction": { // Optional
          "inclusion": "BLACKLIST", // Required
          "document_types": ["NATIONAL_ID"] // Required
        }
      }
    },
    {
      "type": "ID_DOCUMENT",
      "filter": {
        "type": "DOCUMENT_RESTRICTIONS", // Required
        "inclusion": "BLACKLIST", // Required
        "documents": [ // Required
          {
            "country_codes": ["DEU","FRA"] // Optional
          },
          {
            "document_types": ["NATIONAL_ID","PASSPORT"] // Optional
          },
          {
            "country_codes": ["GBR"], // Optional
            "document_types": ["DRIVING_LICENSE"] // Optional
          }
        ]
      }
    }
  ],
{% /tab %}
{% /code %}

We provide 2 different types of filters which perform in different ways:

- ORTHOGONAL_RESTRICTION - Allows the user to WHITELIST or BLACKLIST by _country_ and _document type_ independently.
- DOCUMENT_RESTRICTION - Allows the _Relying Business_ to provide multiple restrictions that filter by _country_ and _document type_ together.  Multiple restrictions are combined and the _Union_ of all restrictions is used as either a WHITELIST or a BLACKLIST.

**ORTHOGONAL_RESTRICTION**

This allows the user to WHITELIST or BLACKLIST by _country_ and _document type_ independently. It is intended as the simplest, easiest to use filter. If there is a WHITELIST for one property and a BLACKLIST for the other, then the BLACKLIST will overrule the WHITELIST.

{% code %}
{% tab language="json" %}
"filter": {
  "type": "ORTHOGONAL_RESTRICTIONS",
  "country_restriction": { // Optional
    "inclusion": "WHITELIST", // Required
    "country_codes": ["GBR", "FRA", "DEU"] // Required list
  },
  "type_restriction": { // Optional
    "inclusion": "BLACKLIST", // Required
    "document_types": ["NATIONAL_ID"] // Required list
  }
}
{% /tab %}
{% /code %}

Below is a collection of grids to help visualise how this filter works.

{% image url="https://image-archive.developerhub.io/image/upload/20557/fetittmsvdlftkisoo42/1578585966.jpg" mode="full" height="223" width="1583" %}
{% /image %}

**DOCUMENT_RESTRICTION**

Allows you to provide multiple restrictions that filter by _country_ and _document type_ together.  Multiple restrictions are combined and the union of all restrictions is used as either a WHITELIST or a BLACKLIST.

This filter allows greater precision but is more verbose to use.

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
        If you are requesting multiple documents from your users you must make sure that you avoid creating sessions where the same document would be used to satisfy multiple filters
    </div>
</div>
{% /html %}

{% code %}
{% tab language="json" %}
"filter": {
  "type": "DOCUMENT_RESTRICTIONS",
  "inclusion": "BLACKLIST", // Required
  "documents": [ // Required
    {
      "country_codes": ["GBR","FRA"] // Optional
    },
    {
      "document_types": ["NATIONAL_ID","PASSPORT"] // Optional
    },
    {
      "country_codes": ["USA"], // Optional
      "document_types": ["DRIVING_LICENSE"] // Optional
    }
  ]
}
{% /tab %}
{% /code %}

You can see a few grids below demonstrating this filter.

{% image url="https://image-archive.developerhub.io/image/upload/20557/jhcyy0jsh05e2dous1u5/1578589030.jpg" mode="responsive" height="228" width="1478" %}
{% /image %}

### 3. Checks Configuration

**1) ID Document authenticity**

A request to assess the characteristics of a document, to determine the validity of the ID document.

{% code %}
{% tab language="json" %}
"requested_checks": [
    {
      "type": "ID_DOCUMENT_AUTHENTICITY",
      "config": {}
    },
  ]
{% /tab %}
{% /code %}

This requires there to be image media attached to the resource (images of the front and back of the document - the back of the document is not always required).

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
       Jump to.. 
    </div>
    <div class="alert-text">
       On successful completion, the check outputs a report in the form of a structured JSON object, which can be found in 
       the ‘retrieve results’ section. Updates are sent to the updates URL (if subscribed to notifications).
    </div>
    <div class="alert-links"> 
        <a href="https://developers.yoti.com/yoti/session-and-media-retrieval">Retrieve results and data</a>
        <a target="_self" href="https://developers.yoti.com/yoti/session-and-media-retrieval#id-document-authenticity">ID Document authenticity results</a> 
   </div>
</div>
{% /html %}

**2) Liveness**

A requested check to assess whether the document scan is being performed by a real person and not someone wearing a mask or an automated system.

{% code %}
{% tab language="json" %}
"requested_checks": [
    {
      "type": "LIVENESS",
      "config": {
        "liveness_type": "ZOOM", // Required
        "max_retries": 3 // Required, must be greater than 0
      }
    }
  ]
{% /tab %}
{% /code %}

You must provide the max number of retries your users can have before the liveness is failed. This must be greater than 1. 

An "attempt" is a completed liveness check that is either rejected or approved. If the user does not complete the liveness check this does not count as an attempt and the user will be prompted to try again.

{% image url="https://image-archive.developerhub.io/image/upload/20557/vx9ombso8moob3g1yidm/1575460964.jpg" caption="Liveness check" mode="600" height="770" width="776" %}
{% /image %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Jump to
    </div>
    <div class="alert-text">
 This will produce a liveness_capture resource in the session as well as a report in the form of a structured JSON object for each attempted liveness check.
    </div>
    <div class="alert-links"> 
        <a href="https://developers.yoti.com/yoti/session-and-media-retrieval">Retrieve results and data</a>
        <a target="_self" href="https://developers.yoti.com/yoti/session-and-media-retrieval#liveness-capture-resources">Liveness results</a> 
   </div>
</div>
{% /html %}

**3) ID Document face match**

A request to assess whether the user's face matches the face on the ID document. The user's facial image is obtained from the liveness check, which must be performed first.

{% code %}
{% tab language="json" %}
"requested_checks": [
    {
      "type": "ID_DOCUMENT_FACE_MATCH",
      "config": {
        "manual_check": "FALLBACK" // | "NEVER" | "ALWAYS"
      }
    }
  ]
{% /tab %}
{% /code %}

This is performed as an automated check, however you can configure whether the check is passed on to our security centre for a manual check by qualified Yoti staff. This can be set to always, fallback or never.

{% table %}
| Manual Check | Explanation | 
| ---- | ---- | 
| ALWAYS | The requested check will always go to the security centre regardless of the success of the automated check. | 
| NEVER | The requested check will never go to the security centre. | 
| FALLBACK | The requested check will only go to the security centre if the machine check fails. | 
{% /table %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Jump to... 
    </div>
    <div class="alert-text">
On successful completion, the check outputs a report in the form of a structured JSON object, which can be found in the ‘checks retrieval’ section of the session retrieval 
    </div>
    <div class="alert-links"> 
        <a href="https://developers.yoti.com/yoti/session-and-media-retrieval">Retrieve results and data</a>
        <a target="_self" href="https://developers.yoti.com/yoti/session-and-media-retrieval#id-document-face-match">ID Document face match results</a> 
   </div>
</div>
{% /html %}

### 4. Tasks Configuration

Yoti can complete the following optional task(s), if requested.

**ID Document text data extraction**

A request to obtain the data printed visually on a document, in structured form.

If machine data extraction is not successful, there is an option (selected at session creation) to fallback to manual data extraction. This generates a ‘text data check’ automatically, and the document is reviewed by one of our document processing experts.

{% code %}
{% tab language="json" %}
"requested_tasks": [
    {
      "type": "ID_DOCUMENT_TEXT_DATA_EXTRACTION",
      "config": {
        "manual_check": "FALLBACK"
      }
    }
  ]
{% /tab %}
{% /code %}

{% table %}
| Manual Data Extraction | Explanation | 
| ---- | ---- | 
| FALLBACK | This will initiate manual data extraction only if the automatic extraction fails. We strongly recommend this option. | 
| NEVER | If the ID fails on automatic extraction, Yoti will not attempt manual extraction and will return a failure in the report. | 
| ALWAYS | The document is always referred for manual review at Yoti's security centre, regardless of whether machine data extraction has suceeded or failed. | 
{% /table %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Jump to
    </div>
    <div class="alert-text">
On successful completion, see the task results section
    </div>
    <div class="alert-links"> 
        <a href="https://developers.yoti.com/yoti/session-and-media-retrieval">Retrieve results and data</a>
        <a target="_self" href="https://developers.yoti.com/yoti/session-and-media-retrieval#retrieved-resources">Retrieved resources</a> 
   </div>
</div>
{% /html %}

{% html %}
<div class="alert-know">
    <div class="alert-title" id="know">
        Knowledge base
    </div>
    <div class="alert-text">
For more information on ID Document Text Data Extraction please head to our knowledge base.
    </div>
    <div class="alert-links"> 
       <a href="https://developers.yoti.com/yoti/knowledge-base-docscan#id-document-text-data-extraction-explained">Text extraction explained</a>
    </div>
</div>
{% /html %}

---

### 5. Client Preferences

The method sdk_config is explained below. These are not mandatory, if not defined then they will be set to default (indicated)

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

{% image url="https://image-archive.developerhub.io/image/upload/20557/ssemb4dxbqggaagtwq1r/1575461026.jpg" caption="Document capture" mode="600" height="790" width="840" %}
{% /image %}

{% table %}
| Type | Parameters (examples) | Description | 
| ---- | ---- | ---- | 
| allowed_capture_methods | CAMERA_AND_UPLOAD, CAMERA(default) | The user must use a camera to take a photo of their ID document, or the user can take a photo or has the option to upload an image of the document from file. | 
| primary_colour | #2d9fff(default), #ff0000 | Colours of the button provided in the frontend client as a hexadecimal value. | 
| preset_issuing_country | USA, GBR | The user must select the issuing country of the document they are uploading. This setting determines which \n\nissuing country is selected by default.\n\n\n\nNOTE: Must be a 3 letter ISO code. | 
| success_url | [https://yourdomain.com/success](https://yourdomain.com/success) | If the upload/photo is successfully captured redirect your users here. Yoti will then begin to carry out the requested checks and tasks. If undefined, the page will not redirect and you can listen to Yoti's post messages on the same page. | 
| error_url | [https://yourdomain.com/error](https://yourdomain.com/error) | If the upload/photo is unsuccessfully captured redirect your users here. If undefined, the user view will display an error screen, with the error code as a query parameter and won't redirect. (Details on the error codes can be found [here](/yoti/render-the-user-view#error-codes).) | 
{% /table %}

**Supported Documents Endpoint**

To see all documents that are supported for Yoti Doc Scan you can send a GET request to our supported-documents endpoint. The request is built in a similar fashion to other Yoti requests, see the examples below.

{% code %}
{% tab language="javascript" %}
const { RequestBuilder } = require("yoti");

const request = new RequestBuilder()
  .withBaseUrl("<YOTI_BASE_URL>/idverify/v1")
  .withPemFilePath("<YOTI_KEY_FILE_PATH>")
  .withEndpoint("/supported-documents")
  .withMethod("GET")
  .withQueryParam("sdkId", "<YOTI_CLIENT_SDK_ID>")
  .build();

//get Yoti response
const response = request.execute();
{% /tab %}
{% tab language="php" %}
<?php
use Yoti\Http\RequestBuilder;
$request = (new RequestBuilder())
    ->withBaseUrl('<YOTI_BASE_URL>/idverify/v1')
    ->withPemFilePath('<YOTI_KEY_FILE_PATH>')
    ->withEndpoint('/supported-documents')
    ->withMethod('GET')
    ->withQueryParam('sdkId', '<YOTI_CLIENT_SDK_ID>')
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
   
    signed_request = (
        SignedRequest
        .builder()
        .with_pem_file("<YOTI_KEY_FILE_PATH>")
        .with_base_url("<YOTI_BASE_URL>/idverify/v1")
        .with_endpoint("/supported-documents")
        .with_http_method("GET")
        .with_param("sdkId", "<YOTI_CLIENT_SDK_ID>")
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
        .withBaseUrl("<YOTI_BASE_URL>/idverify/v1")
        .withEndpoint("/supported-documents")
        .withHttpMethod("GET")
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
    // GET supported documents
    request, _ := requests.SignedRequest{
        HTTPMethod: http.MethodGet,
        BaseURL:    "<YOTI_BASE_URL>/idverify/v1",
        Endpoint:   "/supported-documents",
        Params: map[string]string{
          "sdkId": "<YOTI_CLIENT_SDK_ID>"
        },
        Headers: map[string][]string{
            "Content-Type": {"application/json"},
            "Accept":       {"application/json"}
        },
    }.WithPemFile(key).Request()
	//get Yoti response
	response, _ := http.DefaultClient.Do(request)
{% /tab %}
{% tab language="csharp" %}
// COMING SOON
{% /tab %}
{% tab language="ruby" %}
# COMING SOON
{% /tab %}
{% /code %}

Yoti will return a JSON object with countries listed by ISO country code. Each country will list an array of supported documents from that country. See the example below:

{% code %}
{% tab language="json" %}
{
   "supported_countries": [
      {
         "code": "AGO",
         "supported_documents": [
            {
              "type": "DRIVING_LICENCE"
            },
            {
              "type": "NATIONAL_ID"
            },
            {
              "type": "PASSPORT"
            }
         ]
      },
      {
         "code": "AIA",
         "supported_documents": [
            {
              "type": "PASSPORT"
            }
         ]
      }, ...
{% /tab %}
{% /code %}