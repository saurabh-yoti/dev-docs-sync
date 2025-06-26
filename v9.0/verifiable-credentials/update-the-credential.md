---
type: page
title: Update the credential
listed: true
slug: update-the-credential
description: 
index_title: Update the credential
hidden: 
keywords: 
tags: 
---

You can update an individual users credential by overriding the value and using the issuance token associated to the user. This requires no interaction from the user and will automatically update the Yoti app.

{% code %}
{% tab language="javascript" %}
const payload = new Payload({
    issuance_token: attributeIssuanceDetails.getToken(),
    name: 'com.example.someAttribute',
    value: 'some updated attribute value',
});

const request = new RequestBuilder()
    .withBaseUrl('https://api.yoti.com/api/v1/attribute-registry')
    .withEndpoint('/attribute/update')
    .withPemString('PEM_CONTENT')
    .withHeader('X-Yoti-Auth-Id', 'CLIENT_SDK_ID')
    .withMethod('PUT')
    .withPayload(payload)
    .build();

const response = await request.execute();
{% /tab %}
{% tab language="java" %}
byte[] payload = ...; // Payload is JSON converted to byte array
 
SignedRequest signedRequest = SignedRequestBuilderFactory.create()
    .withKeyPair("PEM_CONTENT")
    .withBaseUrl("https://api.yoti.com/api/v1/attribute-registry")
    .withEndpoint("/attribute/update")
    .withHttpMethod("PUT")
    .withHeader("X-Yoti-Auth-Id", "CLIENT_SDK_ID")
    .withPayload(payload)
    .build();
 
// 'SomeModel' is a POJO that has been defined by the user and is
// used to map JSON response as the SDK doesn't have any built in
// classes to support this
SomeModel someModel = signedRequest.execute(SomeModel.class);
 
/**
 * SignedRequest.execute() uses built in Java HTTP connectivity.
 * To use another framework if required (e.g. apache), you can get
 * all of the pieces of the Yoti signed request off the SignedRequest
 * object e.g.
**/
URI uri = signedRequest.getUri();
String httpMethod = signedRequest.getMethod();
byte[] payloadData = signedRequest.getData();
Map<String, String> headers = signedRequest.getHeaders();
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\Http\Payload;
use Yoti\Http\RequestBuilder;

$payload = Payload::fromJsonData((object) [
    'issuance_token' => $attributeIssuanceDetails->getToken(),
    'name' => 'com.example.someAttribute',
    'value' => 'some updated attribute value',
]);

$request = (new RequestBuilder())
    ->withBaseUrl('https://api.yoti.com/api/v1/attribute-registry')
    ->withEndpoint('/attribute/update')
    ->withPemFilePath('/path/to/key.pem')
    ->withHeader('X-Yoti-Auth-Id', 'CLIENT_SDK_ID')
    ->withMethod('PUT')
    ->withPayload($payload)
    ->build();

$response = $request->execute();

// Note:
// - Use RequestBuilder::withPemFile() to provide a `\Yoti\Util\PemFile`
// - Use RequestBuilder::withPemString() to provide PEM string
{% /tab %}
{% tab language="python" %}
import json

from yoti_python_sdk.http import SignedRequest

payload_data = {
    "issuance_token": attribute_issuance_details.token,
    "name": 'com.example.someAttribute',
    "value": 'some updated attribute value'
}

payload_string = json.dumps(payload_data).encode()

signed_request = (
    SignedRequest
    .builder()
    .with_pem_file("/path/to/key.pem")
    .with_base_url("https://api.yoti.com/api/v1/attribute-registry")
    .with_endpoint("/attribute/update")
    .with_http_method("PUT")
    .with_header("X-Yoti-Auth-Id", "CLIENT_SDK_ID")
    .with_payload(payload_string)
    .build()
)

response = signed_request.execute()
{% /tab %}
{% tab language="csharp" %}
var dynamicScenarioBuilder = new DynamicScenarioBuilder();
var dynamicPolicyBuilder = new DynamicPolicyBuilder();

object deserializedObject;
using (StreamReader r = System.IO.File.OpenText("UpdateValue.json"))
{
	string text = r.ReadToEnd();
	deserializedObject = JsonConvert.DeserializeObject(text);
}

string attributeValueJson = JsonConvert.SerializeObject(deserializedObject);

string base64AttributeValue = Convert.ToBase64String(
	Encoding.UTF8.GetBytes(attributeValueJson));

string json = JsonConvert.SerializeObject(new
{
	issuance_token = _issuanceToken,
	name = _thirdPartyAttributeName,
	value = base64AttributeValue
});

byte[] httpContent = System.Text.Encoding.UTF8.GetBytes(json);

var signedRequest = new RequestBuilder()
	.WithBaseUri(new Uri("https://api.yoti.com/api/v1/attribute-registry"))
	.WithEndpoint("/attribute/update")
	.WithHttpMethod(HttpMethod.Put)
	.WithHeader("X-Yoti-Auth-Id", _clientSdkId)
	.WithKeyPair(_keyPair)
	.WithContent(httpContent)
	.Build();

var result = signedRequest.Execute(_httpClient).Result;
{% /tab %}
{% tab language="go" %}
type Payload struct {
	Token string `json:"issuance_token"`
	Name  string `json:"name"`
	Value string `json:"value"`
}

body, err := json.Marshal(Payload{
	Token: issuingAttributes.Token(),
	Name:  "com.example.someAttribute",
	Value: "some attribute value",
})
if err != nil {
	panic(err)
}

headers := map[string][]string{
	"X-Yoti-Auth-Id": {"CLIENT_SDK_ID"},
}

decodedKey, err := cryptoutil.ParseRSAKey(key)
if err != nil {
	panic(err)
}

request, err := requests.SignedRequest{
	Key:        decodedKey,
	HTTPMethod: http.MethodPut,
	BaseURL:    "https://api.yoti.com/api/v1/attribute-registry",
	Endpoint:   "/attribute/update",
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
  issuance_token: attribute_issuance_details.token,
  name: 'com.example.someAttribute',
  value: 'some updated attribute value'
}

request = Yoti::Request
          .builder
          .with_base_url('https://api.yoti.com/api/v1/attribute-registry')
          .with_http_method('PUT')
          .with_endpoint('attribute/update')
          .with_payload(payload)
          .with_header('X-Yoti-Auth-Id', Yoti.configuration.client_sdk_id)
          .build

response = request.execute
{% /tab %}
{% /code %}