---
type: page
title: Create a session
listed: true
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
using System;
using System.IO;
using System.Net.Http;
using Microsoft.AspNetCore.Mvc;
using Yoti.Auth.Web;

class ExampleClass
{
    private Uri _baseUrl = new UriBuilder("https", "api.yoti.com", 443, "idverify/v1").Uri;

    public void ExampleFunction()
    {
        HttpClient httpClient = new HttpClient();
        StreamReader privateKeyStream = System.IO.File.OpenText(_pemFilePath);

        byte[] byteContent = ...; // JSON Request
        string clientSdkId = Environment.GetEnvironmentVariable("YOTI_CLIENT_SDK_ID");

        Yoti.Auth.Web.Request docScanRequest = new RequestBuilder()
            .WithKeyPair(privateKeyStream)
            .WithBaseUri(_baseUrl)
            .WithEndpoint("/session")
            .WithPayload(byteContent)
            .WithHttpMethod(HttpMethod.Post)
            .WithQueryParam("sdkId", clientSdkId)
            .Build();

        HttpResponseMessage response = docScanRequest.Execute(httpClient).Result;
    }
}
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
    "session_deadline": "2024-09-03T23:59:59.000000+00:00",
    "resources_ttl": "1209600",
    "ibv_options": {
        "support": "MANDATORY"
    },
    "user_tracking_id": "some_id",
    "notifications": {
        "endpoint": "https://some-domain.example",
        "topics": [
            "SESSION_COMPLETION"
        ]
    },
    "requested_checks": [
        {
            "type": "IBV_VISUAL_REVIEW_CHECK",
            "config": {
                "manual_check": "IBV"
            }
        },
        {
            "type": "PROFILE_DOCUMENT_MATCH",
            "config": {
                "manual_check": "IBV"
            }
        },
        {
            "type": "DOCUMENT_SCHEME_VALIDITY_CHECK",
            "config": {
                "manual_check": "IBV",
                "scheme": "UK_DBS"
            }
        }
    ],
    "required_documents": [
        {
            "type": "ID_DOCUMENT",
            "filter": {
                "type": "DOCUMENT_RESTRICTIONS",
                "inclusion": "WHITELIST",
                "documents": [
                    {
                        "country_codes": [
                            "GBR"
                        ],
                        "document_types": [
                            "PASSPORT"
                        ]
                    }
                ]
            }
        },
        {
            "type": "ID_DOCUMENT",
            "filter": {
                "type": "DOCUMENT_RESTRICTIONS",
                "inclusion": "WHITELIST",
                "documents": [
                    {
                        "country_codes": [
                            "GBR"
                        ],
                        "document_types": [
                            "DRIVING_LICENCE"
                        ]
                    }
                ]
            }
        },
        {
            "type": "SUPPLEMENTARY_DOCUMENT",
            "document_types": [
                "UTILITY_BILL"
            ],
            "country_codes": [
                "GBR"
            ],
            "objective": {
                "type": "UK_DBS"
            }
        }
    ],
    "resources": {
        "applicant_profile": {
            "full_name": "John James Doe",
            "date_of_birth": "1988-11-02",
            "structured_postal_address": {
                "address_format": 1,
                "building_number": "74",
                "address_line1": "74 Address Line 1",
                "town_city": "CityName",
                "postal_code": "E14 3RN",
                "country_iso": "GBR",
                "country": "United Kingdom"
            }
        }
    }
}
{% /tab %}
{% /code %}

{% table widths="212,0" %}
| Name | Description | Optional | 
| ---- | ---- | ---- | 
| resources_ttl | Retention period ("time to live") for uploaded documents/images in number of seconds. Default is one week (`60_60_24*7=604800`).\n\nThis value must be at least 24 hours longer than the `client_session_token_ttl`. | ✅ | 
| user__tracking__id | Allows the relying business backend to track the same user across multiple sessions. **Note:** This should not contain any personal identifiable information | ✅ | 
| ibv_options | Outlines that an IBV session is being generated. | ✅ | 
| session_deadline | This is in a date format. The user has up until this date to complete the session. Note: we also have client_session_token_ttl (seconds) to set your session expiry. |  | 
| client_session_token_ttl | An alternative to the session_deadline. Allows a session timer to be specified in seconds, rather than a date time. |  | 
{% /table %}

### Notifications

This service optionally posts an update notification every time the session state changes, based on the selected subscription topics.

{% table widths="26" %}
| Name | Description | 
| ---- | ---- | 
| NEW_PDF_SUPPLIED | You can subscribe to be notified when the user has got the PDF.\n\nOnly relevant when using the At home flow. | 
| INSTRUCTIONS_EMAIL_REQUESTED | If you do not enable this notification an email will automatically be sent to the user with their instructions. If you do enable this notification the email service will be revoked and you will need to configure this set up yourself. Yoti will send an async notification to prompt you to retrieve the PDF from Yoti and send it to the customer. | 
| THANK_YOU_EMAIL_REQUESTED | Enabling this notification suppresses the final email a user receives after completing their journey in the branch. You may want to enable this if planning to send your own completion email. | 
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

Please check out the overview page for which documents we support.In the example below and above, three documents are being set for the applicant (each document is one object in the list).

{% code %}
{% tab language="json" %}
"required_documents": [
        {
            "type": "ID_DOCUMENT",
            "filter": {
                "type": "DOCUMENT_RESTRICTIONS",
                "inclusion": "WHITELIST",
                "documents": [
                    {
                        "country_codes": [
                            "GBR"
                        ],
                        "document_types": [
                            "PASSPORT"
                        ]
                    }
                ]
            }
        },
        {
            "type": "ID_DOCUMENT",
            "filter": {
                "type": "DOCUMENT_RESTRICTIONS",
                "inclusion": "WHITELIST",
                "documents": [
                    {
                        "country_codes": [
                            "GBR"
                        ],
                        "document_types": [
                            "DRIVING_LICENCE"
                        ]
                    }
                ]
            }
        },
        {
            "type": "SUPPLEMENTARY_DOCUMENT",
            "document_types": [
                "UTILITY_BILL"
            ],
            "country_codes": [
                "GBR"
            ],
            "objective": {
                "type": "UK_DBS"
            }
        }
    ],
{% /tab %}
{% /code %}

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
| structured_postal_address | Object | StructuredPostalAddress is the postal address with the breakdown in address lines, post code and so on as well as the formatted address all in one line. See details for structured_postal_address JSON properties below. | See below | 
{% /table %}

#### Structured postal address

{% synced id="structuredpostaladdress" %}
{% /synced %}

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
GET https://api.yoti.com/idverify/v1/sessions/{sessionId}/configuration
{% /tab %}
{% /code %}

### Example

{% code %}
{% tab language="json" %}
{
    "session_id": "c02daa68-ec36-4687-9d4f-090a54b575cc",
    "client_session_token_ttl": 2100341,
    "requested_checks": [
        "IBV_VISUAL_REVIEW_CHECK",
        "DOCUMENT_SCHEME_VALIDITY_CHECK",
        "PROFILE_DOCUMENT_MATCH"
    ],
    "applicant_profile": {
        "media": {
            "id": "c709d220-edd6-4ba6-8494-b9aac6685e19",
            "type": "JSON",
            "created": "2022-10-18T16:33:59Z",
            "last_updated": "2022-10-18T16:33:59Z"
        }
    },
    "capture": {
        "required_resources": [
            {
                "type": "ID_DOCUMENT",
                "id": "d430440c-5c6d-402c-9855-3aebc8145a94",
                "state": "REQUIRED",
                "allowed_sources": [
                    {
                        "type": "IBV"
                    }
                ],
                "requested_tasks": [],
                "ibv_client_assessments": [
                    {
                        "type": "IBV_VISUAL_REVIEW_CHECK",
                        "state": "REQUIRED"
                    },
                    {
                        "type": "DOCUMENT_SCHEME_VALIDITY_CHECK",
                        "state": "REQUIRED",
                        "scheme": "UK_DBS"
                    },
                    {
                        "type": "PROFILE_DOCUMENT_MATCH",
                        "state": "REQUIRED"
                    }
                ],
                "supported_countries": [
                    {
                        "code": "GBR",
                        "supported_documents": [
                            {
                                "type": "PASSPORT"
                            }
                        ]
                    }
                ],
                "allowed_capture_methods": "CAMERA",
                "attempts_remaining": {
                    "RECLASSIFICATION": 2,
                    "GENERIC": 2
                }
            },
            {
                "type": "ID_DOCUMENT",
                "id": "d33f1c38-2f4a-4d10-a22b-971ac63132ce",
                "state": "REQUIRED",
                "allowed_sources": [
                    {
                        "type": "IBV"
                    }
                ],
                "requested_tasks": [],
                "ibv_client_assessments": [
                    {
                        "type": "IBV_VISUAL_REVIEW_CHECK",
                        "state": "REQUIRED"
                    },
                    {
                        "type": "DOCUMENT_SCHEME_VALIDITY_CHECK",
                        "state": "REQUIRED",
                        "scheme": "UK_DBS"
                    },
                    {
                        "type": "PROFILE_DOCUMENT_MATCH",
                        "state": "REQUIRED"
                    }
                ],
                "supported_countries": [
                    {
                        "code": "GBR",
                        "supported_documents": [
                            {
                                "type": "DRIVING_LICENCE"
                            }
                        ]
                    }
                ],
                "allowed_capture_methods": "CAMERA",
                "attempts_remaining": {
                    "RECLASSIFICATION": 2,
                    "GENERIC": 2
                }
            },
            {
                "type": "SUPPLEMENTARY_DOCUMENT",
                "id": "b23048de-0927-4a42-bd38-762d904d9fd7",
                "state": "REQUIRED",
                "allowed_sources": [
                    {
                        "type": "IBV"
                    }
                ],
                "requested_tasks": [],
                "ibv_client_assessments": [
                    {
                        "type": "IBV_VISUAL_REVIEW_CHECK",
                        "state": "REQUIRED"
                    },
                    {
                        "type": "DOCUMENT_SCHEME_VALIDITY_CHECK",
                        "state": "REQUIRED",
                        "scheme": "UK_DBS"
                    },
                    {
                        "type": "PROFILE_DOCUMENT_MATCH",
                        "state": "REQUIRED"
                    }
                ],
                "document_types": ["UTILITY_BILL"],
                "country_codes": ["GBR"],
                "objective": {
                    "type": "UK_DBS"
                }
            }
        ],
        "biometric_consent": "NOT_REQUIRED"
    },
    "sdk_config": {
        "primary_colour": "#D71440",
        "locale": "en-GB",
        "hide_logo": false,
        "allow_handoff": false
    },
    "track_ip_address": true
}
{% /tab %}
{% /code %}