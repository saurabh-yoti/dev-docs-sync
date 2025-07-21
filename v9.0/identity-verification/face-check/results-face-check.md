---
type: page
title: Retrieve results
listed: true
slug: results-face-check
description: 
index_title: Retrieve results
hidden: 
keywords: 
tags: 
---

## Face Check Results

The response will detail the session results information including check and task completion status, resource and media data, along with the associated media identifiers.

{% code %}
{% tab language="javascript" title="Node.js" %}
const { RequestBuilder, Payload } = require("yoti");

const request = new RequestBuilder()
  .withBaseUrl("https://api.yoti.com/idverify/v1")
  .withPemFilePath("<YOTI_KEY_FILE_PATH>") // file path to PEM file
  .withEndpoint("/sessions/<session_id>")
  .withMethod("GET")
  .withQueryParam("sdkId", "<YOTI_CLIENT_SDK_ID>")
  .build();

// get Yoti response
const response = await request.execute();
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

	# get Yoti response
    response = signed_request.execute()
    response_payload = json.loads(response.text)
{% /tab %}
{% tab language="java" %}
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

key, _ := ioutil.ReadFile("<YOTI_KEY_FILE_PATH>")

request, _ := requests.SignedRequest{
    HTTPMethod: http.MethodGet,
    BaseURL:    "https://api.yoti.com/idverify/v1",
    Endpoint:   "/sessions/<SESSION_ID>",
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

{% code %}
{% tab language="http" %}
GET https://api.yoti.com/idverify/v1/sessions/<SESSION_ID>
{% /tab %}
{% /code %}

When the above endpoint is hit you will receive the results of all checks configured in the session, including the familiar face search check. The response will follow the below format.

#### Response body

{% code %}
{% tab language="json" title="Full JSON" %}
{
    "client_session_token_ttl": 0,
    "session_id": "7938ac1e-0a4a-49b7-953f-08cfa764358f",
    "state": "COMPLETED",
    "resources": {
        "id_documents": [
            {
                "id": "02ffe8d4-5f4a-4aaa-a046-21593944e05f",
                "tasks": [
                    {
                        "type": "ID_DOCUMENT_TEXT_DATA_EXTRACTION",
                        "id": "1890a33a-1c9e-47f5-88d1-52ff06854e76",
                        "state": "DONE",
                        "created": "2025-06-04T08:49:53Z",
                        "last_updated": "2025-06-04T08:50:39Z",
                        "generated_checks": [],
                        "generated_media": [
                            {
                                "id": "3943b63a-acf6-4860-9984-b73616007046",
                                "type": "JSON"
                            }
                        ],
                        "recommendation": {
                            "value": "PROGRESS"
                        }
                    }
                ],
                "source": {
                    "type": "END_USER"
                },
                "created_at": "2025-06-04T08:49:53Z",
                "last_updated": "2025-06-04T08:50:39Z",
                "document_type": "PASSPORT",
                "issuing_country": "GBR",
                "pages": [
                    {
                        "capture_method": "CAMERA",
                        "media": {
                            "id": "fa453d19-32d1-467d-adb9-44ed2dcb6783",
                            "type": "IMAGE",
                            "created": "2025-06-04T08:50:30Z",
                            "last_updated": "2025-06-04T08:50:30Z"
                        },
                        "frames": [
                            {
                                "media": {
                                    "id": "29a8110f-3eb6-496a-a2ee-5fc56a9758ac",
                                    "type": "IMAGE",
                                    "created": "2025-06-04T08:50:32Z",
                                    "last_updated": "2025-06-04T08:50:32Z"
                                }
                            },
                            {
                                "media": {
                                    "id": "5db33604-3616-457e-80fe-e44af11df8ba",
                                    "type": "IMAGE",
                                    "created": "2025-06-04T08:50:32Z",
                                    "last_updated": "2025-06-04T08:50:32Z"
                                }
                            },
                            {
                                "media": {
                                    "id": "aefacec4-087b-41e0-ab2c-567fbad9d343",
                                    "type": "IMAGE",
                                    "created": "2025-06-04T08:50:32Z",
                                    "last_updated": "2025-06-04T08:50:32Z"
                                }
                            }
                        ]
                    }
                ],
                "document_fields": {
                    "media": {
                        "id": "3943b63a-acf6-4860-9984-b73616007046",
                        "type": "JSON",
                        "created": "2025-06-04T08:50:39Z",
                        "last_updated": "2025-06-04T08:50:39Z"
                    }
                },
                "document_id_photo": {
                    "media": {
                        "id": "a106c265-80d3-4998-8a77-3ccbc3f29ccd",
                        "type": "IMAGE",
                        "created": "2025-06-04T08:50:39Z",
                        "last_updated": "2025-06-04T08:50:39Z"
                    }
                }
            }
        ],
        "supplementary_documents": [],
        "liveness_capture": [
            {
                "id": "e3d4ce28-4291-4dd4-a650-33fd5c3b0e0f",
                "tasks": [],
                "source": {
                    "type": "END_USER"
                },
                "created_at": "2025-06-04T08:50:45Z",
                "last_updated": "2025-06-04T08:51:00Z",
                "image": {
                    "media": {
                        "id": "d12ad6f6-2d1e-4b0d-9650-a153478c7d6e",
                        "type": "IMAGE",
                        "created": "2025-06-04T08:51:00Z",
                        "last_updated": "2025-06-04T08:51:00Z"
                    }
                },
                "liveness_type": "STATIC"
            }
        ],
        "face_capture": [],
        "applicant_profiles": []
    },
    "checks": [
        {
            "type": "LIVENESS",
            "id": "b1e04326-6bba-4a4e-97c5-7191d60c17d9",
            "state": "DONE",
            "resources_used": [
                "e3d4ce28-4291-4dd4-a650-33fd5c3b0e0f"
            ],
            "generated_media": [],
            "report": {
                "recommendation": {
                    "value": "APPROVE"
                },
                "breakdown": [
                    {
                        "sub_check": "face_processing",
                        "result": "PASS",
                        "details": [],
                        "process": "AUTOMATED"
                    },
                    {
                        "sub_check": "liveness_auth",
                        "result": "PASS",
                        "details": [],
                        "process": "AUTOMATED"
                    },
                    {
                        "sub_check": "payload_signature_verification",
                        "result": "PASS",
                        "details": [],
                        "process": "AUTOMATED"
                    }
                ]
            },
            "created": "2025-06-04T08:51:00Z",
            "last_updated": "2025-06-04T08:51:02Z"
        },
        {
            "type": "FAMILIAR_FACE_SEARCH",
            "id": "c9f2b0c0-df4d-472a-93cb-3f93c7ad9196",
            "state": "DONE",
            "resources_used": [
                "e3d4ce28-4291-4dd4-a650-33fd5c3b0e0f"
            ],
            "generated_media": [],
            "report": {
                "recommendation": {
                    "value": "REJECT",
                    "reason": "MATCH_FOUND"
                },
                "breakdown": [
                    {
                        "sub_check": "face_not_found_in_pool",
                        "result": "FAIL",
                        "details": [
                            {
                                "name": "matching_pool",
                                "value": "a8b2e5de-a31f-4e82-b2ac-557a492fa88e"
                            },
                            {
                                "name": "matching_applicant",
                                "value": "b1ac68ca-c692-449f-b6cc-1ee7c0d366ea"
                            }
                        ],
                        "process": "AUTOMATED"
                    }
                ]
            },
            "created": "2025-06-04T08:51:03Z",
            "last_updated": "2025-06-04T08:51:05Z",
            "config": {
                "pool_id": "a8b2e5de-a31f-4e82-b2ac-557a492fa88e",
                "pool_label": "POOL EXAMPLE",
                "approval_criteria": "NO_MATCH"
            }
        }
    ],
    "user_tracking_id": "<YOUR_USER_ID>",
    "biometric_consent": "2025-06-04T08:50:43Z"
}
{% /tab %}
{% tab language="json" title="MATCH" %}
{
      "type": "FAMILIAR_FACE_SEARCH",
      "id": "bc3caac1-e091-4958-8f05-8763076a6976",
      "state": "DONE",
      "resources_used": [
        "34590c66-0099-4521-b1d7-391bd5ec4e98"
      ],
      "generated_media": [],
      "report": {
        "recommendation": {
          "value": "APPROVE"
        },
        "breakdown": [
          {
            "sub_check": "face_found_in_pool",
            "result": "PASS",
            "details": [
              {
                "name": "matching_pool",
                "value": "a8b2e5de-a31f-4e82-b2ac-557a492fa88e"
              },
              {
                "name": "matching_applicant",
                "value": "b1ac68ca-c692-449f-b6cc-1ee7c0d366ea"
              }
            ],
            "process": "AUTOMATED"
          }
        ]
      },
      "created": "2025-06-25T14:17:29Z",
      "last_updated": "2025-06-25T14:17:32Z",
      "config": {
        "pool_id": "a8b2e5de-a31f-4e82-b2ac-557a492fa88e",
        "pool_label": "Test Pool2",
        "approval_criteria": "MATCH"
      }
    }
{% /tab %}
{% tab language="json" title="NO MATCH" %}
{
  "type": "FAMILIAR_FACE_SEARCH",
  "id": "c9f2b0c0-df4d-472a-93cb-3f93c7ad9196",
  "state": "DONE",
  "resources_used": [
    "e3d4ce28-4291-4dd4-a650-33fd5c3b0e0f"
  ],
  "generated_media": [],
  "report": {
    "recommendation": {
      "value": "REJECT",
      "reason": "MATCH_FOUND"
    },
    "breakdown": [
      {
        "sub_check": "face_not_found_in_pool",
        "result": "FAIL",
        "details": [
          {
            "name": "matching_pool",
            "value": "a8b2e5de-a31f-4e82-b2ac-557a492fa88e"
          },
          {
            "name": "matching_applicant",
            "value": "b1ac68ca-c692-449f-b6cc-1ee7c0d366ea"
          }
        ],
        "process": "AUTOMATED"
      }
    ]
  },
  "created": "2025-06-04T08:51:03Z",
  "last_updated": "2025-06-04T08:51:05Z",
  "config": {
    "pool_id": "a8b2e5de-a31f-4e82-b2ac-557a492fa88e",
    "pool_label": "POOL EXAMPLE",
    "approval_criteria": "NO_MATCH"
  }
}
{% /tab %}
{% /code %}

Within the **Familiar Face Search** check object you will details regarding the result of the check. The recommendation value will depend upon what has been configured in the "approval_criteria"_._ If the approval criteria is set to "MATCH" the recommendation value will be APPROVE if there is a match and if approval_criteria is set to "NO MATCH" the recommendation value will be APPROVE if there is not a match. The Familiar Face Search check object will also detail the applicant pool id that is being searched against as well as a list of applicant ids.

{% table widths="" %}
| Field | Description | 
| ---- | ---- | 
| value | The value will either be "REJECT" or "APPROVE" based on what your approval criteria is and if a match has been found. | 
| reason | The reason tells you why the check was rejected or approved. The reason can either be "MATCH" or "NO_MATCH", and will depend on what you have set as the approval criteria. | 
| breakdown | gives further insight into why the check was approved or rejected. The breakdown will also contain the applicant id of a matching applicant, which can then be used to retrieve the face of that applicant. | 
| sub_check | The sub check just identifies if the users face matches any in the applicant pool you are searching against. And will have a fail or pass result associated to it. | 
| details | The details object will display the applicant id of the applicant that matched with the user as well as the pool id of which the matched applicant is a part of. | 
{% /table %}

---

## Retrieve Face

Integrators also have the ability to retrieve the face associated with the matching applicant. The matching applicant id will need to be used in a GET request to retrieve applicant details including a UUID which can be used to retrieve the image of the users face.

{% code %}
{% tab language="http" %}
GET https://api.yoti.com/idverify/v1/applicant/<applicant_id>
{% /tab %}
{% /code %}

#### Response body

{% code %}
{% tab language="json" %}
{
  "id": "db59ddde-ca99-48aa-ac77-e59be74fc0d1",
  "faces": {
    "archetype_face": "8b9c3ea5-ebd4-436b-836d-ba8dbc80b57e",
    "faces": []
  },
  "pools": [
    {
      "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "label": "Test Pool2"
    }
  ]
}
{% /tab %}
{% /code %}

To retrieve the image of a users face the below endpoint will need to be called using the UUID linked to the applicants face. This will return the image in it's base64 encoded format. 

{% code %}
{% tab language="http" %}
GET https://api.yoti.com/idverify/v1/applicant/<applicant_id>/faces/<face_id>
{% /tab %}
{% /code %}

#### Response body

{% code %}
{% tab language="json" %}
{
  "face": {
    "data": "base64 string",
    "content_type": "image/jpeg"
  }
}
{% /tab %}
{% /code %}