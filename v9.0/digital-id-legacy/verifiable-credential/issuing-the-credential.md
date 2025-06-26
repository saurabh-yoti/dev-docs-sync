---
type: page
title: Issuing the credential
listed: true
slug: issuing-the-credential
description: 
index_title: Issuing the credential
hidden: 
keywords: 
tags: 
---

To issue a credential use the dynamic QR code functionality and the third party attribute extension:

{% code %}
{% tab language="javascript" %}
const expiryDate = new Date();
expiryDate.setDate(expiryDate.getDate() + 1);

const thirdPartyAttributeExtension = new ThirdPartyAttributeExtensionBuilder()
    .withDefinition('com.example.someAttribute')
    .withExpiryDate(expiryDate)
    .build();

const dynamicPolicy = (new DynamicPolicyBuilder())
    .withWantedRememberMe(true)
    .build();

const dynamicScenario = (new DynamicScenarioBuilder())
    .withCallbackEndpoint('/issue-attribute')
    .withPolicy(dynamicPolicy)
    .withExtension(thirdPartyAttributeExtension)
    .build();

const shareUrlResult = await yotiClient.createShareUrl(dynamicScenario);
{% /tab %}
{% tab language="java" %}
Date date = new Date();
Calendar calendar = Calendar.getInstance();
calendar.setTime(date);
calendar.add(Calendar.HOUR_OF_DAY, 5);

Date expiryDate = calendar.getTime();

Extension<ThirdPartyAttributeContent> thirdPartyAttributeExtension = new ThirdPartyAttributeExtensionBuilder()
    .withExpiryDate(expiryDate)
    .withDefinition("com.example.someAttribute")
    .build();
  
DynamicPolicy dynamicPolicy = DynamicPolicy.builder()
    .withWantedRememberMe(true)
  	.withFullName()
    .withSelfie()
    .build();

DynamicScenario dynamicScenario = DynamicScenario.builder()
    .withCallbackEndpoint("/issue")
    .withPolicy(dynamicPolicy)
    .withExtension(thirdPartyAttributeExtension)
    .build();
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\ShareUrl\DynamicScenarioBuilder;
use Yoti\ShareUrl\Extension\ThirdPartyAttributeExtensionBuilder;
use Yoti\ShareUrl\Policy\DynamicPolicyBuilder;

$thirdPartyAttributeExtension = (new ThirdPartyAttributeExtensionBuilder())
    ->withDefinition('com.example.someAttribute')
    ->withExpiryDate(new \DateTime('+1 day'))
    ->build();

$dynamicPolicy = (new DynamicPolicyBuilder())
    ->withWantedRememberMe(true)
    ->build();

$dynamicScenario = (new DynamicScenarioBuilder())
    ->withCallbackEndpoint('/issue-attribute')
    ->withPolicy($dynamicPolicy)
    ->withExtension($thirdPartyAttributeExtension)
    ->build();

$shareUrlResult = $yotiClient->createShareUrl($dynamicScenario);
{% /tab %}
{% tab language="python" %}
from datetime import datetime

from yoti_python_sdk import Client

from yoti_python_sdk.dynamic_sharing_service import (
    create_share_url,
    DynamicScenarioBuilder,
)

from yoti_python_sdk.dynamic_sharing_service.policy.dynamic_policy_builder import (
    DynamicPolicyBuilder,
)

from yoti_python_sdk.dynamic_sharing_service.extension.third_party_attribute_extension import (
    ThirdPartyAttributeExtension,
)

client = Client("YOTI_CLIENT_SDK_ID", "/path/to/key.pem")

expiry_date = datetime.datetime.now() + datetime.timedelta(days=1)

extension = (
    ThirdPartyAttributeExtension()
    .with_expiry_date(expiry_date)
    .with_definitions("com.example.someAttribute")
    .build()
)

policy = (
    DynamicPolicyBuilder()
    .with_wanted_remember_me()
    .build()
)

scenario = (
    DynamicScenarioBuilder()
    .with_callback_endpoint("/issue-attribute")
    .with_policy(policy)
    .with_extension(extension)
    .build()
)

share_url_result = share = create_share_url(client, scenario)
{% /tab %}
{% tab language="csharp" %}
var thirdPartyAttributeExtension = new ThirdPartyAttributeExtensionBuilder()
	.WithDefinition(_thirdPartyAttributeName)
	.WithExpiryDate(DateTime.Today.AddDays(1))
	.Build();

DynamicPolicy dynamicPolicy = new DynamicPolicyBuilder()
	.WithRememberMeId(required: true)
	.Build();

DynamicScenario dynamicScenario = new DynamicScenarioBuilder()
	.WithCallbackEndpoint("/home/issueattribute") //issueAttribute callback
	.WithPolicy(dynamicPolicy)
	.WithExtension(thirdPartyAttributeExtension)
        .Build();

ShareUrlResult shareUrlResult = yotiClient.CreateShareUrl(dynamicScenario);
{% /tab %}
{% tab language="go" %}
expiryDate := time.Now().AddDate(0, 0, 1)

thirdPartyExtension, err := (&extension.ThirdPartyAttributeExtensionBuilder{}).
	WithExpiryDate(&expiryDate).
	WithDefinition(attribute.NewAttributeDefinition(thirdPartyAttributeName)).
	Build()
if err != nil {
	panic(err)
}

var policy dynamic.Policy
policy, err = (&dynamic.PolicyBuilder{}).
	WithWantedRememberMe().
	Build()

if err != nil {
	panic(err)
}

var scenario dynamic.Scenario
scenario, err = (&dynamic.ScenarioBuilder{}).
	WithCallbackEndpoint("/issue-attribute").
	WithPolicy(policy).
	WithExtension(thirdPartyExtension).
	Build()
if err != nil {
	panic(err)
}

var share dynamic.ShareURL
share, err = client.CreateShareURL(&scenario)
if err != nil {
	panic(err)
}
{% /tab %}
{% tab language="ruby" %}
seconds_in_day = 86_400
expiry_date = Time.new + seconds_in_day

extension = Yoti::DynamicSharingService::ThirdPartyAttributeExtension
            .builder
            .with_expiry_date(expiry_date)
            .with_definitions('com.example.someAttribute')
            .build

policy = Yoti::DynamicSharingService::DynamicPolicy
         .builder
         .with_wanted_remember_me_id(true)
         .build

scenario = Yoti::DynamicSharingService::DynamicScenario
           .builder
           .with_callback_endpoint('/issue-attribute')
           .with_policy(policy)
           .with_extension(extension)
           .build

share_url_result = Yoti::DynamicSharingService.create_share_url(scenario)
{% /tab %}
{% /code %}

{% table widths="135" %}
| Parameter | Description | 
| ---- | ---- | 
| withDefinition() | This value will be your credential name “com.example.someAttribute” | 
| withExpiryDate() | The expired date indicates by when the credential should be issued by. If the credential is not issued by that time, the issuance request will be automatically cancelled.\n\n\n\nIt conforms to RFC3339 (e.g.: 2006-01-02T22:04:05.123Z) | 
| Dynamic policy | This is where you define all your [auto$](/digital-id-legacy/yoti-attributes) you wish to retrieve from the user. You may set source constraints to ensure only an individual can only share data from a particular document. The soft preference set to 'false' will ensure this is enforced. Please head over to the [auto$](/digital-id-legacy/createbutton) dynamic QR code section for more details on this. | 
| Dynamic scenario | Build the scenario with the third-party extension request and share policy request. | 
{% /table %}

## Get credential issuance details

The credential issuance details will include an issuance token.

{% html %}
<div class="alert-GTK">

    <div class="alert-title" id="GTK">

        Note.. 

    </div>

    <div class="alert-text">

This should be stored as part of the customer record as this will be required for issuing the credential and revoking / updating the credential in the future.
    </div>

</div>
{% /html %}

{% code %}
{% tab language="javascript" %}
const activityDetails = await yotiClient.getActivityDetails(token);
const attributeIssuanceDetails = activityDetails.getExtraData().getAttributeIssuanceDetails();
const issuingAttributes = attributeIssuanceDetails.getIssuingAttributes();
{% /tab %}
{% tab language="java" %}
ActivityDetails activityDetails = client.getActivityDetails(token);
ExtraData extraData = activityDetails.getExtraData();

AttributeIssuanceDetails attributeIssuanceDetails = extraData.getAttributeIssuanceDetails();
String issuanceToken = attributeIssuanceDetails.getToken();
{% /tab %}
{% tab language="php" %}
<?php

$activityDetails = $yotiClient->getActivityDetails($token);
$attributeIssuanceDetails = $activityDetails->getExtraData()->getAttributeIssuanceDetails();
{% /tab %}
{% tab language="python" %}
activity_details = client.get_activity_details(token)
attribute_issuance_details = activity_details.extra_data.attribute_issuance_details
{% /tab %}
{% tab language="csharp" %}
var httpClient = new HttpClient();

var activityDetails = yotiClient.GetActivityDetails(token);
var attributeIssuanceDetails = activityDetails.ExtraData.AttributeIssuanceDetails;
{% /tab %}
{% tab language="go" %}
activityDetails, err := client.GetActivityDetails(token)
if err != nil {
	panic(err)
}

issuingAttributes := activityDetails.ExtraData().AttributeIssuanceDetails()
{% /tab %}
{% tab language="ruby" %}
activity_details = Yoti::Client.get_activity_details(token)
attribute_issuance_details = activity_details.extra_data.attribute_issuance_details
{% /tab %}
{% /code %}

## Request for credential to be issued

The credential value is now ready to be issued to the Yoti user which is the schema of the credential. You will need to provide the issuance token, the name and the payload below.

{% code %}
{% tab language="javascript" %}
const payload = new Payload({
    issuance_token: attributeIssuanceDetails.getToken(),
    attributes: [
        {
            name: 'com.example.someAttribute',
            value: 'some attribute value',
        },
    ],
});

const request = new RequestBuilder()
    .withBaseUrl('https://api.yoti.com/api/v1/attribute-registry')
    .withEndpoint('/attributes')
    .withPemString('PEM_CONTENT')
    .withHeader('X-Yoti-Auth-Id', 'CLIENT_SDK_ID')
    .withMethod('POST')
    .withPayload(payload)
    .build();

const response = await request.execute();

// Note:
// - Use RequestBuilder::withPemFilePath() to provide a file path
//   (This may have performance implications)
{% /tab %}
{% tab language="java" %}
byte[] payload = ...; // Payload is JSON converted to byte array
 
SignedRequest signedRequest = SignedRequestBuilderFactory.create()
    .withKeyPair("PEM_CONTENT")
    .withBaseUrl("https://api.yoti.com/api/v1/attribute-registry")
    .withEndpoint("/attributes")
    .withHttpMethod("POST")
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
    'attributes' => [
        (object) [
            'name' => 'com.example.someAttribute',
            'value' => 'some attribute value',
        ],
    ],
]);

$request = (new RequestBuilder())
    ->withBaseUrl('https://api.yoti.com/api/v1/attribute-registry')
    ->withEndpoint('/attributes')
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
    "issuance_token": attribute_issuance_details.token,
    "attributes": [
        {
            "name": "com.example.someAttribute",
            "value": "some attribute value"
        }
    ]
}

payload_string = json.dumps(payload_data).encode()

signed_request = (
    SignedRequest
    .builder()
    .with_pem_file("/path/to/key.pem")
    .with_base_url("https://api.yoti.com/api/v1/attribute-registry")
    .with_endpoint("/attributes")
    .with_http_method("POST")
    .with_header("X-Yoti-Auth-Id", "CLIENT_SDK_ID")
    .with_payload(payload_string)
    .build()
)

response = signed_request.execute()
{% /tab %}
{% tab language="csharp" %}
var attributeDefinition = new Yoti.Auth.Share.ThirdParty.AttributeDefinition(attributeIssuanceDetails.IssuingAttributes[0].Name);
var attributeValue = "chosenAttributeValue";

string serializedRequest = JsonConvert.SerializeObject(
new {
	issuance_token = attributeIssuanceDetails.Token,
	attributes = new[]
	{
		new {
			name = _thirdPartyAttributeName,
			value = "chosenAttributeValue" // if type==JSON, this needs to be base64-encoded
		}
	}
});

byte[] httpContent = System.Text.Encoding.UTF8.GetBytes(serializedRequest);

var signedRequest = new RequestBuilder()
	.WithBaseUri(new Uri("https://api.yoti.com/api/v1/attribute-registry"))
	.WithEndpoint("/attributes")
	.WithHttpMethod(HttpMethod.Post)
	.WithHeader("X-Yoti-Auth-Id", _clientSdkId)
	.WithKeyPair(keyPair)
	.WithContent(httpContent)
	.Build();

var result = signedRequest.Execute(httpClient).Result;

if (!result.IsSuccessStatusCode)
	throw new InvalidOperationException($"StatusCode: {result.StatusCode}, Content: {result.Content.ReadAsStringAsync().Result}");
{% /tab %}
{% tab language="go" %}
type Attribute struct {
	Name  string `json:"name"`
	Value string `json:"value"`
}

type Payload struct {
	Token      string      `json:"token"`
	Attributes []Attribute `json:"attributes"`
}

body, err := json.Marshal(Payload{
	Token: issuingAttributes.Token(),
	Attributes: []Attribute{
		Attribute{
			Name:  "com.example.someAttribute",
			Value: "some attribute value",
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
	Endpoint:   "/attributes",
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
  attributes: [
    {
      name: 'com.example.someAttribute',
      value: 'some attribute value'
    }
  ]
}

request = Yoti::Request
          .builder
          .with_base_url('https://api.yoti.com/api/v1/attribute-registry')
          .with_http_method('POST')
          .with_endpoint('attributes')
          .with_payload(payload)
          .with_header('X-Yoti-Auth-Id', Yoti.configuration.client_sdk_id)
          .build

response = request.execute
{% /tab %}
{% tab language="javascript" %}
// Click to edit code
{% /tab %}
{% /code %}

The user will now have the credential.