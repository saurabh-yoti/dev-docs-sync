---
type: page
title: Sandbox
listed: true
slug: sandbox-docscan
description: 
index_title: Sandbox
hidden: 
keywords: 
tags: 
---

Welcome to the developer documentation for the Yoti Doc Scan Sandbox.

With the Doc Scan sandbox, you are able to do the following:

- Set outcomes and mock text results
- Mock approvals and rejections
- Mock liveness and image upload

This guide assumes that you already have an existing Doc Scan environment set up to connect to Yoti’s production services, but wish to introduce sandbox testing on top. We recommend [auto$](/yoti/getting-started-docscan) from the beginning to thoroughly understand the Doc Scan flow before integrating. This will ensure you create reliable tests that accurately simulate the production environment.

The Doc Scan Sandbox service bypasses real world checks and tasks. Instead, you must specify the outcome beforehand, as opposed to it being returned from Yoti’s production systems. This is achieved by using an additional response-config endpoint. A response-config must be set before proceeding with the user view for sandbox setups.

For simplicity, an overview of the steps is shown below:

1 - Generating Sandbox Keys

2 - Creating a Sandbox session

3 - Setting the Doc Scan Sandbox Response Config

4 - Launching the user view

5 - Retrieving results and data

---

## Endpoints

{% code %}
{% tab language="http" %}
Sandbox - https://api.yoti.com/sandbox/idverify/v1
Production - https://api.yoti.com/idverify/v1
{% /tab %}
{% /code %}

---

## Generating Sandbox Keys

Our sandbox service requires its own set of sandbox keys. For further details on how to create these, please see [auto$](/yoti/generate-sandbox-api-keys).

---

## Creating a Sandbox session

For details on how to create a Doc Scan session, please see [auto$](/yoti/generating-a-session). A sandbox session will be created by substituting the Base URL for the Sandbox URL, and replacing your SDK ID and PEM file with your Sandbox keys.

---

## Setting the Doc Scan Sandbox Response Config

Now you that have successfully created a session, the next step is to set the response config. Sandbox requires you to set an expected outcome for your tasks and checks. This will be an object with defined **task_results** and **check_reports**.

{% code %}
{% tab language="javascript" %}
const { RequestBuilder, Payload } = require("yoti");

const request = new RequestBuilder()
  .withBaseUrl("https://api.yoti.com/sandbox/idverify/v1")
  .withPemFilePath("<YOTI_KEY_FILE_PATH>")
  .withEndpoint("/sessions/<SESSION_ID>/response-config")
  .withPayload(new Payload(RESPONSE_CONFIG))
  .withMethod("PUT")
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
    ->withBaseUrl('https://api.yoti.com/sandbox/idverify/v1')
    ->withPemFilePath('<YOTI_KEY_FILE_PATH>')
    ->withEndpoint('/sessions/<SESSION_ID>/response-config')
    ->withPayload(Payload::fromString(RESPONSE_CONFIG_STRING)) // * Version ^2: new Payload(SESSION_OBJ)
    ->withMethod('PUT')
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
    payload_string = json.dumps(data).encode()
    signed_request = (
        SignedRequest
        .builder()
        .with_pem_file("https://api.yoti.com/sandbox/idverify/v1")
        .with_base_url("<BASE_URL>")
        .with_endpoint("/sessions/<SESSION_ID>/response-config")
        .with_http_method("PUT")
        .with_query_param("sdkId", "<YOTI_CLIENT_SDK_ID>")
        .with_payload(payload_string)
        .build()
    )

  # get Yoti response
    response = signed_request.execute()
    response_payload = json.loads(response.text)
{% /tab %}
{% tab language="java" %}
byte[] RESPONSE_CONFIG = ...

try {
    SignedRequest signedRequest = SignedRequestBuilder.newInstance()
        .withKeyPair(<YOTI_KEY_FILE_PATH>)
        .withBaseUrl("https://api.yoti.com/sandbox/idverify/v1")
        .withEndpoint("/sessions/<SESSION_ID>/response-config")
        .withPayload(RESPONSE_CONFIG)
        .withHttpMethod("PUT")
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
        HTTPMethod: http.MethodPut,
        BaseURL:    "<BASE_URL>",
        Endpoint:   "/sessions/<SESSION_ID>/response-config",
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
// COMING SOON
{% /tab %}
{% /code %}

### Task Results

Contains a result set for extracted text, defined by the **document_fields** property. This should be used to mock extracted text from documents. The format of the payload used here should contain properties listed from [document fields explained.](/yoti/session-and-media-retrieval#document-fields-explained)

{% code %}
{% tab language="json" %}
{
  "task_results": {
    "ID_DOCUMENT_TEXT_DATA_EXTRACTION": [
      {
        "result": {
          "document_fields": {
            "full_name": "Test",
            "document_number": "TEST23123",
            "date_of_birth": "1980-12-20"
          }
        }
      }
    ]
  },
}
{% /tab %}
{% /code %}

### Check Results

A Doc Scan check can be one of the following:

- Document Authenticity
- Document Text Data Check
- Liveness
- Face Match

Sandbox will allow you to set a response for each of these checks.

### Document Authenticity

{% code %}
{% tab language="json" %}
{
    "check_reports": {
      "ID_DOCUMENT_AUTHENTICITY": [
          {
            "result": {
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
                    "sub_check": "hologram"
                    "result": "PASS",
                    "details": []
                  },
                  {
                    "sub_check": "hologram_movement",
                    "result": "FAIL",
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
              }
            }
          }
        ],
      "async_report_delay": 1
    }
  }
{% /tab %}
{% /code %}

### Document Text Data Check

{% code %}
{% tab language="json" %}
{
  "check_reports": {
    "ID_DOCUMENT_TEXT_DATA_CHECK": [
      {
        "result": {
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
          }
        }
      }
    ],
    "async_report_delay": 6
  }
}
{% /tab %}
{% /code %}

### Liveness

{% code %}
{% tab language="json" %}
{
  "check_reports": {
    "LIVENESS": [
      {
        "liveness_type": "ZOOM",
        "result": {
          "report": {
            "recommendation": {
              "value": "REJECT"
            },
            "breakdown": [
              {
                "sub_check": "liveness_auth",
                "result": "FAIL",
                "details": []
              }
            ]
          }
        }
      },
      {
        "liveness_type": "ZOOM",
        "result": {
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
          }
        }
      }
    ],
    "async_report_delay": 6
  }
}
{% /tab %}
{% /code %}

### Face Match

{% code %}
{% tab language="json" %}
{
  "check_reports": {
    "ID_DOCUMENT_FACE_MATCH": [
      {
        "result": {
          "report": {
            "recommendation": {
              "value": "APPROVE"
            },
            "breakdown": [
              {
                "sub_check": "ai_face_match",
                "result": "FAIL",
                "details": [
                  {
                    "name": "confidence_score",
                    "value": "0.53"
                  }
                ]
              },
              {
                "sub_check": "manual_face_match",
                "result": "PASS",
                "details": []
              }
            ]
          }
        }
      }
    ],
    "async_report_delay": 6
  }
}
{% /tab %}
{% /code %}

### Async report delay

The Async report delay is a timer (in seconds) which simulates a delay between the Doc Scan iFrame user journey and the result of the report, set by your expectation. By using this facility you can effectively handle pending states, or results that are not returned instantly (such as manual checks).

### Full example response config

{% code %}
{% tab language="json" %}
{
  "task_results": {
    "ID_DOCUMENT_TEXT_DATA_EXTRACTION": [
      {
        "result": {
          "document_fields": {
            "full_name": "Test",
            "document_number": "TEST23123",
            "date_of_birth": "1980-12-20"
          }
        }
      }
    ]
  },
  "check_reports": {
    "ID_DOCUMENT_AUTHENTICITY": [
      {
        "result": {
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
                "result": "FAIL",
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
          }
        }
      }
    ],
    "ID_DOCUMENT_TEXT_DATA_CHECK": [
      {
        "result": {
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
          }
        }
      }
    ],
    "LIVENESS": [
      {
        "liveness_type": "ZOOM",
        "result": {
          "report": {
            "recommendation": {
              "value": "REJECT"
            },
            "breakdown": [
              {
                "sub_check": "liveness_auth",
                "result": "FAIL",
                "details": []
              }
            ]
          }
        }
      },
      {
        "liveness_type": "ZOOM",
        "result": {
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
          }
        }
      }
    ],
    "ID_DOCUMENT_FACE_MATCH": [
      {
        "result": {
          "report": {
            "recommendation": {
              "value": "APPROVE"
            },
            "breakdown": [
              {
                "sub_check": "ai_face_match",
                "result": "FAIL",
                "details": [
                  {
                    "name": "confidence_score",
                    "value": "0.53"
                  }
                ]
              },
              {
                "sub_check": "manual_face_match",
                "result": "PASS",
                "details": []
              }
            ]
          }
        }
      }
    ],
    "async_report_delay": 6
  }
}
{% /tab %}
{% /code %}

---

## Launching the user view

Once you have set your sandbox response config, you will need to fulfil the **user view** for Doc Scan. You may continue to render the Doc Scan Client through an iFrame, however the **base_url** will need to be updated first. The new sandbox iFrame URL is shown below:

{% code %}
{% tab language="http" %}
https://api.yoti.com/sandbox/idverify/v1/web/index.html?sessionID=<inputsessionID>&sessionToken=<yoursessionToken>
{% /tab %}
{% /code %}

The user view must be completed. We are working on allowing this to be achieved programmatically instead of manually.

---

### Retrieving results and data

Retrieving the media response is unchanged. You can still use the same get media endpoint, with the returning media ID from get session, but the base url should be updated to [https://api.yoti.com/sandbox/idverify/v1](https://api.yoti.com/sandbox/idverify/v1) first.

For further details, please see [](/yoti/session-and-media-retrieval).