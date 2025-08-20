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

- Authenticate the request
- Create a session

---

## [Authentication](https://developers.yoti.com/in-branch-verification/create-a-session#authentication)

From here on, each endpoint requires an RSA-signed request for Authentication. This can either be constructed manually or via one of our backend SDKs. The Yoti SDK exposes a simple request builder class to support the authentication process, and the examples provide snippets of this usage in each endpoint code snippet. You will need your Yoti SDK ID and application key pair for either process.

The method is detailed below if you prefer to authenticate without the SDK. 

### [Generate signed request](https://developers.yoti.com/in-branch-verification/create-a-session#generate-signed-request)

Yoti API endpoints are authenticated through signed requests, and the current approach for building signed requests consists of passing the following HTTP Header:

- X-Yoti-Auth-Digest

Here's how to compute it:

1. Concatenate the HTTP method, the path, the query string (enriched with a timestamp and a nonce parameter) and the base64 encoded request body, if available, using the & character.

Example GET request:

{% code %}
{% tab language="http" %}
GET GET&/sessions?sdkId=b88ad843-13cc-44ba-a3e0-053f71d89b1f&nonce=b88ad843-13cc-44ba-a3e0-053f71d89b1f&timestamp=1480509893
{% /tab %}
{% /code %}

Example POST request:

{% code %}
{% tab language="http" %}
POST POST&/sessions?sdkId=b88ad843-13cc-44ba-a3e0-053f71d89b1f&nonce=b88ad843-13cc-44ba-a3e0-053f71d89b1f&timestamp=1480509893&ew0KImlkIiA6IDEsDQoibmFtZSIgOiBpdGVtDQoNCn0=
{% /tab %}
{% /code %}

2. Apply SHA256withRSA to the string generated from step 1, using your PEM private key generated from the Yoti Hub.
3. Base64 encode the result from 2, so that it can be sent as a string header.

The API Base URL is [https://api.yoti.com/idverify/v1](https://api.yoti.com/idverify/v1)

{% table widths="" %}
| Parameter | Description | 
| ---- | ---- | 
| sdkId | UUID generated when producing your Yoti keys | 
| nonce | Nonces are UUID strings | 
| timestamp | UNIX timestamps (number of elapsed seconds since Jan 1st 1970) | 
{% /table %}

### [SDK request builder](https://developers.yoti.com/in-branch-verification/create-a-session#sdk-request-builder)

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
{% tab language="csharp" %}
// COMING SOON
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
    ->withPayload(Payload::fromJsonData($payload)) 
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
// Coming soon
{% /tab %}
{% /code %}

## [Create session](https://developers.yoti.com/in-branch-verification/create-a-session#create-session)

You can use it to build and send your session as shown in the code snippet below. For the claimed ID version you will need to ensure you have captured applicant details including:

- Applicant information: Name, DOB and Address.
- Which three documents they will be bringing to the branch.
- A branch look up service.

This information is needed at a minimum to fulfil the DBS requirements.

{% code %}
{% tab language="http" %}
POST https://api.yoti.com/idverify/v1/sessions
{% /tab %}
{% /code %}

### Example Payloads

{% code %}
{% tab language="json" title="Claimed ID JSON" %}
{
    "session_deadline": "2023-10-15T22:00:00Z",
    "resources_ttl": "604800",
    "ibv_options": {
        "support": "MANDATORY"
    },
    "user_tracking_id": "optional_string",
    "notifications": {
        "endpoint": "https://some-domain.example",
        "topics": [
            "INSTRUCTIONS_EMAIL_REQUESTED",
            "THANK_YOU_EMAIL_REQUESTED",
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
                        "country_codes": ["GBR"],
                        "document_types": ["PASSPORT"]
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
                        "country_codes": ["GBR"],
                        "document_types": ["DRIVING_LICENCE"]
                    }
                ]
            }
        },
        {
            "type": "SUPPLEMENTARY_DOCUMENT",
            "document_types": ["UTILITY_BILL"],
            "country_codes": ["GBR"],
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
                "address_line1": "74 First Address Line",
                "town_city": "London",
                "postal_code": "E14 3RN",
                "country_iso": "GBR",
                "country": "United Kingdom"
            }
        }
    }
}
{% /tab %}
{% tab language="javascript" title="Resultant ID JSON" %}
{
    "session_deadline": "2023-10-15T22:00:00Z",
    "resources_ttl": "604800",
    "user_tracking_id": "some-tracking-id",
    "ibv_options": {
        "required": true,
        "support": "MANDATORY",
        "guidance_url": "https://yourDomain"
    },
    "notifications": {
        "endpoint": "https://yourDomain",
        "topics": [
            "RESOURCE_UPDATE",
            "TASK_COMPLETION",
            "CHECK_COMPLETION",
            "SESSION_COMPLETION",
            "NEW_PDF_SUPPLIED",
            "INSTRUCTIONS_EMAIL_REQUESTED"
        ],
        "auth_token": "xxx",
        "auth_type": "BASIC"
    },
    "requested_checks": [
        {
            "type": "ID_DOCUMENT_AUTHENTICITY",
            "config": {
                "manual_check": "ALWAYS"
            }
        },
        {
            "type": "ID_DOCUMENT_FACE_MATCH",
            "config": {
                "manual_check": "FALLBACK"
            }
        },
        {
            "type": "ID_DOCUMENT_COMPARISON",
            "config": {}
        },
        {
            "type": "THIRD_PARTY_IDENTITY",
            "config": {
                "manual_check": "NEVER"
            }
        },
        {
            "type": "WATCHLIST_SCREENING",
            "config": {
                "manual_check": "NEVER",
                "categories": ["ADVERSE-MEDIA"]
            }
        }
    ],
    "requested_tasks": [
        {
            "type": "ID_DOCUMENT_TEXT_DATA_EXTRACTION",
            "config": {
                "manual_check": "FALLBACK",
                "chip_data": "DESIRED"
            }
        },
        {
            "type": "SUPPLEMENTARY_DOCUMENT_TEXT_DATA_EXTRACTION",
            "config": {
                "manual_check": "FALLBACK"
            }
        }
    ],
    "required_documents": [
        {
            "type": "ID_DOCUMENT",
            "filter": {
                "type": "ORTHOGONAL_RESTRICTIONS",
                "country_restriction": {
                    "inclusion": "WHITELIST",
                    "country_codes": ["GBR"]
                },
                "type_restriction": {
                    "inclusion": "WHITELIST",
                    "document_types": ["PASSPORT"]
                }
            }
        },
        {
            "type": "SUPPLEMENTARY_DOCUMENT",
            "country_codes": ["GBR"],
            "document_types": ["BANK_STATEMENT"],
            "objective": {
                "type": "PROOF_OF_ADDRESS",
                "config": {}
            }
        }
    ]
}
{% /tab %}
{% tab language="json" title="Hybrid JSON" %}
{
    "session_deadline": "2023-10-15T22:00:00Z",
    "resources_ttl": "604800",
    "ibv_options": {
        "support": "MANDATORY"
        "user_price": {
          "amount": "0",
          "currency": "GBP"
        }
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
            "type": "ID_DOCUMENT_AUTHENTICITY",
            "config": {
                "manual_check": "ALWAYS"
            }
        },
        {
            "type": "ID_DOCUMENT_FACE_MATCH",
            "config": {
                "manual_check": "FALLBACK"
            }
        },
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
    "requested_tasks": [
        {
            "type": "ID_DOCUMENT_TEXT_DATA_EXTRACTION",
            "config": {
                "manual_check": "FALLBACK"
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
                "address_line1": "74 First Address Line",
                "town_city": "London",
                "postal_code": "E14 3RN",
                "country_iso": "GBR",
                "country": "United Kingdom"
            }
        }
    }
}
{% /tab %}
{% /code %}

{% table widths="" %}
| Name | Description | Optional | 
| ---- | ---- | ---- | 
| session_deadline | This is in a datetime format. The user has up until this date and time to complete the session. The customer letter will only show the date, not the time, and therefore we recommend setting the time to 22:00 to ensure a candidate has the entire day to enter a Post Office branch.\n\n\n\nThis must be a minimum of 7 days. |  | 
| resources_ttl | This sets the retention time for images, document data and the applicant profile data in the session. This timer must be configured to be at least 24 hours longer than your `session_deadline`. It starts from the first media upload. |  | 
| user_tracking_id | Allows the relying business backend to track the same user across multiple sessions. **Note:** This should not contain any personal identifiable information | ✅ | 
| ibv_options | Outlines that an IBV session is being generated. |  | 
{% /table %}

#### [Notifications](https://developers.yoti.com/in-branch-verification/create-a-session#notifications)

This service optionally posts an update notification every time the session state changes, based on the selected subscription topics.

{% table widths="290" %}
| Name | Description | 
| ---- | ---- | 
| NEW_PDF_SUPPLIED | You can subscribe to be notified when the user has got the PDF.\n\nOnly relevant when using the At home flow. | 
| INSTRUCTIONS_EMAIL_REQUESTED | If you do not enable this notification an email will automatically be sent to the user with their instructions. If you do enable this notification the email service will be revoked and you will need to configure this set up yourself. Yoti will send an async notification to prompt you to retrieve the PDF from Yoti and send it to the customer. | 
| THANK_YOU_EMAIL_REQUESTED | Enabling this notification suppresses the final email a user receives after completing their journey in the branch. You may want to enable this if planning to send your own completion email. | 
| FIRST_BRANCH_VISIT | This notification is triggered when an applicant has had their customer letter QR code scanned in a Post Office branch for the first time.\n\nThe notification could be used to assess whether a customer has visited a branch location, but been turned away due to no follow up session completion. | 
| SESSION_COMPLETION | Triggered when all tasks and all checks inside of a given session have been completed. | 
{% /table %}

### Requested In Person Checks

{% table widths="" %}
| Check | Description | 
| ---- | ---- | 
| PROFILE_DOCUMENT_MATCH | Checks the document the applicant brought with them matches the submitted applicant profile. | 
| DOCUMENT_SCHEME_VALIDITY_CHECK | Checks the documents themselves fit within the rule of that scheme. E.g. DBS have rules of bills and expiry e.g. valid for the last 3 months or issued within X time. | 
| IBV_VISUAL_REVIEW_CHECK | A visual review of the document by the postmaster. | 
{% /table %}

### Additional Optional Checks

This service is highly configurable, if you would like assistance in using any of the checks below please get in touch with our client support team through [support.yoti.com](https://support.yoti.com).

{% table widths="" %}
| Check | Description | 
| ---- | ---- | 
| Document authenticity | A request to assess the characteristics of a document, to determine the validity of the ID document. Yoti will perform multiple checks on a ID document. | 
| Text extraction | A request to obtain the data printed visually on a document, in sta ructured form. | 
| Supporting documents | Yoti offers the ability to request additional documents to enhance the verification of the user. | 
| Document comparison | If you request your users to upload more than one document we offer the ability to cross check the data | 
| Face match check | A request to assess whether the user's face matches the face on the ID document. | 
| Address check | This check will facilitate an extra verification of a user by searching a person’s details against a collated database from various sources worldwide. | 
| AML check | Extend the Identity verification integration by requesting an watchlist, PEPs and sanctions check as part of a session. | 
{% /table %}

### [Required documents](https://developers.yoti.com/in-branch-verification/create-a-session#required-documents)

Please check out the overview page for which documents we support. In the example below and above, three documents are being set for the applicant (each document is one object in the list).

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

{% table widths="194" %}
| Name | Description | 
| ---- | ---- | 
| type | Outlines the type of documents required. Either an ID document or supplementary document. | 
{% /table %}

### Applicant Profile

This is the customer information you will collect before generating the session.

{% table widths="170,0,0" %}
| Name | Type | Description | Example | 
| ---- | ---- | ---- | ---- | 
| full_name | String | FullName contains given names and family name. | “Jon Jim Foo” | 
| date_of_birth | String | DateOfBirth is the date of birth in the form yyyy-mm-dd. | "2000-12-01" | 
| structured_postal_address | Object | StructuredPostalAddress is the postal address with the breakdown in address lines, post code and so on as well as the formatted address all in one line. See details for `structured_postal_address` JSON properties below. | See below | 
{% /table %}

#### Structured Postal Address

{% synced id="structuredpostaladdress" %}
{% /synced %}

## [Example response](https://developers.yoti.com/in-branch-verification/create-a-session#example-response)

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

{% table widths="" %}
| Name | Description | 
| ---- | ---- | 
| client_session_token_ttl | Time in seconds until the client session expires | 
| client_session_token | Used to authenticate the session | 
| session_id | ID of the session | 
{% /table %}

## Error Responses

If the request is unsuccessful you will receive one of the below error responses in the form:

{% code %}
{% tab language="json" %}
// 400 response
{
  "code": "PAYLOAD_VALIDATION",
  "errors": [
    {
      "property": "requested_checks",
      "message": "must not be empty"
    }
  ]
}
{% /tab %}
{% /code %}

{% table widths="231" %}
| Error code | Description | 
| ---- | ---- | 
| 400 | payload validation error | 
| 401 | unauthorised request, wrong key used | 
| 403 | application is disabled or no associated organisation id | 
| 404 | the application for provided sdk id does not exist | 
| 503 | service is unavailable | 
{% /table %}