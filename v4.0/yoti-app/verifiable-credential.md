---
type: page
title: Create your own credential
listed: true
slug: verifiable-credential
description: 
index_title: Create your own credential
hidden: 
keywords: 
tags: 
---

Yoti allows you to issue your own 'attribute' to a Yoti user. This document will walk you through our API giving the ability to choose who is able to both issue and request these credentials in the credential definition stage. At Yoti we call this a verifiable credential.

A verifiable credential​ is handled in the same way as any Yoti [attribute](https://developers.yoti.com/yoti/knowledge-base-hub#general-attributes) but follows the same concept as the [W3C standard](https://www.w3.org/TR/vc-data-model/#what-is-a-verifiable-credential). The definition of an attribute is an assertion made about a user. It can be identity information, something that the user owns and can prove they are in control of.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1604061494/72661/k7rfslsm5vax0lgltljp.png" caption="Credential creation with Yoti" mode="full" height="3692" width="3311" %}
{% /image %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
        If you wish to use this functionality please let us know as this process currently requires us to do a Yoti app change internally.
    </div>
    <div class="alert-links"> 
        <a href="mailto:sdksupport@yoti.com">SDK Support contact</a>
   </div>
</div>
{% /html %}

There are three main stages to create and use your credential:

- [Defining the credential.](https://developers.yoti.com/yoti-app/verifiable-credential#defining-the-credential)
- [Issuing the credential.](https://developers.yoti.com/yoti-app/verifiable-credential#issuing-an-credential)
- [Requesting the credential.](https://developers.yoti.com/yoti-app/verifiable-credential#request-the-credential)

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      Please install our Yoti SDK and get familiar with our dynamic QR code.
   </div>
   <div class="alert-links"> 
      <a href="https://developers.yoti.com/yoti-app/install-the-sdk">Install the SDK</a>
           <a href="https://developers.yoti.com/yoti-app/generate-the-button#dynamic-qr">Dynamic QR code</a>
   </div>
</div>
{% /html %}

## Defining the credential

At the definition stage you will define:

- The name of the credential
- The format and structure of the credential - Yoti currently supports, Text (single line), JPEG, PNG and JSON object.
- Who can issue the credential
- Who can retrieve the credential

You will need to create the definition, using the Yoti SDK. This is a one-time process which will be used and referenced for every credential issuance. 

Once you have added the Yoti SDK dependency to your project, you can use it to build and send your request. See the code snippets below for examples of how to construct the request.

{% code %}
{% tab language="javascript" %}
COMING SOON
{% /tab %}
{% tab language="java" %}
COMING SOON
{% /tab %}
{% tab language="php" %}

{% /tab %}
{% tab language="python" %}
COMING SOON
{% /tab %}
{% tab language="csharp" %}
string json = JsonConvert.SerializeObject(deserializedObject);
byte[] httpContent = System.Text.Encoding.UTF8.GetBytes(jsonString);

var signedRequest = new RequestBuilder()
	.WithBaseUri(new Uri("https://api.yoti.com/api/v1/attribute-registry"))
	.WithEndpoint("/definitions")
	.WithHttpMethod(HttpMethod.Post)
	.WithHeader("X-Yoti-Auth-Id", _clientSdkId)
	.WithKeyPair(keyPair)
	.WithContent(httpContent)
	.Build();
{% /tab %}
{% tab language="go" %}
COMING SOON
{% /tab %}
{% tab language="ruby" %}
# COMING SOON
{% /tab %}
{% /code %}

{% table %}
| Parameter | Description | 
| ---- | ---- | 
| sdkId | sdkId is the SDK_ID found with your Yoti Hub Application | 
| keyPair | The PEM file which is found with your Yoti Hub Application. The PEM file is required to allow the SDK to perform the authentication with the Yoti API. | 
{% /table %}

**Example payload**

{% code %}
{% tab language="json" %}
{
  "name": "credential name",
  "mimeType": "application/json",
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
  "config": {
    "accessProperties": {
      "requestors": [],
      "publiclyAccessible": true
    },
    "localisationProperties": {
      "defaultLocalisation": {
        "locale": "en_GB",
        "value": "Example.com identifier"
      }
    },
    "issuanceProperties": {
      "maxCardinality": 1,
      "issuers": [
        {
          "domain": "example.com"
        }
      ],
      "issuanceURL": "https://www.example.com/get-identifier"
    },
    "displayProperties": {
      "displayValueMimeType": "text/plain",
    }
  }
}
{% /tab %}
{% /code %}

See below for explanation of example payload:

{% table %}
| Parameter | Description | Optional | 
| ---- | ---- | ---- | 
| Name | This is the name of the credential. This is what will appear on the users Yoti app. | N | 
| MimeType | This will declare what type of credential you want. We currently support:\n\ntext/plain, application/JSON, image/png, image/jpeg. | N | 
| Icon | This is the icon that will be presented to a user during the Yoti App share. It will also appear in the sharing receipts.\n\n\n\nThe icon must be at least 112px and smaller than 512kb. | N | 
| locales | A list of localisation values. The name will be the display name of the credential. InfoUri is optional and can be pointer to a page that has a description or more information about your credential | N | 
| Access properties | This is where you define who will be allowed to request the credential. \n\n\n\nThis should be in a fully qualified domain name format.\n\n\n\nIf publicly accessibility is 'True' then the credential can be requested publicly in their Yoti share. If you would like to control which organisations will request this credential please state 'False' here. | N | 
| Localisations properties | This is used to translate the name of the credential as it appears on the Yoti app. This should be in a fully qualified domain name format. \n\nNote: This functionality is not active yet. | Y | 
| Issuance properties | This is where you define who will be allowed to issue the credential. \n\nThis should be in a fully qualified domain name format. | N | 
| Issuance URL | Here you can provide a URL for information on how to obtain the credential. | Y | 
| displayProperties | Customisation of the credential will be configured here. \n\nNote: This functionality is not active yet. | Y | 
{% /table %}

By supplying the credential in the format of a JSON object, this will allow you to bundle multiple pieces of information together in a single credential request. As an example, you could ask for the credential Employee Number. If this is supplied via a JSON object, within that credential can also contain various other bits of information such as name, email address, access level etc.

**Example response**

{% code %}
{% tab language="json" %}
{
  "id": "uuid"
}
{% /tab %}
{% /code %}

---

## Issuing a credential

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

const shareUrlResult = yotiClient.createShareUrl(dynamicScenario);
{% /tab %}
{% tab language="java" %}
Date date = new Date();
Calendar calendar = Calendar.getInstance();
calendar.setTime(date);
calendar.add(Calendar.HOUR_OF_DAY, 5);
 
Date expiryDate = calendar.getTime();
 
ThirdPartyAttributeExtensionBuilder thirdPartyAttributeExtensionBuilder = ExtensionBuilderFactory.newInstance()
    .createThirdPartyAttributeExtensionBuilder();
 
Extension<ThirdPartyAttributeContent> thirdPartyAttributeExtension = thirdPartyAttributeExtensionBuilder
    .withExpiryDate(expiryDate)
    .withDefinition("com.example.someAttribute")
    .build();
 
DynamicPolicy dynamicPolicy = new SimpleDynamicPolicyBuilder()
    .withWantedRememberMe(true)
    .build();
 
DynamicScenario dynamicScenario = new SimpleDynamicScenarioBuilder()
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

{% table %}
| Parameter | Description | 
| ---- | ---- | 
| withDefinition() | This value will be your credential name “com.example.someAttribute” | 
| withExpiryDate() | The expired date indicates by when the credential should be issued by. If the credential is not issued by that time, the issuance request will be automatically cancelled.\n\n\n\nIt conforms to RFC3339 (e.g.: 2006-01-02T22:04:05.123Z) | 
| Dynamic policy | This is where you define all your [attributes](https://developers.yoti.com/yoti/knowledge-base-hub#general-attributes) you wish to retrieve from the user. You may set source constraints to ensure only an individual can only share data from a particular document. The soft preference set to 'false' will ensure this is enforced. Please see [dynamic QR code](https://developers.yoti.com/yoti-app/generate-the-button#dynamic-qr) section for more details on this. | 
| Dynamic scenario | Build the scenario with the third-party extension request and share policy request. | 
{% /table %}

### Get credential issuance details

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
activityDetails = client.getActivityDetails(token);

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

### Request for credential to be issued

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
 
SignedRequest signedRequest = SignedRequestBuilder.newInstance()
            .withKeyPair(YOUR_KEY_PAIR)
            .withBaseUrl("https://api.yoti.com/api/v1/attribute-registry")
            .withEndpoint("/attributes")
            .withHttpMethod("POST")
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
{% /code %}

The user will now have the credential.

---

## Request the credential

You will then need to generate a QR code to retrieve the newly-issued credential. The share result will contain the QR code URL to present the [dynamic QR code](https://developers.yoti.com/yoti-app/generate-the-button#dynamic-qr).

{% code %}
{% tab language="javascript" %}
const dynamicPolicy = new DynamicPolicyBuilder()
    .withWantedAttributeByName('com.example.someAttribute')
    .build();

const dynamicScenario = (new DynamicScenarioBuilder())
    .withCallbackEndpoint('/account/connect')
    .withPolicy(dynamicPolicy)
    .build();

const shareUrlResult = yotiClient.createShareUrl(dynamicScenario);
{% /tab %}
{% tab language="java" %}
DynamicPolicy dynamicPolicy = new SimpleDynamicPolicyBuilder()
    .withWantedAttribute(false, "com.example.someAttribute")
    .build();
 
DynamicScenario dynamicScenario = new SimpleDynamicScenarioBuilder()
    .withCallbackEndpoint("/account/connect")
    .withPolicy(dynamicPolicy)
    .build();
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\ShareUrl\DynamicScenarioBuilder;
use Yoti\ShareUrl\Policy\DynamicPolicyBuilder;

$dynamicPolicy = (new DynamicPolicyBuilder())
    ->withWantedAttributeByName('com.example.someAttribute')
    ->build();

$dynamicScenario = (new DynamicScenarioBuilder())
    ->withCallbackEndpoint('/account/connect')
    ->withPolicy($dynamicPolicy)
    ->build();

$shareUrlResult = $yotiClient->createShareUrl($dynamicScenario);
{% /tab %}
{% tab language="python" %}
from yoti_python_sdk import Client

from yoti_python_sdk.dynamic_sharing_service import (
    create_share_url,
    DynamicScenarioBuilder,
)

from yoti_python_sdk.dynamic_sharing_service.policy.dynamic_policy_builder import (
    DynamicPolicyBuilder,
)

client = Client("CLIENT_SDK_ID", "/path/to/key.pem")

policy = (
    DynamicPolicyBuilder()
    .with_wanted_attribute_by_name("com.example.someAttribute")
    .build()
)

scenario = (
    DynamicScenarioBuilder()
    .with_callback_endpoint("/account/connect")
    .with_policy(policy)
    .build()
)

share_url_result = share = create_share_url(client, scenario)
{% /tab %}
{% tab language="csharp" %}
DynamicPolicy dynamicPolicy = new DynamicPolicyBuilder()
   .WithWantedAttribute(_thirdPartyAttributeName)
   .Build();

DynamicScenario dynamicScenario = new DynamicScenarioBuilder()
	.WithCallbackEndpoint("/account/connect")
	.WithPolicy(dynamicPolicy)
	.Build();

ShareUrlResult shareUrlResult = yotiClient.CreateShareUrl(dynamicScenario);
{% /tab %}
{% tab language="go" %}
policy, err := (&dynamic.PolicyBuilder{}).
	WithWantedAttributeByName("com.example.someAttribute").
	Build()

if err != nil {
	panic(err)
}

var scenario dynamic.Scenario
scenario, err = (&dynamic.ScenarioBuilder{}).
	WithCallbackEndpoint("/account/connect").
	WithPolicy(policy).
	Build()

if err != nil {
	panic(err)
}

var shareUrlResult dynamic.ShareURL
shareUrlResult, err = client.CreateShareURL(&scenario)
{% /tab %}
{% tab language="ruby" %}
policy = Yoti::DynamicSharingService::DynamicPolicy
         .builder
         .with_wanted_attribute_by_name('com.example.someAttribute')
         .build

scenario = Yoti::DynamicSharingService::DynamicScenario
           .builder
           .with_callback_endpoint('/account/connect')
           .with_policy(policy)
           .build

share_url_result = Yoti::DynamicSharingService.create_share_url(scenario)
{% /tab %}
{% /code %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
        To generate your dynamic QR code on your front end you will need the shareURL and SDK ID from your application.
    </div>
    <div class="alert-links"> 
   </div>
</div>
{% /html %}

---

## Retrieving an credential

Once the user has scanned the Yoti QR code, Yoti will perform a GET request to the defined call-back URL, passing a token as a query string parameter, any additional relying party defined query parameters will also be passed here.

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      Please get familiar with our user profile service with the Yoti App.
   </div>
   <div class="alert-links"> 
           <a href="https://developers.yoti.com/yoti/web-integration#retrieve-a-profile">Retrieve a profile</a>
   </div>
</div>
{% /html %}

{% code %}
{% tab language="javascript" %}
COMING SOON
{% /tab %}
{% tab language="java" %}
COMING SOON
{% /tab %}
{% tab language="php" %}
COMING SOON
{% /tab %}
{% tab language="python" %}
COMING SOON
{% /tab %}
{% tab language="csharp" %}
profile.GetAttributeByName<string>(name: "_thirdPartyAttributeName"); //text/string
profile.GetAttributeByName<Dictionary<string, JToken>>(name: "_thirdPartyAttributeName"); //application/json
profile.GetAttributeByName<PngImage>(name: "_thirdPartyAttributeName"); //image/png
profile.GetAttributeByName<JpegImage>(name: "_thirdPartyAttributeName"); //image/jpeg
profile.GetAttributeByName<DateTime>(name: "_thirdPartyAttributeName"); //DateTime
profile.GetAttributeByName<int>(name: "_thirdPartyAttributeName"); //integer
{% /tab %}
{% tab language="go" %}
COMING SOON
{% /tab %}
{% tab language="ruby" %}
COMING SOON
{% /tab %}
{% /code %}

---

## Updating a credential

You can update an individual users credential by overriding the value and using the issuance token associated to the user.  This requires no interaction from the user and will automatically update the Yoti app.

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
 
SignedRequest signedRequest = SignedRequestBuilder.newInstance()
            .withKeyPair(YOUR_KEY_PAIR)
            .withBaseUrl("https://api.yoti.com/api/v1/attribute-registry")
            .withEndpoint("/attribute/update")
            .withHttpMethod("PUT")
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

---

## Revoking a credential

You can revoke a credential from a users profile using the issuance token.  This requires no interaction from the user and will automatically update the Yoti app. The user will no longer be able to share or use the Yoti credential.

{% code %}
{% tab language="javascript" %}
const payload = new Payload({
    issuance_token: attributeIssuanceDetails.getToken(),
    name: 'com.example.someAttribute',
});

const request = new RequestBuilder()
    .withBaseUrl('https://api.yoti.com/api/v1/attribute-registry')
    .withEndpoint('/attribute/revoke')
    .withPemString('PEM_CONTENT')
    .withHeader('X-Yoti-Auth-Id', 'CLIENT_SDK_ID')
    .withMethod('PUT')
    .withPayload(payload)
    .build();

const response = await request.execute();
{% /tab %}
{% tab language="java" %}
byte[] payload = ...; // Payload is JSON converted to byte array
 
SignedRequest signedRequest = SignedRequestBuilder.newInstance()
            .withKeyPair(YOUR_KEY_PAIR)
            .withBaseUrl("https://api.yoti.com/api/v1/attribute-registry")
            .withEndpoint("/attribute/revoke")
            .withHttpMethod("PUT")
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
]);

$request = (new RequestBuilder())
    ->withBaseUrl('https://api.yoti.com/api/v1/attribute-registry')
    ->withEndpoint("/attribute/revoke")
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
}

payload_string = json.dumps(payload_data).encode()

signed_request = (
    SignedRequest
    .builder()
    .with_pem_file("/path/to/key.pem")
    .with_base_url("https://api.yoti.com/api/v1/attribute-registry")
    .with_endpoint("/attribute/revoke")
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

string json = JsonConvert.SerializeObject(new
{
	issuance_token = _issuanceToken,
	name = _thirdPartyAttributeName
});

byte[] httpContent = System.Text.Encoding.UTF8.GetBytes(json);

var signedRequest = new RequestBuilder()
	.WithBaseUri(new Uri("https://api.yoti.com/api/v1/attribute-registry"))
	.WithEndpoint("/attribute/revoke")
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
}

body, err := json.Marshal(Payload{
	Token: issuingAttributes.Token(),
	Name:  "com.example.someAttribute",
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
	Endpoint:   "/attribute/revoke",
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
  name: 'com.example.someAttribute'
}

request = Yoti::Request
          .builder
          .with_base_url('https://api.yoti.com/api/v1/attribute-registry')
          .with_http_method('PUT')
          .with_endpoint('attribute/revoke')
          .with_payload(payload)
          .with_header('X-Yoti-Auth-Id', Yoti.configuration.client_sdk_id)
          .build

response = request.execute
{% /tab %}
{% /code %}