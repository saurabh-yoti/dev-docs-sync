---
type: page
title: Defining the credential
listed: true
slug: defining-the-credential
description: 
index_title: Defining the credential
hidden: 
keywords: 
tags: 
---

At the definition stage you will define:

- The name of the credential.
- The schema for the credential.
- The format and structure of the credential - Yoti currently supports, Text (single line), JPEG, PNG and JSON object.
- Who can issue the credential.
- Who can retrieve the credential.

You will need to create the definition, using the Yoti SDK. This is a one-time process which will be used and referenced for every credential issuance.

Once you have added the Yoti SDK dependency to your project, you can use it to build and send your request. See the code snippets below for examples of how to construct the request.

{% code %}
{% tab language="javascript" %}
const payload = new Payload({
    "name": "com.example.credential",
    "mimeType": "application/json",
    "icon": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAIQAACECAYAAhOAFFlC...",
    "locales": {
        "default": "en_GB",
        "values": [
            {
                "locale": "en_GB",
                "infoUri": "https://www.example.com",
                "name": "Example Credential Name"
            }
        ]
    },
    "authz": {
        "rules": [
            {
                "name": "REQUEST",
                "orgs": ["a2399abe-c767-4748-ac37-4b726a9f9150"]
            },
            {
                "name": "ISSUE",
                "orgs": ["b3ef4e6d-581e-46e7-a373-7da2a88bc76d"]
            }
        ]
    }
});

const request = new RequestBuilder()
    .withBaseUrl('https://api.yoti.com/api/v1/attribute-registry')
    .withEndpoint('/definitions')
    .withPemString('PEM_CONTENT')
    .withHeader('X-Yoti-Auth-Id', 'CLIENT_SDK_ID')
    .withMethod('POST')
    .withPayload(payload)
    .build();

const response = await request.execute();
{% /tab %}
{% tab language="java" %}
String payload = "{ \"name\" : \"com.example.credential\", \"mimeType\" : \"application/json\", \"icon\" : \"data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAIQAACECAYAAhOAFFlC...\", \"locales\" : { \"default\" : \"en_GB\", \"values\" : [ { \"locale\" : \"en_GB\", \"infoUri\" : \"https://www.example.com\", \"name\" : \"Example Credential Name\" } ] }, \"authz\" : { \"rules\" : [ { \"name\" : \"REQUEST\", \"orgs\" : [ \"a2399abe-c767-4748-ac37-4b726a9f9150\" ] }, { \"name\" : \"ISSUE\", \"orgs\" : [ \"b3ef4e6d-581e-46e7-a373-7da2a88bc76d\" ] } ] } }";

byte[] payload = payloadString.getBytes("UTF-8");

SignedRequest signedRequest = SignedRequestBuilderFactory.create()
    .withKeyPair("PEM_CONTENT")
    .withBaseUrl("https://api.yoti.com/api/v1/attribute-registry")
    .withEndpoint("/definitions")
    .withHttpMethod(HTTP_POST)
    .withPayload(payload)
    .withHeader("X-Yoti-Auth-Id", "CLIENT_SDK_ID")
    .build();

SignedRequestResponse response = signedRequest.execute();
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\Http\Payload;
use Yoti\Http\RequestBuilder;

$payload = Payload::fromJsonData((object) [
    "name" => "com.example.credential",
    "mimeType" => "application/json",
    "icon" => "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAIQAACECAYAAhOAFFlC...",
    "locales" => (object) [
        "default" => "en_GB",
        "values" => [
            (object)[
                "locale" => "en_GB",
                "infoUri" => "https://www.example.com",
                "name" => "Example Credential Name"
            ]
        ]
    ],
    "authz" => (object) [
        "rules" => [
            (object) [
                "name" => "REQUEST",
                "orgs" => ["a2399abe-c767-4748-ac37-4b726a9f9150"]
            ],
            (object) [
                "name" => "ISSUE",
                "orgs" => ["b3ef4e6d-581e-46e7-a373-7da2a88bc76d"]
            ]
        ]
    ]
]);

$request = (new RequestBuilder())
    ->withBaseUrl('https://api.yoti.com/api/v1/attribute-registry')
    ->withEndpoint('/definitions')
    ->withPemFilePath('/path/to/key.pem')
    ->withHeader('X-Yoti-Auth-Id', 'CLIENT_SDK_ID')
    ->withMethod('POST')
    ->withPayload($payload)
    ->build();

$response = $request->execute();

if ($response->getStatusCode() !== 201) {
    // Handle error.
}

// Note:
// - Use RequestBuilder::withPemFile() to provide a `\Yoti\Util\PemFile`
// - Use RequestBuilder::withPemString() to provide PEM string
{% /tab %}
{% tab language="python" %}
import json
from yoti_python_sdk.http import SignedRequest

payload_data = {
    "name": "your_credential_name",
    "schema": { #... 
    },
    "mimeType": "mimeType",
    "icon": "base64icon",
    "locales": {
        "default": "en_GB",
    },
    "authz": {
        #...
    }   
}

payload_string = json.dumps(payload_data).encode()

signed_request = (
    SignedRequest
    .builder()
    .with_pem_file("/path/to/key.pem")
    .with_base_url("https://api.yoti.com/api/v1/attribute-registry")
    .with_endpoint("/definitions")
    .with_http_method("POST")
    .with_header("X-Yoti-Auth-Id", "CLIENT_SDK_ID")
    .with_payload(payload_string)
    .build()
)

response = signed_request.execute()
{% /tab %}
{% tab language="csharp" %}
HttpClient _httpClient = new HttpClient();

string json = JsonConvert.SerializeObject(new
{
  name = 'your_credential_name',
  schema = new { },
  mimeType = 'mimeType',
  icon = 'base64icon',
  locales = new {
    default: 'en_GB'
    },
  authz = new { }
});

byte[] httpContent = System.Text.Encoding.UTF8.GetBytes(jsonString);

var signedRequest = new RequestBuilder()
	.WithBaseUri(new Uri("https://api.yoti.com/api/v1/attribute-registry"))
	.WithEndpoint("/definitions")
	.WithHttpMethod(HttpMethod.Post)
	.WithHeader("X-Yoti-Auth-Id", _clientSdkId)
	.WithKeyPair(keyPair)
	.WithContent(httpContent)
	.Build();

HttpResponseMessage response = await signedRequest.Execute(_httpClient).ConfigureAwait(false);
{% /tab %}
{% tab language="go" %}
type Schema struct {
	Title string `json:"title"`
}

type Locale struct {
	Default string `json:"default"`
}

type Rule struct {
	Name string `json:"name"`
}

type Authz struct {
	Rules []Rule `json:"rules"`
}

type Payload struct {
	Name string `json:"name"`
  Schema Schema `json:"schema"`
	MimeType  string `json:"mimeType"`
	Icon string `json:"icon"`
  Locales Locale `json:"locales"`
  Authz Authz `json:"authz"`
}

body, err := json.Marshal(Payload{
	Name: "your_credential_name",
  Schema: Schema{
    Title: "your_schema_title",
  },
  MimeType: "mimeType",
  Icon: "base64icon",
  Locales: Locale{
    Default: "en_GB",
  },
  Authz: Authz{
    Rules: []Rules{
      Rule{
        Name: "REQUEST" | "ISSUE",
      },
  	},
  },
})
if err != nil {
	panic(err)
}

headers := map[string][]string{
	"X-Yoti-Auth-Id": []string{"CLIENT_SDK_ID"},
}

decodedKey, err := cryptoutil.ParseRSAKey(key)
if err != nil {
	panic(err)
}

request, err := requests.SignedRequest{
	Key:        decodedKey,
	HTTPMethod: http.MethodPost,
	BaseURL:    "https://api.yoti.com/api/v1/attribute-registry",
	Endpoint:   "/definitions",
	Headers:    headers,
	Body:       body,
}.Request()
if err != nil {
	panic(err)
}

response, err := requests.Execute(&http.Client{}, request)
{% /tab %}
{% tab language="ruby" %}
payload = {
    name: 'your_credential_name',
  	schema: { #... 
    } ,
  	mimeType: 'mimeType',
  	icon: 'base64icon',
    locales: {
    	default: 'en_GB'
    },
  	authz: { #... 
    }
}

request = Yoti::Request
    .builder
    .with_base_url('https://api.yoti.com/api/v1/attribute-registry')
    .with_http_method('POST')
    .with_endpoint('definitions')
    .with_payload(payload)
    .with_header('X-Yoti-Auth-Id', 'CLIENT_SDK_ID')
    .build

response = request.execute
{% /tab %}
{% /code %}

{% table %}
| Parameter | Description | 
| ---- | ---- | 
| sdkId | sdkId is the SDK_ID found with your Yoti Hub Application | 
| keyPair | The PEM file which is found with your Yoti Hub Application. The PEM file is required to allow the SDK to perform the authentication with the Yoti API. | 
{% /table %}

## Example payload

{% code %}
{% tab language="json" %}
{
  "name": "com.example.company-id",
  "schema": {
    "$id": "https://example.com/person.schema.json",
    "$schema": "http://json-schema.org/draft-07/schema#",
    "title": "Person",
    "type": "object",
    "properties": {
      "firstName": {
        "type": "string",
        "description": "The person's first name."
      },
      "lastName": {
        "type": "string",
        "description": "The person's last name."
      },
      "age": {
        "description": "Age in years which must be equal to or greater than zero.",
        "type": "integer",
        "minimum": 0
      }
    }
  },
  "mimeType": "MimeType",
  "subjectSchema": {
    "$ref": "#/schema"
  },
  "subjectMimeType": "MimeType",
  "icon": "data:image/png;base64,iVB...g==",
  "locales": {
    "default": "en_GB",
    "values": [
      {
        "locale": "en_GB",
        "infoUri": "https://some.website.com/",
        "name": "example.com identifier"
      },
      {
        "locale": "it_IT",
        "name": "Identificativo di example.com"
      }
    ]
  },
  "authz": {
    "rules": [
      {
        "name": "REQUEST" | "ISSUE",
        "orgs": [
          "<UUID>"
        ],
        "apps": [
          "<UUID>",
          "<UUID>"
        ]
      }
    ]
  }
}
{% /tab %}
{% /code %}

See below for explanation of example payload:

{% table %}
| Parameter | Description | Optional | 
| ---- | ---- | ---- | 
| Name | This is the name of the credential. This is what will appear on the users Yoti app. | ❌ | 
| MimeType | This will declare what type of credential you want. We currently support:\n\ntext/plain, application/JSON, image/png, image/jpeg. | ❌ | 
| Icon | This is the icon that will be presented to a user during the Yoti App share. It will also appear in the sharing receipts.\n\n\n\nThe icon must be at least 112px and smaller than 512kb. | ❌ | 
| locales | A list of localisation values. The name will be the display name of the credential. InfoUri is optional and can be pointer to a page that has a description or more information about your credential | ❌ | 
| authz | This is where you define who will be allowed to request or issue a credential. \n\n\n\nThis should be in a Yoti SDK ID or Organisation ID. | ❌ | 
{% /table %}

By supplying the credential in the format of a JSON object, this will allow you to bundle multiple pieces of information together in a single credential request. As an example, you could ask for the credential Employee Number. If this is supplied via a JSON object, within that credential can also contain various other bits of information such as name, email address, access level etc.

## Example response

{% code %}
{% tab language="json" %}
{
  "id": "uuid"
}
{% /tab %}
{% /code %}