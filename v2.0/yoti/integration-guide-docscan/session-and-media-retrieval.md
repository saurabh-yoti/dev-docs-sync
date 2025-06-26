---
type: page
title: Retrieve results and data
listed: true
slug: session-and-media-retrieval
description: 
index_title: Retrieve results and data
hidden: 
keywords: 
tags: 
---

The response will detail all information, check and task completion status, resource and media data, along with the associated media identifiers. 

Sessions can be retrieved at any time, however the integrating backend will be notified when a session update occurs, according to the notifications settings provided at session creation.

## Get Session Request

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      Please see our create a session section
   </div>
   <div class="alert-links"> 
         <a href="https://developers.yoti.com/yoti/generating-a-session">Create a session</a>
   </div>
</div>
{% /html %}

Please note:

- `withMethod` should be set to `GET`
- The `withEndpoint` should be set to `/sessions/SESSION_ID` where `SESSION_ID` should be replaced with the `SESSION_ID` obtained at [auto$](/yoti/generating-a-session#example-response-payload).

{% code %}
{% tab language="javascript" %}
const { RequestBuilder, Payload } = require("yoti");

const request = new RequestBuilder()
  .withBaseUrl("https://api.yoti.com/idverify/v1")
  .withPemFilePath("<YOTI_KEY_FILE_PATH>")
  .withEndpoint(`/sessions/<SESSION_ID>`)
  .withMethod("GET")
  .withQueryParam("sdkId", "<YOTI_CLIENT_SDK_ID>")
  .build();

//get Yoti response
const response = request.execute();
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\Http\RequestBuilder;
use Yoti\Http\Payload;

$request = (new RequestBuilder())
    ->withBaseUrl('https://api.yoti.com/idverify/v1')
    ->withPemFilePath('<YOTI_KEY_FILE_PATH>')
    ->withEndpoint('/sessions/<SESSION_ID>')
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


def get_session():

    signed_request = (
        SignedRequest
        .builder()
        .with_pem_file("<YOTI_KEY_FILE_PATH>")
        .with_base_url("https://api.yoti.com/idverify/v1")
        .with_endpoint("/sessions/<SESSION_ID>")
        .with_http_method("GET")
        .with_param("sdkId", "<YOTI_CLIENT_SDK_ID>")
        .build()
    )

    response = signed_request.execute()
    response_payload = json.loads(response.text)

//get Yoti response
print(get_session())
{% /tab %}
{% tab language="java" %}
byte[] payload = ...

try {
    SignedRequest signedRequest = SignedRequestBuilder.newInstance()
        .withKeyPair(<YOTI_KEY_FILE_PATH>)
        .withBaseUrl("https://api.yoti.com/idverify/v1")
        .withEndpoint("/sessions/<SESSION_ID>")
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

    sdkID := "<YOTI_CLIENT_SDK_ID>";
    key, _ := ioutil.ReadFile("<YOTI_KEY_FILE_PATH>")
    // Create session
    sessionRequest, _ := requests.SignedRequest{
        HTTPMethod: http.MethodGet,
        BaseURL:    "https://api.yoti.com/idverify/v1",
        Endpoint:   "/sessions/<SESSION_ID>",
        Params: map[string]string{
            "sdkId": sdkID,
        },
        Headers: map[string][]string{
            "Content-Type": {"application/json"},
            "Accept":       {"application/json"},
        },
    }.WithPemFile(key).Request()

    //get Yoti response
    sessionResponse, _ := http.DefaultClient.Do(sessionRequest)
{% /tab %}
{% tab language="csharp" %}
// Coming Soon
{% /tab %}
{% tab language="ruby" %}
// Coming Soon
{% /tab %}
{% /code %}

See below for an example response from the retrieve session endpoint.

### Example of a full session retrieval

{% code %}
{% tab language="json" %}
{
  "client_session_token_ttl": 599,
  "session_id": "<uuid>",
  "user_tracking_id": "<uuid>",
  "state": "COMPLETED",
  "client_session_token": "<uuid>",
  "resources": {
    "id_documents": [
      {
        "id": "<uuid>",
        "tasks": [
          {
            "type": "ID_DOCUMENT_TEXT_DATA_EXTRACTION",
            "id": "<uuid>",
            "state": "DONE",
            "created": "<yyyy-mm-ddThh:mm:ssZ>",
            "last_updated": "<yyyy-mm-ddThh:mm:ssZ>",
            "generated_checks": [],
            "generated_media": [
              {
                "id": "<uuid>",
                "type": "JSON"
              }
            ]
          }
        ],
        "document_type": "DRIVING_LICENCE",
        "issuing_country": "GBR",
        "pages": [
          {
            "capture_method": "CAMERA",
            "media": {
              "id": "<uuid>",
              "type": "IMAGE",
              "created": "<yyyy-mm-ddThh:mm:ssZ>",
              "last_updated": "<yyyy-mm-ddThh:mm:ssZ>"
            }
          }
        ],
        "document_fields": {
          "media": {
            "id": "<uuid>",
            "type": "JSON",
            "created": "<yyyy-mm-ddThh:mm:ssZ>",
            "last_updated": "<yyyy-mm-ddThh:mm:ssZ>"
          }
        }
      }
    ],
    "liveness_capture": [
      {
        "id": "<uuid>",
        "tasks": [],
        "frames": [
          {
            "media": {
              "id": "<uuid>",
              "type": "IMAGE",
              "created": "<yyyy-mm-ddThh:mm:ssZ>",
              "last_updated": "<yyyy-mm-ddThh:mm:ssZ>"
            }
          },
          {
            "media": {
              "id": "<uuid>",
              "type": "IMAGE",
              "created": "<yyyy-mm-ddThh:mm:ssZ>",
              "last_updated": "<yyyy-mm-ddThh:mm:ssZ>"
            }
          },
          {
            "media": {
              "id": "<uuid>",
              "type": "IMAGE",
              "created": "<yyyy-mm-ddThh:mm:ssZ>",
              "last_updated": "<yyyy-mm-ddThh:mm:ssZ>"
            }
          },
          {},
          {},
          {},
          {}
        ],
        "liveness_type": "ZOOM",
        "facemap": {
          "media": {
            "id": "<uuid>",
            "type": "BINARY",
            "created": "<yyyy-mm-ddThh:mm:ssZ>",
            "last_updated": "<yyyy-mm-ddThh:mm:ssZ>"
          }
        }
      }
    ]
  },
  "checks": [
    {
      "id": "<uuid>",
      "type": "ID_DOCUMENT_AUTHENTICITY",
      "state": "DONE",
      "resources_used": [
        "<uuid>"
      ],
      "report": {
        "recommendation": {
          "value": "APPROVE"
        },
        "breakdown": [
          {
            "sub_check": "data_in_correct_position",
            "result": "PASS",
            "details": []
          },
          {
            "sub_check": "document_in_date",
            "result": "PASS",
            "details": []
          },
          {
            "sub_check": "expected_data_present",
            "result": "PASS",
            "details": []
          },
          {
            "sub_check": "fraud_list_check",
            "result": "PASS",
            "details": []
          },
          {
            "sub_check": "hologram",
            "result": "PASS",
            "details": []
          },
          {
            "sub_check": "hologram_movement",
            "result": "PASS",
            "details": []
          },
          {
            "sub_check": "no_sign_of_tampering",
            "result": "PASS",
            "details": []
          },
          {
            "sub_check": "other_security_features",
            "result": "PASS",
            "details": []
          },
          {
            "sub_check": "real_document",
            "result": "PASS",
            "details": []
          }
        ]
      },
      "created": "<yyyy-mm-ddThh:mm:ssZ>",
     "last_updated": "<yyyy-mm-ddThh:mm:ssZ>"

    },
    {
      "type": "LIVENESS",
      "id": "<uuid>",
      "state": "DONE",
      "resources_used": [
        "<uuid>"
      ],
      "generated_media": [],
      "report": {
        "recommendation": {
          "value": "APPROVE"
        },
        "breakdown": [
          {
            "sub_check": "liveness_auth",
            "result": "PASS",
            "details": []
          }
        ]
      },
      "created": "<yyyy-mm-ddThh:mm:ssZ>",
      "last_updated": "<yyyy-mm-ddThh:mm:ssZ>"
    },
    {
      "type": "ID_DOCUMENT_FACE_MATCH",
      "id": "<uuid>",
      "state": "DONE",
      "resources_used": [
          "<uuid>",
          "<uuid>"
      ],
      "generated_media": [],
      "report": {
          "recommendation": {
              "value": "APPROVE" // "REJECT"
          },
          "breakdown": [
              {
                  "sub_check": "manual_face_match",
                  "result": "PASS", // "FAIL"
                  "details": []
              },
              {
                  "sub_check": "ai_face_match",
                  "result": "PASS", // "FAIL"
                  "details": [
                      {
                          "name": "confidence_score",
                          "value": "1.00"
                      }
                  ]
              }
          ]
      },
      "created": "<yyyy-mm-ddThh:mm:ssZ>",
      "last_updated": "<yyyy-mm-ddThh:mm:ssZ>"
    }
  ]
}
{% /tab %}
{% /code %}

---

## Get Session Response Explained

## Retrieved State

Yoti will provide back the following information regarding the state of the session:

- The state of the session
- Session ID
- client_session_token_ttl - will be 0 if expired.
- user_tracking_id set by the relying business backend

{% code %}
{% tab language="json" %}
{
  "client_session_token_ttl" : 599,
  "session_id" : "<uuid>",
  "user_tracking_id" : "<uuid>",
  "state" : "ONGOING",
  "client_session_token" : "<uuid>",
}
{% /tab %}
{% /code %}

{% table %}
| State | Description | 
| ---- | ---- | 
| ONGOING | Yoti is still working on tasks and checks for the user's ID. | 
| COMPLETED | Yoti has completed checks and tasks. | 
| EXPIRED | Yoti could not complete the checks and tasks. | 
{% /table %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Jump to... 
    </div>
    <div class="alert-text">
        To find out how to create this session please head back to the create a session section.
    </div>
    <div class="alert-links"> 
        <a href="https://developers.yoti.com/yoti/generating-a-session">Create a session</a>
   </div>
</div>
{% /html %}

## Retrieved Checks

We provide back the following details for the checks:

- Type and unique ID
- Resources used
- State
- Report - containing a recommendation and a breakdown of the report.

{% table %}
| Response Topic | Response | Description | 
| ---- | ---- | ---- | 
| State | CREATED, READY, PENDING, INTERNAL_ERROR, DONE | The status of the check.\n\nIf subscribed you will receive a check completion notification when the check is move to a DONE state. | 
| Recommendation | APPROVE, REJECT, NOT_AVAILABLE | Yoti will provide you a recommendation based on the checks. | 
{% /table %}

### ID Document Authenticity

An example of an 'APPROVE' report is shown below, please use the language snippet to see examples of a  'REJECT' and 'NOT_AVAILABLE' report.

{% code %}
{% tab language="json" %}
// APPROVE REPORT. Navigate to the next tab for the rejected example.

"checks": [
      {
         "type": "ID_DOCUMENT_AUTHENTICITY",
         "id": "<uuid>",
         "state": "DONE",
         "resources_used": [
            "<uuid>"
         ],
         "generated_media": [],
         "report": {
            "recommendation": {
               "value": "APPROVE"
            },
         "breakdown": [
          {
            "sub_check": "data_in_correct_position",
            "result": "PASS",
            "details": []
          },
          {
            "sub_check": "document_in_date",
            "result": "PASS",
            "details": []
          },
          {
            "sub_check": "expected_data_present",
            "result": "PASS",
            "details": []
          },
          {
            "sub_check": "fraud_list_check",
            "result": "PASS",
            "details": []
          },
          {
            "sub_check": "hologram",
            "result": "PASS",
            "details": []
          },
          {
            "sub_check": "hologram_movement",
            "result": "PASS",
            "details": []
          },
          {
            "sub_check": "no_sign_of_tampering",
            "result": "PASS",
            "details": []
          },
          {
            "sub_check": "other_security_features",
            "result": "PASS",
            "details": []
          },
          {
            "sub_check": "real_document",
            "result": "PASS",
            "details": []
          }
        ]
         },
         "created": "<yyyy-mm-ddThh:mm:ssZ>",
         "last_updated": "<yyyy-mm-ddThh:mm:ssZ>"
      }
]
{% /tab %}
{% tab language="json" %}
// REJECT REPORT. Navigate to the next tab for the not available example.

"checks": [
   {
      "id" : "<uuid>",
      "type" : "ID_DOCUMENT_AUTHENTICITY",
      "state" : "DONE", 
      "resources_used" : [
		"<uuid>"
	  ],
      "report" : {
        "recommendation": {
          "value" : "REJECT",
          "reason" : "EXPIRED_DOCUMENT" 
        },
             "breakdown": [
          {
            "sub_check": "data_in_correct_position",
            "result": "PASS",
            "details": []
          },
          {
            "sub_check": "document_in_date",
            "result": "PASS",
            "details": []
          },
          {
            "sub_check": "expected_data_present",
            "result": "PASS",
            "details": []
          },
          {
            "sub_check": "hologram",
            "result": "FAIL",
            "details": []
          },
          {
            "sub_check": "hologram_movement",
            "result": "FAIL",
            "details": []
          },
          {
            "sub_check": "no_sign_of_tampering",
            "result": "FAIL",
            "details": []
          },
          {
            "sub_check": "other_security_features",
            "result": "PASS",
            "details": []
          },
          {
            "sub_check": "real_document",
            "result": "PASS",
            "details": []
          }
        ]
      },
      "created" : "<yyyy-mm-ddThh:mm:ssZ>",
      "last_updated" : "<yyyy-mm-ddThh:mm:ssZ>"
    }
  ]
{% /tab %}
{% tab language="json" %}
// NOT AVAILABLE REPORT.

"checks": [
 {
      "type" : "ID_DOCUMENT_AUTHENTICITY",
      "id" : "<uuid>",
      "state" : "DONE"
      "resources_used" : [
        "<uuid>"
      ],
      "report" : {
        "recommendation": {
          "value" : "NOT_AVAILABLE",
          "reason" : "PICTURE_TOO_DARK"
        },
        "breakdown": [
          {
            "sub_check": "issuing_authority_verification",
            "result": "PASS"
          }
        ]
      },
      "created" : "<yyyy-mm-ddThh:mm:ssZ>",
      "last_updated" : "<yyyy-mm-ddThh:mm:ssZ>"
    }
]
{% /tab %}
{% /code %}

If Yoti responds with the REJECT recommendation there will be a rejection reason alongside this. 

- Missing Hologram
- Document Copy
- Tampered
- Not genuine 

If Yoti responds with the NOT AVAILABLE recommendation, this means we were unable to carry out the check. A recovery suggestion will be provided to give the user an idea of what can be done to correct the issue causing the not available recommendation. A full list of possible reasons for this can be found below:

{% table %}
| Yoti Response | Description | Recommendation | 
| ---- | ---- | ---- | 
| PHOTO_OVEREXPOSED | The photo is overexposed | NOT_AVAILABLE | 
| PHOTO_TOO_DARK | The photo is dark | NOT_AVAILABLE | 
| PHOTO_TOO_BLURRY | The photo is blurry | NOT_AVAILABLE | 
| DOCUMENT_TOO_DAMAGED | Document is too damaged (at the point we cannot check) | NOT_AVAILABLE | 
| GLARE_OBSTRUCTION | The photo has a glare | NOT_AVAILABLE | 
| OBJECT_OBSTRUCTION | Object in the way | NOT_AVAILABLE | 
| UNABLE_TO_LOAD | Unable to load file | NOT_AVAILABLE | 
| PARTIAL_PHOTO | The photo is partially taken | NOT_AVAILABLE | 
| IMAGE_RESOLUTION_TOO_LOW | The image resolution is too low | NOT_AVAILABLE | 
| COUNTRY_NOT_SUPPORTED | The country is not supported | NOT_AVAILABLE | 
| DOCUMENT_NOT_SUPPORTED | Yoti does not support this document | NOT_AVAILABLE | 
| INCORRECT_DOCUMENT_TYPE | The document type is incorrect | NOT_AVAILABLE | 
| INCORRECT_MRZ | MRZ on passport is incorrect | NOT_AVAILABLE | 
| DOCUMENT_VERSION_NOT_SUPPORTED | Yoti does not support this document template | NOT_AVAILABLE | 
| MISSING_DOCUMENT_SIDE | The full document was not sent | NOT_AVAILABLE | 
| BLACK_AND_WHITE_IMAGE | Black and white photo | NOT_AVAILABLE | 
| MISUSE | The photo has been misused | NOT_AVAILABLE | 
| INVALID | The photo is not a valid photo | NOT_AVAILABLE | 
| DOCUMENT_COPY | The photo has been photocopied | REJECT | 
| NO_HOLOGRAM_MOVEMENT | There is no hologram movement detected | REJECT | 
| TAMPERED | The photo seems to be tampered with | REJECT | 
| MISSING_HOLOGRAM | There is no hologram on the photo | REJECT | 
| OTHER_SECURITY_FEATURES | Expected data present or data in correct position failed. This will vary document to document, an example of features checked:\n\nMicroprint, watermarks, optically variable ink, presence of fingerprint / other notable (non-text) features and any visible embossing / engraving | REJECT | 
| EXPIRED_DOCUMENT | The document has expired | REJECT | 
| FRAUD_LIST_MATCH | The fraud match list check failed | REJECT | 
{% /table %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Jump to... 
    </div>
    <div class="alert-text">
        To find out how to create this session please head back to the create a session section.
    </div>
    <div class="alert-links"> 
        <a href="https://developers.yoti.com/yoti/generating-a-session#2-checks-configuration">Checks configuration</a>
   </div>
</div>
{% /html %}

### Liveness

Liveness checks can be retried if failed, depending on specified limited set when generating the session. Each try will generate a new report in the JSON response. The check will either be approved or rejected based on the result of the liveness check which is a pass/fail result.

{% code %}
{% tab language="json" %}
"checks": [
  {
         "type": "LIVENESS",
         "id": "<uuid>",
         "state": "DONE",
         "resources_used": [
            "<uuid>"
         ],
         "generated_media": [],
         "report": {
            "recommendation": {
               "value": "APPROVE" //"REJECT
            },
            "breakdown": [
               {
                  "sub_check": "liveness_auth",
                  "result": "PASS", //"FAIL"
                  "details": []
               }
            ]
         },
         "created": "<yyyy-mm-ddThh:mm:ssZ>",
         "last_updated": "<yyyy-mm-ddThh:mm:ssZ>"
      }
]
{% /tab %}
{% /code %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Jump to... 
    </div>
    <div class="alert-text">
        To find out how to create this session please head back to the create a session section.
    </div>
    <div class="alert-links"> 
        <a href="https://developers.yoti.com/yoti/generating-a-session#2-checks-configuration">Checks configuration</a>
   </div>
</div>
{% /html %}

### ID Document Face Match

An ID_DOCUMENT_FACE_MATCH check will return a report containing an overall recommendation, and the breakdown of sub checks performed (the result of the machine (AI) face match, and/or the manual face match, according to which were performed).

If an AI face match is performed, a pass/fail result is returned, along with a confidence score (between 0 and 1) depending on how successful the match is, Yoti offers a PASS score if the confidence score is over 0.7.

A manual check will be either a pass or a fail.

The face match check will give a recommendation based on these as either APPROVE or REJECT.

{% code %}
{% tab language="json" %}
{
    "type": "ID_DOCUMENT_FACE_MATCH",
    "id": "<uuid>",
    "state": "DONE",
    "resources_used": [
        "<uuid>",
        "<uuid>"
    ],
    "generated_media": [],
    "report": {
        "recommendation": {
            "value": "APPROVE" // "REJECT"
        },
        "breakdown": [
            {
                "sub_check": "manual_face_match",
                "result": "PASS", // "FAIL"
                "details": []
            },
            {
                "sub_check": "ai_face_match",
                "result": "PASS", // "FAIL"
                "details": [
                    {
                        "name": "confidence_score",
                        "value": "1.00"
                    }
                ]
            }
        ]
    },
    "created": "<yyyy-mm-ddThh:mm:ssZ>",
    "last_updated": "<yyyy-mm-ddThh:mm:ssZ>"
}
{% /tab %}
{% /code %}

The below responses are only for manual checks:

{% table %}
| Yoti Response | Description | Recommendation | 
| ---- | ---- | ---- | 
| PHOTO_OVEREXPOSED | The photo is overexposed | NOT_AVAILABLE | 
| PHOTO_TOO_DARK | The photo is dark | NOT_AVAILABLE | 
| PHOTO_TOO_BLURRY | The photo is blurry | NOT_AVAILABLE | 
| FACE_NOT_FOUND | No face detected | NOT_AVAILABLE | 
| GLARE_OBSTRUCTION | The photo has a glare | NOT_AVAILABLE | 
| OBJECT_OBSTRUCTION | Object in the way | NOT_AVAILABLE | 
| DOCUMENT_NOT_FOUND | No photo detected | NOT_AVAILABLE | 
| PARTIAL_PHOTO | Only part of the photo was shown | NOT_AVAILABLE | 
| FACE_PHOTO_LOW_RESOLUTION | The photo had low resolution | NOT_AVAILABLE | 
| MISUSE | The photo is misused | NOT_AVAILABLE | 
| INVALID | The photo is invalid | NOT_AVAILABLE | 
| FACE_NOT_GENUINE | The face shown is not genuine | REJECT | 
| LARGE_AGE_GAP | The age gap looks unrealistic | REJECT | 
| DOCUMENT_COPY | The document has been photocopied | REJECT | 
| TAMPERED | The photo has been tampered | REJECT | 
| PHOTO_OF_MASK | The user is wearing a mask | REJECT | 
| PHOTO_OF_PHOTO | The photo has been photocopied | REJECT | 
| DIFFERENT_PERSON | Different person is detected from ID. | REJECT | 
{% /table %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Jump to... 
    </div>
    <div class="alert-text">
        To find out how to create this session please head back to the create a session section.
    </div>
    <div class="alert-links"> 
        <a href="https://developers.yoti.com/yoti/generating-a-session#2-checks-configuration">Checks configuration</a>
   </div>
</div>
{% /html %}

### ID Document Text Data Check

This check is generated by the ID Document Text Data Extraction task (see below). This will only be generated if the "manual_check" is set to ALWAYS or FALLBACK. This check is performed by our security centre to manually check that the automatic text data extraction was correct or to perform the extraction if the automatic task fails.

{% code %}
{% tab language="json" %}
{
            "type": "ID_DOCUMENT_TEXT_DATA_CHECK",
            "id": "<UUID>",
            "state": "DONE",
            "resources_used": [
                "<UUID>"
            ],
            "generated_media": [
                {
                    "id": "<UUID>",
                    "type": "JSON"
                }
            ],
            "report": {
                "recommendation": {
                    "value": "APPROVE"
                },
                "breakdown": [
                    {
                        "sub_check": "text_data_readable",
                        "result": "PASS",
                        "details": []
                    }
                ]
            },
            "created": "YYYY-MM-DDTHH:MM:SSZ",
            "last_updated": "YYYY-MM-DDTHH:MM:SSZ"
        }
{% /tab %}
{% /code %}

The ID Document Text Data check will give a recommendation either APPROVE or REJECT. The recommendation will come with a breakdown which will contain the subcheck text_data_readable which will either be a PASS or a FAIL. 

If this check is successfully approved then the generated media array will contain the extracted text media ID, which can be used to retrieve the JSON object with the extracted data. 

This media will replace the "document_fields" media in the resources. Details of this can be found here: [retrieved resources](https://developers.yoti.com/yoti/session-and-media-retrieval#retrieved-resources).

## Retrieved Tasks

### ID Document Text Data Extraction

An ID_DOCUMENT_TEXT_DATA task will return a state and a JSON. See [Retrieved resources](https://developers.yoti.com/yoti/session-and-media-retrieval#retrieved-resources) section for more detail.

{% code %}
{% tab language="json" %}
"tasks": [
          {
            "type": "ID_DOCUMENT_TEXT_DATA_EXTRACTION",
            "id": "<uuid>",
            "state": "DONE",
            "created": "<yyyy-mm-ddThh:mm:ssZ>",
            "last_updated": "<yyyy-mm-ddThh:mm:ssZ>",
            "generated_checks": [],
            "generated_media": [
              {
                "id": "<uuid>",
                "type": "JSON"
              }
            ]
          }
        ],
{% /tab %}
{% /code %}

If Yoti responds with the NOT AVAILABLE recommendation, this means we were unable to carry out the check. A recovery suggestion will be provided to give the user an idea of what can be done to correct the issue causing the not available recommendation. A full list of possible reasons for this can be found below:

{% table %}
| Yoti response | Description | Recommendation | 
| ---- | ---- | ---- | 
| PHOTO_OVEREXPOSED | The photo is overexposed | NOT_AVAILABLE | 
| PHOTO_TOO_DARK | The photo is dark | NOT_AVAILABLE | 
| PHOTO_TOO_BLURRY | The photo is blurry | NOT_AVAILABLE | 
| DOCUMENT_TOO_DAMAGED | Document is too damaged (at the point we cannot check) | NOT_AVAILABLE | 
| GLARE_OBSTRUCTION | The photo has a glare | NOT_AVAILABLE | 
| OBJECT_OBSTRUCTION | Object in the way | NOT_AVAILABLE | 
| UNABLE_TO_LOAD | Unable to load file | NOT_AVAILABLE | 
| PARTIAL_PHOTO | The photo is partially taken | NOT_AVAILABLE | 
| IMAGE_RESOLUTION_TOO_LOW | The image resolution is too low | NOT_AVAILABLE | 
| COUNTRY_NOT_SUPPORTED | The country is not supported | NOT_AVAILABLE | 
| DOCUMENT_NOT_SUPPORTED | Yoti does not support this document | NOT_AVAILABLE | 
| INCORRECT_DOCUMENT_TYPE | The document type is incorrect | NOT_AVAILABLE | 
| INCORRECT_MRZ | MRZ on passport is incorrect | NOT_AVAILABLE | 
| DOCUMENT_VERSION_NOT_SUPPORTED | Yoti does not support this document template | NOT_AVAILABLE | 
| MISSING_DOCUMENT_SIDE | The full document was not sent | NOT_AVAILABLE | 
| BLACK_AND_WHITE_IMAGE | Black and white photo | NOT_AVAILABLE | 
| MISUSE | The photo has been misused | NOT_AVAILABLE | 
| INVALID | The photo is not a valid photo | NOT_AVAILABLE | 
{% /table %}

{% html %}
<div class="alert-GTK">

    <div class="alert-title" id="GTK">

        Jump to... 

    </div>

    <div class="alert-text">

        To find out how to create this session please head back to the create a session section.

    </div>

    <div class="alert-links"> 

        <a href="https://developers.yoti.com/yoti/generating-a-session#4-tasks-configuration">Task configuration</a>

   </div>

</div>
{% /html %}

---

## Get Media Request

For security reasons, we do not include personally identifiable information (PII) within the standard response to a session retrieval request. Rather, we provide pointers to 'media' associated with the session, which are stored and can be retrieved separately. Examples of media are: document images, structured fields extracted from a document, face images, and so on.

Using the media IDs contained within the response to a GET session request, you can retrieve the associated media using the session ID and media ID.

Please note the:

- withMethod should be set to GET 
- The withEndpoint should be set to /sessions/SESSIONID/media/MEDIA ID/content where SESSION_ID should be replaced with the SESSION_ID obtained at Create a Session.
- MEDIA_ID should be replaced with the MEDIA_ ID obtained at session retrieval.

{% code %}
{% tab language="javascript" %}
const { RequestBuilder, Payload } = require("yoti");

const request = new RequestBuilder()
  .withBaseUrl("https://api.yoti.com/idverify/v1")
  .withPemFilePath("<YOTI_KEY_FILE_PATH>")
  .withEndpoint(`/sessions/<SESSION_ID>/media/<MEDIA_ID>/content`)
  .withMethod("GET")
  .withQueryParam("sdkId", "<YOTI_CLIENT_SDK_ID>")
  .build();

//get Yoti response
const response = request.execute();
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\Http\RequestBuilder;
use Yoti\Http\Payload;

$request = (new RequestBuilder())
    ->withBaseUrl('https://api.yoti.com/idverify/v1')
    ->withPemFilePath('<YOTI_KEY_FILE_PATH>')
    ->withEndpoint('/sessions/<SESSION_ID>/media/<MEDIA_ID>/content')
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


def get_media():

    signed_request = (
        SignedRequest
        .builder()
        .with_pem_file("<YOTI_KEY_FILE_PATH>")
        .with_base_url("https://api.yoti.com/idverify/v1")
        .with_endpoint("/sessions/<SESSION_ID>/media/<MEDIA_ID>/content")
        .with_http_method("GET")
        .with_param("sdkId", "<YOTI_CLIENT_SDK_ID>")
        .build()
    )

    response = signed_request.execute()
    response_payload = json.loads(response.text)

//get Yoti response
print(get_media())
{% /tab %}
{% tab language="java" %}
byte[] payload = ...

try {
    SignedRequest signedRequest = SignedRequestBuilder.newInstance()
        .withKeyPair(<YOTI_KEY_FILE_PATH>)
        .withBaseUrl("https://api.yoti.com/idverify/v1")
        .withEndpoint("/sessions/<SESSION_ID>/media/<MEDIA_ID>/content")
        .withHttpMethod("GET")
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

    sdkID := "<YOTI_CLIENT_SDK_ID>";
    key, _ := ioutil.ReadFile("<YOTI_KEY_FILE_PATH>")
    // Create session
    sessionRequest, _ := requests.SignedRequest{
        HTTPMethod: http.MethodGet,
        BaseURL:    "https://api.yoti.com/idverify/v1",
        Endpoint:   "/sessions/<SESSION_ID>/media/<MEDIA_ID>/content",
        Params: map[string]string{
            "sdkId": sdkID,
        },
        Headers: map[string][]string{
            "Content-Type": {"application/json"},
            "Accept":       {"application/json"},
        },
    }.WithPemFile(key).Request()

    //get Yoti response
    sessionResponse, _ := http.DefaultClient.Do(sessionRequest)
{% /tab %}
{% tab language="csharp" %}
// Coming Soon
{% /tab %}
{% tab language="ruby" %}
# Coming Soon
{% /tab %}
{% /code %}

The response will be returned as a JSON object and image media will be returned as a buffer string.

{% html %}
<div class="alert-know">
    <div class="alert-title" id="know">
        Knowledge base
    </div>
    <div class="alert-text">
        Retrieving media for Aadhaar is slightly different, for more information see the section linked. 
    </div>
    <div class="alert-links"> 
       <a target="_self" href="https://developers.yoti.com/yoti/knowledge-base-docscan#aadhaar">
           Aadhaar masking
       </a> 
    </div>
</div>
{% /html %}

## Session & Media Deletion

It is possible to delete a session or session media before the defined retention period (ttl) is over. However, this can only be done once the session is completed. Deleting the session will also delete all media from that session. Deleting a media object will delete only that specific object, leaving the rest of the session untouched.

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know... 
    </div>
    <div class="alert-text">
Please note that the session, along with all associated resources and media, will be automatically deleted once the retention period (defined in the session creation) is reached.
    </div>
</div>
{% /html %}

For more information about DELETE requests see our [API references](https://yoti.com/api-reference#yoti-doc-scan-delete-a-session)

### Session Deletion

- withMethod should be set to `DELETE`
- The `withEndpoint` should be set to `/sessions/SESSION_ID` where `SESSION_ID` should be replaced with the `SESSION_ID` obtained in [auto$](/yoti/generating-a-session#example-response-payload).

{% code %}
{% tab language="javascript" %}
const { RequestBuilder, Payload } = require("yoti");

const request = new RequestBuilder()
  .withBaseUrl("https://api.yoti.com/idverify/v1")
  .withPemFilePath("<YOTI_KEY_FILE_PATH>")
  .withEndpoint(`/sessions/<SESSION_ID>`)
  .withMethod("DELETE")
  .withQueryParam("sdkId", "<YOTI_CLIENT_SDK_ID>")
  .build();

//get Yoti response
const response = request.execute();
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\Http\RequestBuilder;
use Yoti\Http\Payload;

$request = (new RequestBuilder())
    ->withBaseUrl('https://api.yoti.com/idverify/v1')
    ->withPemFilePath('<YOTI_KEY_FILE_PATH>')
    ->withEndpoint('/sessions/<SESSION_ID>')
    ->withMethod('DELETE')
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
        .with_base_url("https://api.yoti.com/idverify/v1")
        .with_endpoint("/sessions/<SESSION_ID>")
        .with_http_method("DELETE")
        .with_param("sdkId", "<YOTI_CLIENT_SDK_ID>")
        .build()
    )

    response = signed_request.execute()
    response_payload = json.loads(response.text)

//get Yoti response
print(generate_session())
{% /tab %}
{% tab language="java" %}
byte[] payload = ...

try {
    SignedRequest signedRequest = SignedRequestBuilder.newInstance()
        .withKeyPair(<YOTI_KEY_FILE_PATH>)
        .withBaseUrl("https://api.yoti.com/idverify/v1")
        .withEndpoint("/sessions/<SESSION_ID>")
        .withHttpMethod("DELETE")
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

    sdkID := "<YOTI_CLIENT_SDK_ID>";
    key, _ := ioutil.ReadFile("<YOTI_KEY_FILE_PATH>")
    // Create session
    sessionRequest, _ := requests.SignedRequest{
        HTTPMethod: http.MethodDelete,
        BaseURL:    "https://api.yoti.com/idverify/v1",
        Endpoint:   "/sessions/<SESSION_ID>",
        Params: map[string]string{
            "sdkId": sdkID,
        },
        Headers: map[string][]string{
            "Content-Type": {"application/json"},
            "Accept":       {"application/json"},
        },
    }.WithPemFile(key).Request()

    //get Yoti response
    sessionResponse, _ := http.DefaultClient.Do(sessionRequest)
{% /tab %}
{% tab language="csharp" %}
// Coming Soon
{% /tab %}
{% tab language="ruby" %}
// Coming Soon
{% /tab %}
{% /code %}

### Media Deletion

Please note the:

- withMethod should be set to `DELETE`
- The `withEndpoint` should be set to `/sessions/SESSION_ID/media/MEDIA_ID/content` where `SESSION_ID` should be replaced with the `SESSION_ID` obtained in [auto$](/yoti/generating-a-session#example-response-payload) and `MEDIA_ID` should be replaced with the `MEDIA_ID` obtained in the [get session request](/yoti/session-and-media-retrieval#get-session-request).

{% code %}
{% tab language="javascript" %}
const { RequestBuilder, Payload } = require("yoti");

const request = new RequestBuilder()
  .withBaseUrl("https://api.yoti.com/idverify/v1")
  .withPemFilePath("<YOTI_KEY_FILE_PATH>")
  .withEndpoint(`/sessions/<SESSION_ID>/media/<MEDIA_ID>/content`)
  .withMethod("DELETE")
  .withQueryParam("sdkId", "<YOTI_CLIENT_SDK_ID>")
  .build();

//get Yoti response
const response = request.execute();
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\Http\RequestBuilder;
use Yoti\Http\Payload;

$request = (new RequestBuilder())
    ->withBaseUrl('https://api.yoti.com/idverify/v1')
    ->withPemFilePath('<YOTI_KEY_FILE_PATH>')
    ->withEndpoint('/sessions/<SESSION_ID>/media/<MEDIA_ID>/content')
    ->withMethod('DELETE')
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


def delete_media():

    signed_request = (
        SignedRequest
        .builder()
        .with_pem_file("<YOTI_KEY_FILE_PATH>")
        .with_base_url("https://api.yoti.com/idverify/v1")
        .with_endpoint("/sessions/<SESSION_ID>/media/<MEDIA_ID>/content")
        .with_http_method("DELETE")
        .with_param("sdkId", "<YOTI_CLIENT_SDK_ID>")
        .build()
    )

    response = signed_request.execute()
    response_payload = json.loads(response.text)

//get Yoti response
print(delete_media())
{% /tab %}
{% tab language="java" %}
byte[] payload = ...

try {
    SignedRequest signedRequest = SignedRequestBuilder.newInstance()
        .withKeyPair(<YOTI_KEY_FILE_PATH>)
        .withBaseUrl("https://api.yoti.com/idverify/v1")
        .withEndpoint("/sessions/<SESSION_ID>/media/<MEDIA_ID>/content")
        .withHttpMethod("DELETE")
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

    sdkID := "<YOTI_CLIENT_SDK_ID>";
    key, _ := ioutil.ReadFile("<YOTI_KEY_FILE_PATH>")
    // Create session
    sessionRequest, _ := requests.SignedRequest{
        HTTPMethod: http.MethodDelete,
        BaseURL:    "https://api.yoti.com/idverify/v1",
        Endpoint:   "/sessions/<SESSION_ID>/media/<MEDIA_ID>/content",
        Params: map[string]string{
            "sdkId": sdkID,
        },
        Headers: map[string][]string{
            "Content-Type": {"application/json"},
            "Accept":       {"application/json"},
        },
    }.WithPemFile(key).Request()

    //get Yoti response
    sessionResponse, _ := http.DefaultClient.Do(sessionRequest)
{% /tab %}
{% tab language="csharp" %}
// Coming Soon
{% /tab %}
{% tab language="ruby" %}
# Coming Soon
{% /tab %}
{% /code %}

---

## Retrieved Resources

The resources retrieval returns back details and resources of the id document and liveness check depending on what tasks and checks you request.

### ID Document Resources

When the session is retrieved there will be details regarding the ID document and associated tasks.

{% code %}
{% tab language="json" %}
"id_documents": [
      {
        "id": "<uuid>",
        "tasks": [
          {
            "type": "ID_DOCUMENT_TEXT_DATA_EXTRACTION",
            "id": "<uuid>",
            "state": "DONE",
            "created": "<yyyy-mm-ddThh:mm:ssZ>",
            "last_updated": "<yyyy-mm-ddThh:mm:ssZ>",
            "generated_checks": [],
            "generated_media": [
              {
                "id": "<uuid>",
                "type": "JSON"
              }
            ]
          }
        ],
        "document_type": "DRIVING_LICENCE",
        "issuing_country": "GBR",
        "pages": [
          {
            "capture_method": "CAMERA",
            "media": {
              "id": "<uuid>",
              "type": "IMAGE",
              "created": "<yyyy-mm-ddThh:mm:ssZ>",
              "last_updated": "<yyyy-mm-ddThh:mm:ssZ>"
            }
          }
        ],
        "document_fields": {
          "media": {
            "id": "<uuid>",
            "type": "JSON",
            "created": "<yyyy-mm-ddThh:mm:ssZ>",
            "last_updated": "<yyyy-mm-ddThh:mm:ssZ>"
          }
        }
      }
    ]
{% /tab %}
{% /code %}

{% table %}
| Response Topic | Example Response | Description | 
| ---- | ---- | ---- | 
| id | 89eab361-7d91-42c5-a833-06a212cwfdb2 | ID of the document. In UUID form. | 
| tasks | N/A | Information on any tasks requested. | 
| document_type | DRIVING LICENSE | Type of document scanned - this is selected by the user before uploading their document. We support, passports, driving licenses and citizen cards of select countries. For a list of supported documents see [here](https://yoti.zendesk.com/hc/en-us/articles/360002886594-What-ID-documents-do-you-currently-support-). | 
| issuing_country | GBR | Issuing country of the document - this is selected by the user before uploading their document. Will be in 3 letter ISO country code format. | 
| pages | N/A | Pages of document - will be multiple if user is required to upload a front and back image of their document. Generated media and capture_method are provided here. | 
| document_fields | N/A | If the task ID_DOCUMENT_TEXT_DATA_EXTRACTION is requested then the generated media containing the extracted data will be presented here. | 
{% /table %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Jump to... 
    </div>
    <div class="alert-text">
        To find our how to create this session please head back to the task section.
    </div>
    <div class="alert-links"> 
        <a href="https://developers.yoti.com/yoti/generating-a-session#3-tasks-configuration">Task Configuration</a>
   </div>
</div>
{% /html %}

### Liveness Capture Resources

If a liveness check is requested then it will generate resources.

{% code %}
{% tab language="json" %}
"liveness_capture": [
        {
          "id": "<uuid>",
          "tasks": [],
          "frames": [
            {
              "media": {
                "id": "<uuid>",
                "type": "IMAGE",
                "created": "<yyyy-mm-ddThh:mm:ssZ>",
                "last_updated": "<yyyy-mm-ddThh:mm:ssZ>"
              }
            },
            {
              "media": {
                "id": "<uuid>",
                "type": "IMAGE",
                "created": "<yyyy-mm-ddThh:mm:ssZ>",
                "last_updated": "<yyyy-mm-ddThh:mm:ssZ>"
              }
            },
            {
              "media": {
                "id": "<uuid>",
                "type": "IMAGE",
                "created": "<yyyy-mm-ddThh:mm:ssZ>",
                "last_updated": "<yyyy-mm-ddThh:mm:ssZ>"
              }
            },
            {},
            {},
            {},
            {}
          ],
          "liveness_type": "ZOOM",
          "facemap": {
            "media": {
              "id": "<uuid>",
              "type": "BINARY",
              "created": "<yyyy-mm-ddThh:mm:ssZ>",
              "last_updated": "<yyyy-mm-ddThh:mm:ssZ>"
            }
          }
        }
      ]
{% /tab %}
{% /code %}

{% table %}
| Response Topic | Description | 
| ---- | ---- | 
| id | A unique ID in UUID form. | 
| tasks | Any tasks performed on the liveness capture. | 
| frames | Media generated during the liveness check. | 
| liveness_type | Type of liveness. | 
| facemap | If a facemap is generated the media data is provided here. | 
{% /table %}

## Document fields explained

This is the JSON version of the user.

Explanation of the address format can be found [here](/yoti/knowledge-base-hub#address-attributes)

{% code %}
{% tab language="json" %}
{
  // FullName contains given names and family name.
  "full_name" : "Jon Jim Foo",
  // DateOfBirth is the date of birth in the form yyyy-mm-dd.
  "date_of_birth" : "2000-12-01",
  // Nationality is the nationality expressed as
  // an ISO/ICAO alpha-3 country code.
  "nationality" : "GBR",
  // GivenNames contains first and middle names.
  "given_names" : "Jon Jim",
  // FirstName is the first name only.
  "first_name" : "Jon",
  // MiddleName is the middle name only.
  "middle_name" : "Jim",
  // FamilyName is the family name.
  "family_name" : "Foo",
  // PlaceOfBirth is the place of birth,
  // it may contain a country name or a city name or both.
  "place_of_birth" : "London",
  // CountryOfBirth is the country of birth,
  // as an ISO/ICAO alpha-3 country code.
  "country_of_birth" : "GBR",
  // Gender is the gender and can be any of the
  // following values:
  // "MALE", "FEMALE", "TRANSGENDER" or "OTHER".
  "gender" : "MALE",
  // NamePrefix is the name prefix, for example a title.
  "name_prefix" : "Dr",
  // NameSuffix is the name suffix.
  "name_suffix" : "Jr",
  // FirstNameAlias is the alias for the first name.
  "first_name_alias" : "",
  // MiddleNameAlias is the alias for the middle name.
  "middle_name_alias" : "",
  // FamilyNameAlias is the alias for the family name.
  "family_name_alias" : "",
  // Weight is the weight as displayed on the document.
  // Should contain weight and the unit.
  "weight" : "",
  // Height is the height as displayed on the document.
  // Should contain height and the unit.
  "height" : "",
  // EyeColor is the eye colour as displayed on the document.
  "eye_color" : "",
  "structured_postal_address" : {},
  // DocumentType specifies the type of document.
  // Values: "DRIVING_LICENCE", "PASSPORT", "NATIONAL_ID"
  "document_type" : "DRIVING_LICENCE",
  // IssuingCountry is the country the document was issued in.
  // Defined as an ISO/ICAO alpha-3 country code.
  "issuing_country" : "GBR",
  // DocumentNumber is the document number.
  "document_number" : "EF1523467",
  // ExpirationDate defines the date of expire for the document
  // in the form yyyy-mm-dd.
  "expiration_date" : "2030-12-01",
  // DateOfIssue is the date of issue of the document
  // in the form yyyy-mm-dd.
  "date_of_issue" : "2001-12-01",
  // IssuingAuthority is the authority that issued the document.
  "issuing_authority" : "DVLA",
  // MRZ provides the content of the machine readable zone,
  // as displayed on the document.
  "mrz" : {
	"type" : 1, // 1=TD1, 2=TD3,
	"line1" : "<<<<<...",
	"line2" : "<<<<<...",
	"line3" : "<<<<<..."
	}
}
{% /tab %}
{% /code %}