---
type: page
title: Retrieve Results
listed: true
slug: retrieve-results
description: 
index_title: Retrieve Results
hidden: 
keywords: 
tags: 
---

After the user has completed their session you will then be able to retrieve the result of the session.

For any active session, you can use the Yoti API to retrieve a report on the session (containing all the end-user's uploaded documents, and recommendations). If you wish to be notified of the session completion, please use notifications.

This sections explains how to:

- Retrieve the results of the session

If you would like information on retrieving the ID document images, user information and the report head [here](https://developers.yoti.com/identity-verification/results).

{% code %}
{% tab language="http" %}
GET https://api.yoti.com/idverify/v1/sessions/{sessionId}
{% /tab %}
{% /code %}

#### SDK Example:

{% code %}
{% tab language="javascript" %}
const { RequestBuilder} = require("yoti");

const request = new RequestBuilder()
  .withBaseUrl("https://api.yoti.com/idverify/v1")
  .withPemFilePath("<YOTI_KEY_FILE_PATH>") // file path to PEM file
  .withEndpoint("/sessions/<sessionId>")
  .withMethod("GET")
  .withQueryParam("sdkId", "<YOTI_CLIENT_SDK_ID>")
  .build();

//get Yoti response
const response = await request.execute();
{% /tab %}
{% tab language="php" %}
<?php

require_once './vendor/autoload.php';

use Yoti\Http\RequestBuilder;

$response = (new RequestBuilder())
    ->withBaseUrl('https://api.yoti.com/idverify/v1')
    ->withPemFilePath('<YOTI_KEY_FILE_PATH>')
    ->withEndpoint('/sessions/<sessionId>')
    ->withMethod('GET')
    ->withQueryParam('sdkId', '<YOTI_CLIENT_SDK_ID>')
    ->build()
    ->execute();

//get Yoti response
$result = json_decode((string) $response->getBody());
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
        .with_endpoint("/sessions/<sessionId>")
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
{% /code %}

Example of the get session response of a completed session, outlining the state of the checks. A recommendation value of "APPROVE" will be issued for each one. The person in branch will not complete the session if:

- All / Any of the documents are not present
- The profile data doesn't match
- If the wrong documents are brought in
- If the documents are not valid

#### Example Responses:

The below responses are examples of the various stages of fetching a session. Typically it's recommended to use the Session Completion webhook notification to be noticed of a completed Session.

These examples are based on a three document flow, two Identity documents and one Supplementary document.

{% synced id="expand-json-block" %}
{% /synced %}

**Immediately after session creation**

{% code %}
{% tab language="json" %}
{
    "client_session_token_ttl": 2637668,
    "session_id": "1c3cae90-1769-43a9-8554-d85f2e7cdb0f",
    "state": "ONGOING",
    "client_session_token": "039abe07-166b-4f1d-9442-c86127d0143e",
    "resources": {
        "id_documents": [],
        "supplementary_documents": [],
        "liveness_capture": [],
        "face_capture": [],
        "applicant_profiles": [
            {
                "id": "9ab4729c-9777-44cd-acc1-c8d96a658125",
                "tasks": [],
                "source": {
                    "type": "RELYING_BUSINESS"
                },
                "created_at": "2023-10-16T09:18:46Z",
                "last_updated": "2023-10-16T09:18:46Z",
                "media": {
                    "id": "d609734c-e444-4c97-8211-6a3fe81e64e2",
                    "type": "JSON",
                    "created": "2023-10-16T09:18:46Z",
                    "last_updated": "2023-10-16T09:18:46Z"
                }
            }
        ]
    },
    "checks": [],
    "user_tracking_id": "optional_string"
}
{% /tab %}
{% /code %}

**After the first uploaded document**

{% code %}
{% tab language="json" %}
{
    "client_session_token_ttl": 2637490,
    "session_id": "1c3cae90-1769-43a9-8554-d85f2e7cdb0f",
    "state": "ONGOING",
    "client_session_token": "039abe07-166b-4f1d-9442-c86127d0143e",
    "resources": {
        "id_documents": [
            {
                "id": "3332241d-2ae7-437a-ae48-4b50ddb41638",
                "tasks": [],
                "source": {
                    "type": "IBV"
                },
                "created_at": "2023-10-16T09:21:19Z",
                "last_updated": "2023-10-16T09:21:40Z",
                "document_type": "PASSPORT",
                "issuing_country": "GBR",
                "pages": [
                    {
                        "capture_method": "CAMERA",
                        "media": {
                            "id": "9935a420-364e-4d45-a25d-81b971c7307a",
                            "type": "IMAGE",
                            "created": "2023-10-16T09:21:40Z",
                            "last_updated": "2023-10-16T09:21:40Z"
                        },
                        "frames": [
                            {
                                "media": {
                                    "id": "188259c5-430f-47cc-8ea2-a7c873c18dda",
                                    "type": "IMAGE",
                                    "created": "2023-10-16T09:21:42Z",
                                    "last_updated": "2023-10-16T09:21:42Z"
                                }
                            },
                            {
                                "media": {
                                    "id": "37cbd9b9-b62b-478f-aaf1-233dc0d6eda4",
                                    "type": "IMAGE",
                                    "created": "2023-10-16T09:21:44Z",
                                    "last_updated": "2023-10-16T09:21:44Z"
                                }
                            },
                            {
                                "media": {
                                    "id": "c8aa83c5-0292-4b4b-9f37-46b6bdca1856",
                                    "type": "IMAGE",
                                    "created": "2023-10-16T09:21:45Z",
                                    "last_updated": "2023-10-16T09:21:45Z"
                                }
                            }
                        ]
                    }
                ]
            }
        ],
        "supplementary_documents": [],
        "liveness_capture": [],
        "face_capture": [],
        "applicant_profiles": [
            {
                "id": "9ab4729c-9777-44cd-acc1-c8d96a658125",
                "tasks": [],
                "source": {
                    "type": "RELYING_BUSINESS"
                },
                "created_at": "2023-10-16T09:18:46Z",
                "last_updated": "2023-10-16T09:18:46Z",
                "media": {
                    "id": "d609734c-e444-4c97-8211-6a3fe81e64e2",
                    "type": "JSON",
                    "created": "2023-10-16T09:18:46Z",
                    "last_updated": "2023-10-16T09:18:46Z"
                }
            }
        ]
    },
    "checks": [],
    "user_tracking_id": "optional_string"
}
{% /tab %}
{% /code %}

**After the second uploaded document**

{% code %}
{% tab language="json" %}
{
    "client_session_token_ttl": 2637311,
    "session_id": "1c3cae90-1769-43a9-8554-d85f2e7cdb0f",
    "state": "ONGOING",
    "client_session_token": "039abe07-166b-4f1d-9442-c86127d0143e",
    "resources": {
        "id_documents": [
            {
                "id": "979b352c-8f62-4f2e-ae6e-f651c1cdd768",
                "tasks": [],
                "source": {
                    "type": "IBV"
                },
                "created_at": "2023-10-16T09:24:11Z",
                "last_updated": "2023-10-16T09:24:36Z",
                "document_type": "DRIVING_LICENCE",
                "issuing_country": "GBR",
                "pages": [
                    {
                        "capture_method": "CAMERA",
                        "media": {
                            "id": "ced2e1fa-3fe6-4aa6-9c45-4b3a71e804c8",
                            "type": "IMAGE",
                            "created": "2023-10-16T09:24:32Z",
                            "last_updated": "2023-10-16T09:24:32Z"
                        },
                        "frames": [
                            {
                                "media": {
                                    "id": "1e9e27b4-0586-4e86-9228-8c6db5c05252",
                                    "type": "IMAGE",
                                    "created": "2023-10-16T09:24:33Z",
                                    "last_updated": "2023-10-16T09:24:33Z"
                                }
                            },
                            {
                                "media": {
                                    "id": "0019a1ff-6081-405d-965a-45d2cc0d35c0",
                                    "type": "IMAGE",
                                    "created": "2023-10-16T09:24:35Z",
                                    "last_updated": "2023-10-16T09:24:35Z"
                                }
                            }
                        ]
                    },
                    {
                        "capture_method": "CAMERA",
                        "media": {
                            "id": "3a10ad34-90be-487b-9b27-63e81f3dfa57",
                            "type": "IMAGE",
                            "created": "2023-10-16T09:24:36Z",
                            "last_updated": "2023-10-16T09:24:36Z"
                        },
                        "frames": [
                            {
                                "media": {
                                    "id": "dce584db-a2cb-4f18-8076-9e04618a435a",
                                    "type": "IMAGE",
                                    "created": "2023-10-16T09:24:39Z",
                                    "last_updated": "2023-10-16T09:24:39Z"
                                }
                            },
                            {
                                "media": {
                                    "id": "0e056bcd-21db-4b04-b345-3997be10b512",
                                    "type": "IMAGE",
                                    "created": "2023-10-16T09:24:40Z",
                                    "last_updated": "2023-10-16T09:24:40Z"
                                }
                            }
                        ]
                    }
                ]
            },
            {
                "id": "3332241d-2ae7-437a-ae48-4b50ddb41638",
                "tasks": [],
                "source": {
                    "type": "IBV"
                },
                "created_at": "2023-10-16T09:21:19Z",
                "last_updated": "2023-10-16T09:21:40Z",
                "document_type": "PASSPORT",
                "issuing_country": "GBR",
                "pages": [
                    {
                        "capture_method": "CAMERA",
                        "media": {
                            "id": "9935a420-364e-4d45-a25d-81b971c7307a",
                            "type": "IMAGE",
                            "created": "2023-10-16T09:21:40Z",
                            "last_updated": "2023-10-16T09:21:40Z"
                        },
                        "frames": [
                            {
                                "media": {
                                    "id": "188259c5-430f-47cc-8ea2-a7c873c18dda",
                                    "type": "IMAGE",
                                    "created": "2023-10-16T09:21:42Z",
                                    "last_updated": "2023-10-16T09:21:42Z"
                                }
                            },
                            {
                                "media": {
                                    "id": "37cbd9b9-b62b-478f-aaf1-233dc0d6eda4",
                                    "type": "IMAGE",
                                    "created": "2023-10-16T09:21:44Z",
                                    "last_updated": "2023-10-16T09:21:44Z"
                                }
                            },
                            {
                                "media": {
                                    "id": "c8aa83c5-0292-4b4b-9f37-46b6bdca1856",
                                    "type": "IMAGE",
                                    "created": "2023-10-16T09:21:45Z",
                                    "last_updated": "2023-10-16T09:21:45Z"
                                }
                            }
                        ]
                    }
                ]
            }
        ],
        "supplementary_documents": [],
        "liveness_capture": [],
        "face_capture": [],
        "applicant_profiles": [
            {
                "id": "9ab4729c-9777-44cd-acc1-c8d96a658125",
                "tasks": [],
                "source": {
                    "type": "RELYING_BUSINESS"
                },
                "created_at": "2023-10-16T09:18:46Z",
                "last_updated": "2023-10-16T09:18:46Z",
                "media": {
                    "id": "d609734c-e444-4c97-8211-6a3fe81e64e2",
                    "type": "JSON",
                    "created": "2023-10-16T09:18:46Z",
                    "last_updated": "2023-10-16T09:18:46Z"
                }
            }
        ]
    },
    "checks": [],
    "user_tracking_id": "optional_string"
}
{% /tab %}
{% /code %}

**After the third uploaded document**

{% code %}
{% tab language="json" %}
{
    "client_session_token_ttl": 2637186,
    "session_id": "1c3cae90-1769-43a9-8554-d85f2e7cdb0f",
    "state": "ONGOING",
    "client_session_token": "039abe07-166b-4f1d-9442-c86127d0143e",
    "resources": {
        "id_documents": [
            {
                "id": "979b352c-8f62-4f2e-ae6e-f651c1cdd768",
                "tasks": [],
                "source": {
                    "type": "IBV"
                },
                "created_at": "2023-10-16T09:24:11Z",
                "last_updated": "2023-10-16T09:24:36Z",
                "document_type": "DRIVING_LICENCE",
                "issuing_country": "GBR",
                "pages": [
                    {
                        "capture_method": "CAMERA",
                        "media": {
                            "id": "ced2e1fa-3fe6-4aa6-9c45-4b3a71e804c8",
                            "type": "IMAGE",
                            "created": "2023-10-16T09:24:32Z",
                            "last_updated": "2023-10-16T09:24:32Z"
                        },
                        "frames": [
                            {
                                "media": {
                                    "id": "1e9e27b4-0586-4e86-9228-8c6db5c05252",
                                    "type": "IMAGE",
                                    "created": "2023-10-16T09:24:33Z",
                                    "last_updated": "2023-10-16T09:24:33Z"
                                }
                            },
                            {
                                "media": {
                                    "id": "0019a1ff-6081-405d-965a-45d2cc0d35c0",
                                    "type": "IMAGE",
                                    "created": "2023-10-16T09:24:35Z",
                                    "last_updated": "2023-10-16T09:24:35Z"
                                }
                            }
                        ]
                    },
                    {
                        "capture_method": "CAMERA",
                        "media": {
                            "id": "3a10ad34-90be-487b-9b27-63e81f3dfa57",
                            "type": "IMAGE",
                            "created": "2023-10-16T09:24:36Z",
                            "last_updated": "2023-10-16T09:24:36Z"
                        },
                        "frames": [
                            {
                                "media": {
                                    "id": "dce584db-a2cb-4f18-8076-9e04618a435a",
                                    "type": "IMAGE",
                                    "created": "2023-10-16T09:24:39Z",
                                    "last_updated": "2023-10-16T09:24:39Z"
                                }
                            },
                            {
                                "media": {
                                    "id": "0e056bcd-21db-4b04-b345-3997be10b512",
                                    "type": "IMAGE",
                                    "created": "2023-10-16T09:24:40Z",
                                    "last_updated": "2023-10-16T09:24:40Z"
                                }
                            }
                        ]
                    }
                ]
            },
            {
                "id": "3332241d-2ae7-437a-ae48-4b50ddb41638",
                "tasks": [],
                "source": {
                    "type": "IBV"
                },
                "created_at": "2023-10-16T09:21:19Z",
                "last_updated": "2023-10-16T09:21:40Z",
                "document_type": "PASSPORT",
                "issuing_country": "GBR",
                "pages": [
                    {
                        "capture_method": "CAMERA",
                        "media": {
                            "id": "9935a420-364e-4d45-a25d-81b971c7307a",
                            "type": "IMAGE",
                            "created": "2023-10-16T09:21:40Z",
                            "last_updated": "2023-10-16T09:21:40Z"
                        },
                        "frames": [
                            {
                                "media": {
                                    "id": "188259c5-430f-47cc-8ea2-a7c873c18dda",
                                    "type": "IMAGE",
                                    "created": "2023-10-16T09:21:42Z",
                                    "last_updated": "2023-10-16T09:21:42Z"
                                }
                            },
                            {
                                "media": {
                                    "id": "37cbd9b9-b62b-478f-aaf1-233dc0d6eda4",
                                    "type": "IMAGE",
                                    "created": "2023-10-16T09:21:44Z",
                                    "last_updated": "2023-10-16T09:21:44Z"
                                }
                            },
                            {
                                "media": {
                                    "id": "c8aa83c5-0292-4b4b-9f37-46b6bdca1856",
                                    "type": "IMAGE",
                                    "created": "2023-10-16T09:21:45Z",
                                    "last_updated": "2023-10-16T09:21:45Z"
                                }
                            }
                        ]
                    }
                ]
            }
        ],
        "supplementary_documents": [
            {
                "id": "26d51b69-7436-43d8-970c-30f5afe95ab5",
                "tasks": [],
                "source": {
                    "type": "IBV"
                },
                "created_at": "2023-10-16T09:26:18Z",
                "last_updated": "2023-10-16T09:26:43Z",
                "document_type": "UTILITY_BILL",
                "issuing_country": "GBR",
                "pages": [
                    {
                        "capture_method": "CAMERA",
                        "media": {
                            "id": "c591e997-20b4-40aa-a719-5b46f91c76a2",
                            "type": "IMAGE",
                            "created": "2023-10-16T09:26:43Z",
                            "last_updated": "2023-10-16T09:26:43Z"
                        }
                    }
                ]
            }
        ],
        "liveness_capture": [],
        "face_capture": [],
        "applicant_profiles": [
            {
                "id": "9ab4729c-9777-44cd-acc1-c8d96a658125",
                "tasks": [],
                "source": {
                    "type": "RELYING_BUSINESS"
                },
                "created_at": "2023-10-16T09:18:46Z",
                "last_updated": "2023-10-16T09:18:46Z",
                "media": {
                    "id": "d609734c-e444-4c97-8211-6a3fe81e64e2",
                    "type": "JSON",
                    "created": "2023-10-16T09:18:46Z",
                    "last_updated": "2023-10-16T09:18:46Z"
                }
            }
        ]
    },
    "checks": [],
    "user_tracking_id": "optional_string"
}
{% /tab %}
{% /code %}

**Session Completion**

{% code %}
{% tab language="json" %}
{
    "client_session_token_ttl": 2637097,
    "session_id": "1c3cae90-1769-43a9-8554-d85f2e7cdb0f",
    "state": "COMPLETED",
    "resources": {
        "id_documents": [
            {
                "id": "979b352c-8f62-4f2e-ae6e-f651c1cdd768",
                "tasks": [],
                "source": {
                    "type": "IBV"
                },
                "created_at": "2023-10-16T09:24:11Z",
                "last_updated": "2023-10-16T09:24:36Z",
                "document_type": "DRIVING_LICENCE",
                "issuing_country": "GBR",
                "pages": [
                    {
                        "capture_method": "CAMERA",
                        "media": {
                            "id": "ced2e1fa-3fe6-4aa6-9c45-4b3a71e804c8",
                            "type": "IMAGE",
                            "created": "2023-10-16T09:24:32Z",
                            "last_updated": "2023-10-16T09:24:32Z"
                        },
                        "frames": [
                            {
                                "media": {
                                    "id": "1e9e27b4-0586-4e86-9228-8c6db5c05252",
                                    "type": "IMAGE",
                                    "created": "2023-10-16T09:24:33Z",
                                    "last_updated": "2023-10-16T09:24:33Z"
                                }
                            },
                            {
                                "media": {
                                    "id": "0019a1ff-6081-405d-965a-45d2cc0d35c0",
                                    "type": "IMAGE",
                                    "created": "2023-10-16T09:24:35Z",
                                    "last_updated": "2023-10-16T09:24:35Z"
                                }
                            }
                        ]
                    },
                    {
                        "capture_method": "CAMERA",
                        "media": {
                            "id": "3a10ad34-90be-487b-9b27-63e81f3dfa57",
                            "type": "IMAGE",
                            "created": "2023-10-16T09:24:36Z",
                            "last_updated": "2023-10-16T09:24:36Z"
                        },
                        "frames": [
                            {
                                "media": {
                                    "id": "dce584db-a2cb-4f18-8076-9e04618a435a",
                                    "type": "IMAGE",
                                    "created": "2023-10-16T09:24:39Z",
                                    "last_updated": "2023-10-16T09:24:39Z"
                                }
                            },
                            {
                                "media": {
                                    "id": "0e056bcd-21db-4b04-b345-3997be10b512",
                                    "type": "IMAGE",
                                    "created": "2023-10-16T09:24:40Z",
                                    "last_updated": "2023-10-16T09:24:40Z"
                                }
                            }
                        ]
                    }
                ]
            },
            {
                "id": "3332241d-2ae7-437a-ae48-4b50ddb41638",
                "tasks": [],
                "source": {
                    "type": "IBV"
                },
                "created_at": "2023-10-16T09:21:19Z",
                "last_updated": "2023-10-16T09:21:40Z",
                "document_type": "PASSPORT",
                "issuing_country": "GBR",
                "pages": [
                    {
                        "capture_method": "CAMERA",
                        "media": {
                            "id": "9935a420-364e-4d45-a25d-81b971c7307a",
                            "type": "IMAGE",
                            "created": "2023-10-16T09:21:40Z",
                            "last_updated": "2023-10-16T09:21:40Z"
                        },
                        "frames": [
                            {
                                "media": {
                                    "id": "188259c5-430f-47cc-8ea2-a7c873c18dda",
                                    "type": "IMAGE",
                                    "created": "2023-10-16T09:21:42Z",
                                    "last_updated": "2023-10-16T09:21:42Z"
                                }
                            },
                            {
                                "media": {
                                    "id": "37cbd9b9-b62b-478f-aaf1-233dc0d6eda4",
                                    "type": "IMAGE",
                                    "created": "2023-10-16T09:21:44Z",
                                    "last_updated": "2023-10-16T09:21:44Z"
                                }
                            },
                            {
                                "media": {
                                    "id": "c8aa83c5-0292-4b4b-9f37-46b6bdca1856",
                                    "type": "IMAGE",
                                    "created": "2023-10-16T09:21:45Z",
                                    "last_updated": "2023-10-16T09:21:45Z"
                                }
                            }
                        ]
                    }
                ]
            }
        ],
        "supplementary_documents": [
            {
                "id": "26d51b69-7436-43d8-970c-30f5afe95ab5",
                "tasks": [],
                "source": {
                    "type": "IBV"
                },
                "created_at": "2023-10-16T09:26:18Z",
                "last_updated": "2023-10-16T09:26:43Z",
                "document_type": "UTILITY_BILL",
                "issuing_country": "GBR",
                "pages": [
                    {
                        "capture_method": "CAMERA",
                        "media": {
                            "id": "c591e997-20b4-40aa-a719-5b46f91c76a2",
                            "type": "IMAGE",
                            "created": "2023-10-16T09:26:43Z",
                            "last_updated": "2023-10-16T09:26:43Z"
                        }
                    }
                ]
            }
        ],
        "liveness_capture": [],
        "face_capture": [],
        "applicant_profiles": [
            {
                "id": "9ab4729c-9777-44cd-acc1-c8d96a658125",
                "tasks": [],
                "source": {
                    "type": "RELYING_BUSINESS"
                },
                "created_at": "2023-10-16T09:18:46Z",
                "last_updated": "2023-10-16T09:18:46Z",
                "media": {
                    "id": "d609734c-e444-4c97-8211-6a3fe81e64e2",
                    "type": "JSON",
                    "created": "2023-10-16T09:18:46Z",
                    "last_updated": "2023-10-16T09:18:46Z"
                }
            }
        ]
    },
    "checks": [
        {
            "type": "IBV_VISUAL_REVIEW_CHECK",
            "id": "0d0fb9e8-dcf5-4dfe-9313-6f72d7094a7c",
            "state": "DONE",
            "resources_used": [
                "979b352c-8f62-4f2e-ae6e-f651c1cdd768"
            ],
            "generated_media": [],
            "report": {
                "recommendation": {
                    "value": "APPROVE"
                },
                "breakdown": []
            },
            "created": "2023-10-16T09:28:18Z",
            "last_updated": "2023-10-16T09:28:18Z"
        },
        {
            "type": "IBV_VISUAL_REVIEW_CHECK",
            "id": "37e5b474-dafe-4d70-969b-c1da91d339d0",
            "state": "DONE",
            "resources_used": [
                "26d51b69-7436-43d8-970c-30f5afe95ab5"
            ],
            "generated_media": [],
            "report": {
                "recommendation": {
                    "value": "APPROVE"
                },
                "breakdown": []
            },
            "created": "2023-10-16T09:28:18Z",
            "last_updated": "2023-10-16T09:28:18Z"
        },
        {
            "type": "IBV_VISUAL_REVIEW_CHECK",
            "id": "0f11f52c-733f-474c-8628-170c25d0a595",
            "state": "DONE",
            "resources_used": [
                "3332241d-2ae7-437a-ae48-4b50ddb41638"
            ],
            "generated_media": [],
            "report": {
                "recommendation": {
                    "value": "APPROVE"
                },
                "breakdown": []
            },
            "created": "2023-10-16T09:28:18Z",
            "last_updated": "2023-10-16T09:28:18Z"
        },
        {
            "type": "DOCUMENT_SCHEME_VALIDITY_CHECK",
            "id": "497f77ec-0574-4ccf-95fd-57ddc9f85afa",
            "state": "DONE",
            "resources_used": [
                "26d51b69-7436-43d8-970c-30f5afe95ab5"
            ],
            "generated_media": [],
            "report": {
                "recommendation": {
                    "value": "APPROVE"
                },
                "breakdown": []
            },
            "created": "2023-10-16T09:28:18Z",
            "last_updated": "2023-10-16T09:28:18Z",
            "scheme": "UK_DBS"
        },
        {
            "type": "DOCUMENT_SCHEME_VALIDITY_CHECK",
            "id": "6b52d3c8-2f7e-42dc-bb67-5b66ac5f54b1",
            "state": "DONE",
            "resources_used": [
                "979b352c-8f62-4f2e-ae6e-f651c1cdd768"
            ],
            "generated_media": [],
            "report": {
                "recommendation": {
                    "value": "APPROVE"
                },
                "breakdown": []
            },
            "created": "2023-10-16T09:28:18Z",
            "last_updated": "2023-10-16T09:28:18Z",
            "scheme": "UK_DBS"
        },
        {
            "type": "DOCUMENT_SCHEME_VALIDITY_CHECK",
            "id": "07893874-75a3-4ce8-a734-93a0e1636005",
            "state": "DONE",
            "resources_used": [
                "3332241d-2ae7-437a-ae48-4b50ddb41638"
            ],
            "generated_media": [],
            "report": {
                "recommendation": {
                    "value": "APPROVE"
                },
                "breakdown": []
            },
            "created": "2023-10-16T09:28:18Z",
            "last_updated": "2023-10-16T09:28:18Z",
            "scheme": "UK_DBS"
        },
        {
            "type": "PROFILE_DOCUMENT_MATCH",
            "id": "6f685893-3177-49fd-bf50-b3f3629d45a4",
            "state": "DONE",
            "resources_used": [
                "979b352c-8f62-4f2e-ae6e-f651c1cdd768",
                "9ab4729c-9777-44cd-acc1-c8d96a658125"
            ],
            "generated_media": [],
            "report": {
                "recommendation": {
                    "value": "APPROVE"
                },
                "breakdown": []
            },
            "created": "2023-10-16T09:28:18Z",
            "last_updated": "2023-10-16T09:28:18Z"
        },
        {
            "type": "PROFILE_DOCUMENT_MATCH",
            "id": "d665dde2-f024-464f-be32-b4a6e47104e3",
            "state": "DONE",
            "resources_used": [
                "26d51b69-7436-43d8-970c-30f5afe95ab5",
                "9ab4729c-9777-44cd-acc1-c8d96a658125"
            ],
            "generated_media": [],
            "report": {
                "recommendation": {
                    "value": "APPROVE"
                },
                "breakdown": []
            },
            "created": "2023-10-16T09:28:18Z",
            "last_updated": "2023-10-16T09:28:18Z"
        },
        {
            "type": "PROFILE_DOCUMENT_MATCH",
            "id": "afa9c5e7-2e45-4350-93e1-6f60702e80a1",
            "state": "DONE",
            "resources_used": [
                "3332241d-2ae7-437a-ae48-4b50ddb41638",
                "9ab4729c-9777-44cd-acc1-c8d96a658125"
            ],
            "generated_media": [],
            "report": {
                "recommendation": {
                    "value": "APPROVE"
                },
                "breakdown": []
            },
            "created": "2023-10-16T09:28:18Z",
            "last_updated": "2023-10-16T09:28:18Z"
        }
    ],
    "user_tracking_id": "optional_string"
}
{% /tab %}
{% /code %}

 

The following is present in every session result.

{% table %}
| Value | Description | 
| ---- | ---- | 
| Resources | A container of all ID documents and liveness captures for this session. | 
| Checks | A container of all checks performed for this session | 
{% /table %}

### Retrieving Media

A second API call will need to be made to retrieve the media related to a session e.g document images.  

#### SDK Example:

{% code %}
{% tab language="javascript" %}
const { RequestBuilder} = require("yoti");

const request = new RequestBuilder()
  .withBaseUrl("https://api.yoti.com/idverify/v1")
  .withPemFilePath("<YOTI_KEY_FILE_PATH>") // file path to PEM file
  .withEndpoint("/sessions/<sessionId>/media/<mediaId>/content")
  .withMethod("GET")
  .withQueryParam("sdkId", "<YOTI_CLIENT_SDK_ID>")
  .build();

//get Yoti response
const response = await request.execute();
{% /tab %}
{% tab language="php" %}
<?php

require_once './vendor/autoload.php';

use Yoti\Http\RequestBuilder;

$response = (new RequestBuilder())
    ->withBaseUrl('https://api.yoti.com/idverify/v1')
    ->withPemFilePath('<YOTI_KEY_FILE_PATH>')
    ->withEndpoint('/sessions/<sessionId>/media/<mediaId>/content')
    ->withMethod('GET')
    ->withQueryParam('sdkId', '<YOTI_CLIENT_SDK_ID>')
    ->build()
    ->execute();

//get Yoti response
$result = $response->getBody();
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
        .with_endpoint("/sessions/<sessionId>/media/<mediaId>/content")
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
try {
    SignedRequest signedRequest = SignedRequestBuilder.newInstance()
        .withKeyPair(<YOTI_KEY_FILE_PATH>)
        .withBaseUrl("https://api.yoti.com/idverify/v1")
        .withEndpoint("/sessions/<SESSION_ID>/media/<mediaId>/content")
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
        Endpoint:   "/sessions/<SESSION_ID>/media/<mediaId>/content",
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
{% /code %}