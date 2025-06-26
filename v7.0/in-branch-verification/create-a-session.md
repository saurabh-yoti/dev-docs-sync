---
type: page
title: Create a session
listed: false
slug: create-a-session
description: 
index_title: Create a session
hidden: 
keywords: 
tags: 
---

This section will show you how to:

- Authentication
- Create the session
- Fetch the session

---

## Authentication

Please use our Yoti SDKs to automatically build the relevant session for you. First you will need the following information about your application from [Yoti Hub](https://hub.yoti.com/login):

- Yoti SDK ID
- Your application key pair.

There are two ways in which generate a signed request:

- Generate signed request
- SDK request builder. 

### Generate signed request

You can create your own signed request using the below endpoint:

{% code %}
{% tab language="http" title="HTTP" %}
GET /sessions?sdkId=b88ad843-13cc-44ba-a3e0-053f71d89b1f&nonce=b88ad843-13cc-44ba-a3e0-053f71d89b1f&timestamp=1480509893

POST /sessions?sdkId=b88ad843-13cc-44ba-a3e0-053f71d89b1f&nonce=b88ad843-13cc-44ba-a3e0-053f71d89b1f&timestamp=1480509893&ew0KImlkIiA6IDEsDQoibmFtZSIgOiBpdGVtDQoNCn0=
{% /tab %}
{% /code %}

Concatenate the:

- HTTP method
- The path 
- The query string (enriched with a timestamp and a nonce parameter)
- The base64 encoded request body, if available, using the & character

Apply SHA256withRSA to the string generated from 1. Base64 encode the result from 2, so that it can be sent as a string for the **X-Yoti-Auth-Digest** header.

{% table %}
| Parameter | Description | 
| ---- | ---- | 
| SDK ID | UUID generated when producing your Yoti keys | 
| nonce | Nonces are UUID strings | 
| Timestamp | UNIX timestamps (number of elapsed seconds since Jan 1st 1970). | 
{% /table %}

### SDK request builder

Please use our Yoti SDKs to automatically build the relevant request. The Yoti SDKs are available via popular dependency management systems.

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

{% code %}
{% tab language="javascript" %}
const { RequestBuilder, Payload } = require("yoti");

const request = new RequestBuilder()
  .withBaseUrl("https://api.yoti.com/idverify/v1")
  .withPemFilePath("<YOTI_KEY_FILE_PATH>") // file path to PEM file
  .withEndpoint("/sessions")
  .withPayload(new Payload(SESSION_OBJ))
  .withMethod("POST")
  .withQueryParam("sdkId", "<YOTI_CLIENT_SDK_ID>")
  .build();

//get Yoti response
const response = await request.execute();
{% /tab %}
{% tab language="php" %}
<?php
use Yoti\Http\RequestBuilder;
use Yoti\Http\Payload;
$request = (new RequestBuilder())
    ->withBaseUrl('https://api.yoti.com/idverify/v1')
    ->withPemFilePath('<YOTI_KEY_FILE_PATH>')
    ->withEndpoint('/sessions')
    ->withPayload(Payload::fromString(SESSION_JSON_STRING)) // * Version ^2: new Payload(SESSION_OBJ)
    ->withMethod('POST')
    ->withQueryParam('sdkId', '<YOTI_CLIENT_SDK_ID>')
    ->build()
    //get Yoti Response
    ->execute();

// * For JSON data in Version >3 please use Payload::fromJsonData(SESSION_OBJ)
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

    payload = {} # payload
    payload_string = json.dumps(payload).encode()
   
    signed_request = (
        SignedRequest
        .builder()
        .with_pem_file("<YOTI_KEY_FILE_PATH>")
        .with_base_url("https://api.yoti.com/idverify/v1")
        .with_endpoint("/sessions")
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
byte[] SESSION_OBJ = ...

try {
    SignedRequest signedRequest = SignedRequestBuilder.newInstance()
        .withKeyPair(<YOTI_KEY_FILE_PATH>)
        .withBaseUrl("https://api.yoti.com/idverify/v1")
        .withEndpoint("/sessions")
        .withPayload(SESSION_OBJ)
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
    // Create session
    request, _ := requests.SignedRequest{
        HTTPMethod: http.MethodPost,
        BaseURL:    "https://api.yoti.com/idverify/v1",
        Endpoint:   "/sessions",
        Params: map[string]string{
          "sdkId": "<YOTI_CLIENT_SDK_ID>"
        },
        Headers: map[string][]string{
            "Content-Type": {"application/json"},
            "Accept":       {"application/json"}
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
# COMING SOON
{% /tab %}
{% /code %}

Once you have added the Yoti SDK dependency to your project, you can use it to build and send your request. See the code snippets below for examples of how to construct the session.

---

## Create session

You can use it to build and send your session as shown in the code snippet below.  You will need to ensure you have captured applicant details including:

- Applicant information: Name, DOB and Address.
- Which three documents they will be bringing to the branch. 
- A branch look up service. 

This information is needed at a minimum to fulfil the DBS requirements.

{% badge type="success" text="Hint" /%} remember to pass the **X-Yoti-Auth-Digest** as a header when making the requests

{% code %}
{% tab language="http" %}
POST https://api.yoti.com/idverify/v1/sessions
{% /tab %}
{% /code %}

### Example

{% code %}
{% tab language="json" %}
{
  "client_session_token_ttl": 604800,
  "resources_ttl": 1604800,
  "user_tracking_id": "some_string",
  "ibv_options": {
    "support": "MANDATORY"
  },
  "notifications": {
    "endpoint": "https://domain.example",
    "topics": [
      "SESSION_COMPLETION",
      "INSTRUCTIONS_EMAIL_REQUESTED",
      "NEW_PDF_SUPPLIED"
      
    ],
    "auth_token": "string",
    "auth_type": "BASIC"
  }
  "requested_checks": [
    {
      "type": "IBV_VISUAL_REVIEW_CHECK",
      "config": {
        "manual_check": "IBV"
      }
    },
    {
      "type": "DOCUMENT_SCHEME_VALIDITY_CHECK",
      "config": {
        "scheme": "UK_DBS",
        "manual_check": "IBV"
      }
    },
    {
      "type": "PROFILE_DOCUMENT_MATCH",
      "config": {
        "manual_check": "IBV"
      }
    }
  ],
  "required_documents": [
    {
      "type": "ID_DOCUMENT",
      "filter": {
        "type": "DOCUMENT_RESTRICTION",
        "inclusion": "WHITELIST",
        "documents": [
          {
            "country_codes": ["GBR"],
            "document_types": ["PASSPORT]"
          }
        ]
      }
    },
    {
      "type": "ID_DOCUMENT",
      "filter": {
        "type": "DOCUMENT_RESTRICTION",
        "inclusion": "WHITELIST",
        "documents": [
          {
            "country_codes": ["GBR"],
            "document_types": ["DRIVING_LICENCE]"
          }
        ]
      }
    },
    {
      "type": "SUPPLEMENTARY_DOCUMENT",
      "country_codes": [ "GBR" ],
      "document_types": [ "UTILITY_BILL" ],
      "objective": {
        "type": "UK_DBS",
        "config": {}
      }
    }
  ],
  "applicant_profile": {
    "title": "Mr",
    "full_name": "John Doe",
    "given_name": "John",
    "family_name": "Doe",
    "middle_name": "James Henry",
    "date_of_birth": "1988-11-02",
    "address": {
      "building_number": "someValueHere",
      "building_name": "someValueHere",
      "sub_building_name": "someValueHere",
      "address_line_1": "someValueHere",
      "address_line_2": "someValueHere",
      "address_line_3": "someValueHere",
      "town": "someValueHere",
      "country": "someValueHere",
      "postal_code": "someValueHere",
      "postal_address": "someValueHere",
      "structured_postal_address": "someValueHere"
    }
  }
}
{% /tab %}
{% /code %}

{% table widths="212,0" %}
| Name | Description | Optional | 
| ---- | ---- | ---- | 
| client_session_token_ttl | Dictates how long the applicant has to complete the session in seconds. This must be longer than 300s (5 minutes). | ✅ | 
| resources_ttl | Retention period ("time to live") for uploaded documents/images in number of seconds. Default is one week (`60_60_24*7=604800`). This can be a minimum of 24 hours and must be at least 24 hours longer than the client_session_token_ttl. This starts once the `client_session_token_ttl` is completed. | ✅ | 
| user__tracking__id | Allows the relying business backend to track the same user across multiple sessions. **Note:** This should not contain any personal identifiable information | ✅ | 
| ibv_options | Outlines that an IBV session is being generated. | ✅ | 
{% /table %}

### Notifications

This service optionally posts an update notification every time the session state changes, based on the selected subscription topics.

{% table widths="26" %}
| Name | Description | 
| ---- | ---- | 
| NEW_PDF_SUPPLIED | You can subscribe to be notified when the user has got the PDF. | 
| INSTRUCTIONS_EMAIL_REQUESTED | If you do not enable this notification an email will automatically be sent to the user with their instructions. If you do enable this notification the email service will be revoked and you will need to configure this set up yourself. Yoti will send an async notification to prompt you to retrieve the PDF from Yoti and send it to the customer. | 
| SESSION_COMPLETION | Triggered when all tasks and all checks inside of a given session have been completed. | 
{% /table %}

## Requested checks

The below represents the in-person checks.

{% table %}
| Check | Description | 
| ---- | ---- | 
| PROFILE_DOCUMENT_MATCH | Checks the document the applicant brought with them matches the submitted applicant profile. | 
| DOCUMENT__SCHEME__VALIDITY_CHECK | Checks the documents themselves fit within the rule of that scheme. E.g. DBS have rules of bills and expiry e.g. valid for the last 3 months or issued within X time. | 
| IBV_VISUAL_REVIEW_CHECK | A visual review of the document by the postmaster. | 
{% /table %}

### Required documents

Please check out the overview page for which documents we support.

{% table widths="138" %}
| Name | Description | 
| ---- | ---- | 
| type | Outlines the type of documents required. Either an ID document or supplementary document. | 
{% /table %}

### Applicant profile

This is the customer information you will collect before generating the session.

{% table widths="154,0,330" %}
| Name | Type | Description | Example | 
| ---- | ---- | ---- | ---- | 
| full_name | String | FullName contains given names and family name. | “Jon Jim Foo” | 
| date_of_birth | String | DateOfBirth is the date of birth in the form yyyy-mm-dd. | "2000-12-01" | 
| given_names | String | GivenNames contains first and middle names. | "Jon Jim" | 
| first_name | String | FirstName is the first name only. | “Jon” | 
| middle_name | String | MiddleName contains the middle names only. | “Jim” | 
| family_name | String | The family name. | “Foo” | 
| building_number | String | BuildingNumber is the number of the building. | "15a" | 
| building_name | String | Building is the name of the building. | "Fountain House" | 
| sub_building_name | String | SubBuilding is used when the building is divided into smaller units (e.g. a block of flats) to identify the sub unit. | "Copper works Flat 4" | 
| address_line1 | String | AddressLine1 is the first line of the address. | "15a North Street" | 
| address_line2 | String | AddressLine2 is the second line of the address. | "Flat 4" | 
| town | String | Town is the town/city/village/hamlet/community/etc. that the building is in. | "CARSHALTON" | 
| country | String | Country is the country the building is in. Localised. | "UK" | 
| postal_code | String | PostalCode is a code used by the country's postal service to aid in sorting and delivering mail (e.g. postcode, zipcode, pincode). | "SM1 2JW" | 
| postal_address | String | The full address. |  | 
{% /table %}

---

## Example response

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
| client_session_token_ttl | Time in seconds until the client session expires | 
| client_session_token | Used to authenticate the session | 
| session_id | ID of the session | 
{% /table %}

---

## Fetch session config

This endpoint will retrieve the session configuration, and also provide the requirement ID to be used for the instructions. This will be in a UUID format per document requested. 

{% code %}
{% tab language="http" %}
GET https://api.yoti.com/sessions/{sessionId}/configuration
{% /tab %}
{% /code %}

### Example

{% code %}
{% tab language="json" %}
"type": "SUPPLEMENTARY_DOCUMENT",
                "id": "4b0c16e6-8437-4501-9361-a51de362f93c",
                "state": "REQUIRED",
                "allowed_sources": [
                    {
                        "type": "IBV"
                    }
                ],
                "requested_tasks": [],
                "document_types": [
                    "UTILITY_BILL",
                    "COUNCIL_TAX_BILL",
                    "PHONE_BILL",
                    "BANK_STATEMENT"
                ],
               ...
                "type": "ID_DOCUMENT",
                "id": "4c723a12-ffd4-4643-838d-d2a0fb684cbc",
                "state": "REQUIRED",
                "allowed_sources": [
                    {
                        "type": "IBV"
                    }
                ],
                "requested_tasks": [],
               ...
{% /tab %}
{% /code %}