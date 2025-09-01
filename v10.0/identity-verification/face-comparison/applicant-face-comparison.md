---
type: page
title: Applicant Face Comparison
listed: true
slug: applicant-face-comparison
description: 
index_title: Applicant Face Comparison
hidden: 
keywords: 
tags: 
---

Instead of suppling an image to use for the Face Comparison check, you can provide an Applicant ID and use the face stored with this. 

This will required steps from the previous page:

1. [Create a session](/identity-verification/face-comparison#configure-selfie-auth)  with Liveness and Face Comparison check
2. [Create a resource](/identity-verification/face-comparison#create-a-face-capture-resource) for the Face Capture

Additional steps you will need to take to use an applicant.

3. [Create an Applicant](/identity-verification/create-applicant) if you haven't already and add a Face
4. Provide the Applicant ID to the session to perform the Face Comparison check

## Add Applicant to session

{% code %}
{% tab language="http" %}
PUT https://api.yoti.com/idverify/v1/sessions/{sessionID}/resources/face-capture/{resourceID}/applicant
{% /tab %}
{% /code %}

{% code %}
{% tab language="javascript" title="Node.js" %}
const { RequestBuilder, Payload } = require("yoti");

const payload = {
  "applicant_id": "<uuid>"
};

const request = new RequestBuilder()
  .withBaseUrl("https://api.yoti.com/idverify/v1")
  .withPemFilePath("<YOTI_KEY_FILE_PATH>") // file path to PEM file
  .withEndpoint("/sessions/{sessionID}/resources/face-capture/{resourceID}/applicant")
  .withPayload(new Payload(payload))
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

$payload = [
    'applicant_id' => '<uuid>',
];
$request = (new RequestBuilder())
    ->withBaseUrl('https://api.yoti.com/idverify/v1')
    ->withPemFilePath('<YOTI_KEY_FILE_PATH>')
    ->withEndpoint('/sessions/{sessionID}/resources/face-capture/{resourceID}/applicant')
    ->withPayload(Payload::fromJsonData($payload)) 
    ->withMethod('PUT')
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

    payload = {
    		"applicant_id": applicant
		}
    payload_string = json.dumps(payload).encode()
    
    signed_request = (
        SignedRequest
        .builder()
        .with_pem_file("<YOTI_KEY_FILE_PATH>")
        .with_base_url("https://api.yoti.com/idverify/v1")
        .with_endpoint("/sessions/{sessionID}/resources/face-capture/{resourceID}/applicant")
        .with_http_method("PUT")
        .with_param("sdkId", "<YOTI_CLIENT_SDK_ID>")
				.with_payload(payload_string)
        .build()
    )

	# get Yoti response
    response = signed_request.execute()
    response_payload = json.loads(response.text)
{% /tab %}
{% tab language="java" %}
byte[] PAYLOAD = "{\"applicant_id\":\"<uuid>\"}".getBytes(StandardCharsets.UTF_8);

try {
    SignedRequest signedRequest = SignedRequestBuilder.newInstance()
        .withKeyPair(<YOTI_KEY_FILE_PATH>)
        .withBaseUrl("https://api.yoti.com/idverify/v1")
        .withEndpoint("/sessions/{sessionID}/resources/face-capture/{resourceID}/applicant")
        .withPayload(PAYLOAD)
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
data := map[string]interface{}{
    "applicant_id": "<uuid>",
}

request, _ := requests.SignedRequest{
    HTTPMethod: http.MethodPut,
    BaseURL:    "https://api.yoti.com/idverify/v1",
    Endpoint:   "/sessions/{sessionID}/resources/face-capture/{resourceID}/applicant",
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

The sessionID and resourceID will be obtained in steps 1 and 2. The Applicant ID will be obtained from step 3.

### Request Body

{% code %}
{% tab language="json" %}
{
  "applicant_id": "<uuid>",
}
{% /tab %}
{% /code %}

### Response

There will be no body in the response, only a 200 status code if successful

{% code %}
{% tab language="http" %}
HTTP/1.1 200 OK
{% /tab %}
{% /code %}

### Error codes

If there is an error, we will return an error code and error message. For example

{% code %}
{% tab language="http" title="401" %}
HTTP/1.1 401 Unauthorised request

{
  "code": "BAD_TOKEN",
  "message": "Cannot authorize your request for the session with the given token"
}
{% /tab %}
{% tab language="http" title="400" %}
HTTP/1.1 400 Bad request

{
  "code": "PAYLOAD_VALIDATION",
  "message": "There were errors validating the payload",
  "errors": [
    {
      "property": "propertyName",
      "message": "specificMessage"
    }
  ]
}
{% /tab %}
{% /code %}

{% table widths="" %}
| Error code | Description | 
| ---- | ---- | 
| 400 | Bad request - there was an error when validating the request payload. further details will be provided in errors array. See the 400 tab above. | 
| 401 | Cannot authorize your request for the session with the given token | 
| 403 | You may only update Resources that you have created | 
| 404 | No resource found for the sessionId & resourceId provided | 
| 409 | The session has expired | 
| 422 | The media provided is not processable | 
| 503 | The service is unavailable. Further details may be provided in errors array | 
{% /table %}

## Completing the session

The Liveness check will be still need to be completed by the user. Any document checks configured will also need to be completed. The user view should be presented for this. Details on this can be found [here](/identity-verification/render-the-user-view).

## Retrieving the results

Once the session is completed, you will be able to retrieve the results of the Face Comparison check. See this [page](/identity-verification/face-comparison#retrieve-results) comparison for details on how to do this.