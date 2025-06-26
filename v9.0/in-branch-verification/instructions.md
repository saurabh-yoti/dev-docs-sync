---
type: page
title: Customer Letter
listed: true
slug: instructions
description: 
index_title: Customer Letter
hidden: 
keywords: 
tags: 
---

Here we will show you how to generate the Post Office in branch verification customer letter which contains;   

- Applicant information
- List of documents
- Branch address
- Further information.
- A QR code that the person in branch will be required to scan.

## Fetch session config

This endpoint will retrieve the session configuration, and also provide the requirement ID to be used for the instructions. This will be in a UUID format per document requested, and can be found in the required_resources array per document.

{% code %}
{% tab language="http" %}
GET https://api.yoti.com/idverify/v1/sessions/{sessionId}/configuration
{% /tab %}
{% /code %}

#### SDK Example:

{% code %}
{% tab language="javascript" %}
const { RequestBuilder} = require("yoti");

const request = new RequestBuilder()
  .withBaseUrl("https://api.yoti.com/idverify/v1")
  .withPemFilePath("<YOTI_KEY_FILE_PATH>") // file path to PEM file
  .withEndpoint("/sessions/<sessionId>/configuration")
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
    ->withEndpoint('/sessions/<sessionId>/configuration')
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
        .with_endpoint("/sessions/<sessionId>/configuration")
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
        .withEndpoint("/sessions/<SESSION_ID>/configuration")
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
        Endpoint:   "/sessions/<SESSION_ID>/configuration",
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
{% /code %}

### Example Response

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

### Error Response

{% code %}
{% tab language="json" %}
// 400 response
{
  "code": "MALFORMED_REQUEST",
  "errors": [
    {
      "property": "header.X-Yoti-Auth-Token",
      "message": "must not be null or empty"
    }
  ]
}
{% /tab %}
{% /code %}

{% table %}
| Error code | Description | 
| ---- | ---- | 
| 400 | malformed request | 
| 401 | unauthorised request, wrong key used | 
| 404 | no session found matching the sessionId provided | 
| 409 | cannot begin this session until integrator provides all required resources | 
| 503 | service is unavailable | 
{% /table %}

## Generate Customer Letter

This endpoint will generate the letter that the applicant needs to complete the IBV session. 

{% code %}
{% tab language="http" %}
PUT https://api.yoti.com/idverify/v1/sessions/{sessionId}/instructions
{% /tab %}
{% /code %}

#### SDK Example

{% code %}
{% tab language="javascript" %}
const { RequestBuilder} = require("yoti");

const request = new RequestBuilder()
  .withBaseUrl("https://api.yoti.com/idverify/v1")
  .withPemFilePath("<YOTI_KEY_FILE_PATH>") // file path to PEM file
  .withEndpoint("/sessions/<sessionId>/instructions")
  .withPayload(new Payload(INSTRUCTIONS_OBJ))
  .withMethod("PUT")
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
    ->withEndpoint('/sessions/<sessionId>/instructions')
    ->withMethod('PUT')
    ->withPayload(Payload::fromJsonData($payload))
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
  
    payload = {} # payload
    payload_string = json.dumps(payload).encode()

    signed_request = (
        SignedRequest
        .builder()
        .with_pem_file("<YOTI_KEY_FILE_PATH>")
        .with_base_url("https://api.yoti.com/idverify/v1")
        .with_endpoint("/sessions/<sessionId>/instructions")
        .with_http_method("PUT")
        .with_payload(payload_string)
        .with_param("sdkId", "<YOTI_CLIENT_SDK_ID>")
        .build()
    )

    response = signed_request.execute()
    response_payload = json.loads(response.text)

//get Yoti response
print(get_session())
{% /tab %}
{% tab language="java" %}
byte[] INSTRUCTIONS_OBJ = ...

try {
    SignedRequest signedRequest = SignedRequestBuilder.newInstance()
        .withKeyPair(<YOTI_KEY_FILE_PATH>)
        .withBaseUrl("https://api.yoti.com/idverify/v1")
        .withEndpoint("/sessions/<sessionID>/instructions")
        .withPayload(INSTRUCTIONS_OBJ)
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
        BaseURL:    "https://api.yoti.com/idverify/v1",
        Endpoint:   "/sessions/<sessionId>/instructions",
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

## [Example](https://developers.yoti.com/in-branch-verification/instructions#example)

See below for a complete payload. This will just return a null body.

{% code %}
{% tab language="json" %}
{
  "contact_profile": {
    "first_name": "John",
    "last_name": "Doe",
    "email": "john.doe@gmail.com"
  },
  "documents": [
    {
      "requirement_id": "someIdDocumentRequirementId",
      "document": {
        "type": "ID_DOCUMENT",
        "country_code": "GBR",
        "document_type": "PASSPORT"
      }
    },
    {
      "requirement_id": "someSupplementaryDocumentRequirementId",
      "document": {
        "type": "SUPPLEMENTARY_DOCUMENT",
        "country_code": "GBR",
        "document_type": "UTILITY_BILL"
      }
    }
  ],
  "branch": {
    "type": "UK_POST_OFFICE",
    "fad_code": "12345678"
  }
}
{% /tab %}
{% /code %}

### Error Response

{% code %}
{% tab language="json" %}
//400 response
{
  "code": "PAYLOAD_VALIDATION",
  "message": "There were errors validating the payload",
  "errors": [
    {
      "property": "The JSON property name",
      "message": "The error message associated with the property"
    }
  ]
}
{% /tab %}
{% /code %}

{% table %}
| Error code | Description | 
| ---- | ---- | 
| 400 | payload validation error | 
| 401 | unauthorised request, wrong key used | 
| 404 | the referenced application does not exist | 
| 409 | the session has expired | 
| 500 | internal server error | 
| 503 | service is unavailable | 
{% /table %}

---

## Retrieving Customer Letter

This endpoint is used to pull the generated letter in a PDF format, which you can then send to the applicant.

{% code %}
{% tab language="http" %}
GET https://api.yoti.com/idverify/v1/sessions/{sessionId}/instructions/pdf
{% /tab %}
{% /code %}

#### SDK Example

{% code %}
{% tab language="javascript" %}
const fs = require('fs');
const { RequestBuilder } = require("yoti");

const request = new RequestBuilder()
  .withBaseUrl("https://api.yoti.com/idverify/v1")
  .withPemFilePath("<YOTI_KEY_FILE_PATH>") // file path to PEM file
  .withEndpoint("/sessions/<sessionId>/instructions/pdf")
  .withMethod("GET")
  .withQueryParam("sdkId", "<YOTI_CLIENT_SDK_ID>")
  .build();

// get Yoti response, buffer set to true for execute
const response = await request.execute(true);

// get parsed response
const instructions = response.getParsedResponse();

// Decode instructions octet stream to base64
const base64 = instructions.toString('base64');

// Convert base64 to pdf buffer
const pdf = Buffer.from(base64, 'base64');

// Write pdf buffer to file
const fileName = 'instructions.pdf';
fs.writeFile(fileName, pdf, (error) => {
  if (error) throw error;
  console.log(`PDF saved to ${fileName}`);
});
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\Http\RequestBuilder;

$request = (new RequestBuilder())
    ->withBaseUrl('https://api.yoti.com/idverify/v1')
    ->withPemFilePath('<YOTI_KEY_FILE_PATH>')
    ->withEndpoint('/sessions/<sessionId>/instructions/pdf')
    ->withMethod('GET')
    ->withQueryParam('sdkId', '<YOTI_CLIENT_SDK_ID>')
    ->build();

// get Yoti Response
$response = $request->execute();

// get parsed response
$instructions = $response->getParsedResponse();

// Decode instructions octet stream to base64
$base64 = base64_encode($instructions);

// Convert base64 to pdf
$pdf = base64_decode($base64);

// Write pdf to file
$fileName = 'instructions.pdf';
file_put_contents($fileName, $pdf);

echo "PDF saved to $fileName";
{% /tab %}
{% tab language="python" %}
import base64
from yoti_python_sdk.http import SignedRequest

signed_request = (
    SignedRequest.builder()
    .with_base_url("https://api.yoti.com/idverify/v1")
    .with_pem_file("<YOTI_KEY_FILE_PATH>")
    .with_endpoint("/sessions/<sessionId>/instructions/pdf")
    .with_http_method("GET")
    .with_param("sdkId", "<YOTI_CLIENT_SDK_ID>")
    .build()
)

# get Yoti Response
response = signed_request.execute()

# get parsed response
instructions = response.parsed_response

# Decode instructions octet stream to base64
base64_instructions = base64.b64encode(instructions)

# Convert base64 to pdf
pdf = base64.b64decode(base64_instructions)

# Write pdf to file
file_name = 'instructions.pdf'
with open(file_name, 'wb') as f:
    f.write(pdf)

print(f"PDF saved to {file_name}")
{% /tab %}
{% tab language="java" %}
import org.apache.commons.codec.binary.Base64;
import com.yoti.api.client.spi.remote.call.SignedRequest;
import com.yoti.api.client.spi.remote.call.SignedRequestResponse;
import java.nio.file.Files;
import java.nio.file.Paths;
import java.io.IOException;

SignedRequest signedRequest = SignedRequest.builder()
    .withBaseUrl("https://api.yoti.com/idverify/v1")
    .withPemContents("PEM_CONTENT")
    .withEndpoint("/sessions/<sessionId>/instructions/pdf")
    .withHttpMethod("GET")
    .withQueryParam("sdkId", "<YOTI_CLIENT_SDK_ID>")
    .build();

// get Yoti Response
SignedRequestResponse response = signedRequest.execute();

// get parsed response
byte[] instructions = response.getParsedResponse();

// Decode instructions octet stream to base64
String base64 = Base64.encodeBase64String(instructions);

// Convert base64 to pdf
byte[] pdf = Base64.decodeBase64(base64);

// Write pdf to file
String fileName = "instructions.pdf";
try {
    Files.write(Paths.get(fileName), pdf);
    System.out.println("PDF saved to " + fileName);
} catch (IOException e) {
    e.printStackTrace();
}
{% /tab %}
{% tab language="go" %}
package main

import (
    "encoding/base64"
    "fmt"
    "io"
    "net/http"
    "os"

    "github.com/getyoti/yoti-go-sdk/v3/requests"
)

func main() {
    key, _ := os.ReadFile("<YOTI_KEY_FILE_PATH>")

    request, _ := requests.SignedRequest{
        HTTPMethod: http.MethodGet,
        BaseURL:    "https://api.yoti.com/idverify/v1",
        Endpoint:   "/sessions/<sessionId>/instructions/pdf",
				Params:     map[string]string{"sdkID": "<YOTI_CLIENT_SDK_ID>"},
    }.WithPemFile(key).Request()

    // Get Yoti response
    response, err := http.DefaultClient.Do(request)
    if err != nil {
        fmt.Println("Error making HTTP request:", err)
        return
    }

    // Get parsed response
    instructions, _ := io.ReadAll(response.Body)

    // Decode instructions octet stream to base64
    base64Instructions := base64.StdEncoding.EncodeToString(instructions)

    // Convert base64 to pdf
    pdf, _ := base64.StdEncoding.DecodeString(base64Instructions)

    // Write pdf to file
    fileName := "instructions.pdf"
    os.WriteFile(fileName, pdf, 0644)

    fmt.Printf("PDF saved to %s\n", fileName)
}
{% /tab %}
{% tab language="csharp" %}
using System;
using System.IO;
using System.Net.Http;
using System.Threading.Tasks;
using Yoti.Auth.Web;

HttpClient _httpClient = new HttpClient();

Request signedRequest = new RequestBuilder()
    .WithBaseUri(new Uri("https://api.yoti.com/idverify/v1"))
    .WithKeyPair("PEM_CONTENT")
    .WithEndpoint("/sessions/<sessionId>/instructions/pdf")
    .WithHttpMethod(HttpMethod.Get)
    .WithQueryParam("sdkId", "<YOTI_CLIENT_SDK_ID>")
    .Build();

// get Yoti Response
HttpResponseMessage response = await signedRequest.Execute(_httpClient).ConfigureAwait(false);

// get parsed response
var instructions = await response.Content.ReadAsByteArrayAsync();

// Decode instructions octet stream to base64
var base64 = Convert.ToBase64String(instructions);

// Convert base64 to pdf
var pdf = Convert.FromBase64String(base64);

// Write pdf to file
var fileName = "instructions.pdf";
await File.WriteAllBytesAsync(fileName, pdf);

Console.WriteLine($"PDF saved to {fileName}");
{% /tab %}
{% /code %}

#### PDF Example

{% image url="https://uploads.developerhub.io/prod/kvAX/3uf2kbdc321rnbxdtzbtdi3os68dswrwphw4z98ap3qd2ldj37l8qb4axitzschw.png" mode="600" height="841" width="595" %}
{% /image %}

Important - The use of the Post Office branded customer letter is mandatory for the In-Branch Verification service.

### Error Response

{% code %}
{% tab language="json" %}
//400 response
{
  "code": "PAYLOAD_VALIDATION",
  "message": "There were errors validating the payload",
  "errors": [
    {
      "property": "The JSON property name",
      "message": "The error message associated with the property"
    }
  ]
}
{% /tab %}
{% /code %}

{% table %}
| Error code | Description | 
| ---- | ---- | 
| 400 | payload validation error | 
| 401 | unauthorised request, wrong key used | 
| 404 | the referenced application does not exist | 
| 409 | the session has expired | 
| 500 | internal server error | 
| 503 | service is unavailable | 
{% /table %}