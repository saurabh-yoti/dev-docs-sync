---
type: page
title: Reusable Digital ID
listed: true
slug: reusable-digital-id
description: 
index_title: Reusable Digital ID
hidden: 
keywords: 
tags: 
---

#### Install the SDK

Once you have added the Yoti SDK dependency to your project, it’s time to initialise a Yoti client as shown in the code snippet below.

Once you have a working button, you can move on to installing the SDK.

To successfully integrate you will need the following information about your application from Yoti Hub:

- SDK ID
- Your application key pair

The Yoti SDKs are available via popular dependency management systems. Further details can be found on the pages of the specific projects.

To install the Yoti SDK:

{% code %}
{% tab language="javascript" %}
npm install -S -E yoti
{% /tab %}
{% tab language="java" %}
// If you are using Maven, add the following dependency:
<dependency>
    <groupId>com.yoti</groupId>
    <artifactId>yoti-sdk-api</artifactId>
    <version>3.5.0</version>
</dependency>

// If you are using Gradle, add the following dependency:
compile group: 'com.yoti', name: 'yoti-sdk-api', version: '3.5.0'
{% /tab %}
{% tab language="php" %}
// Get the Yoti PHP SDK library via a Composer package
composer require yoti/yoti-php-sdk
{% /tab %}
{% tab language="csharp" %}
// To install the Yoti NuGet package you will need to install NuGet.
// To import the latest Yoti SDK into your project, enter the following
// command from NuGet Package Manager Console in Visual Studio:

Install-Package Yoti

// For other installation methods, see https://www.nuget.org/packages/Yoti
{% /tab %}
{% tab language="go" %}
// As of version 2.4.0, modules are used. This means it's not necessary to get a copy or fetch all dependencies 
// as instructed below, as the Go toolchain will fetch them as necessary. 
// You can simply add a `require github.com/getyoti/yoti-go-sdk/v3` to go.mod.
// To download and install the Yoti SDK and its dependencies, run the following command from your terminal:

go get "github.com/getyoti/yoti-go-sdk/v3”
{% /tab %}
{% /code %}

Once you have added the Yoti SDK dependency to your project, it’s time to initialise a Yoti client as shown in the code snippet below.

{% code %}
{% tab language="javascript" %}
const yoti = require('yoti')
const CLIENT_SDK_ID = 'YOTI_CLIENT_SDK_ID'
const PEM_PATH = 'YOTI_KEY_FILE_PATH'
const PEM_KEY = fs.readFileSync(PEM_PATH)
// For SDK version < 3
const yotiClient = new yoti(CLIENT_SDK_ID, PEM)
// For SDK version >= 3
const yotiClient = new yoti.Client(CLIENT_SDK_ID, PEM_KEY)
{% /tab %}
{% tab language="java" %}
import java.io.File;
import com.yoti.api.client.ActivityDetails;
import com.yoti.api.client.Date;
import com.yoti.api.client.FileKeyPairSource;
import com.yoti.api.client.HumanProfile;
import com.yoti.api.client.HumanProfile.Gender;
import com.yoti.api.client.Image;
import com.yoti.api.client.YotiClient;
import com.yoti.api.client.YotiClientBuilder;

YotiClient client = YotiClient.builder()
    .withClientSdkId(<YOTI_CLIENT_SDK_ID>)
    .withKeyPair(FileKeyPairSource.fromFile(new File("<YOTI_KEY_FILE_PATH>")))
    .build();
{% /tab %}
{% tab language="php" %}
<?php
require_once './vendor/autoload.php';
$client = new \Yoti\YotiClient('YOTI_CLIENT_SDK_ID', 'YOTI_KEY_FILE_PATH');
{% /tab %}
{% tab language="csharp" %}
const string SDK_ID = "YOTI_CLIENT_SDK_ID";
const string PEM_PATH = "YOTI_KEY_FILE_PATH";

var privateKeyStream = System.IO.File.OpenText(PEM_PATH);
var yotiClient = new YotiClient(SDK_ID, privateKeyStream);
{% /tab %}
{% tab language="go" %}
sdkID := "YOTI_CLIENT_SDK_ID";
key, _ := ioutil.ReadFile("YOTI_KEY_FILE_PATH")

client, err := yoti.NewClient(sdkId, key)
{% /tab %}
{% /code %}

---

## Using Yoti SDK's

The description on how to use the SDK can be found here:

- [Create button](https://developers.yoti.com/digital-id/createbutton#dynamic-qr)
- [Retrieve the profile](https://developers.yoti.com/digital-id/retrieve-the-profile)

Please read the above for a full description and understanding, below we’ll provide examples on how those requests will expose the new functionality.

{% code %}
{% tab language="javascript" %}
const identityProfileRequirements = 
      {
        trust_framework: 'UK_TFIDA',
              scheme: {
                type: 'DBS',
                objective: 'STANDARD',
              }
      };

const subject = 
      {
        subject_id: 'subject_id_string',
      };

const dynamicPolicy = new Yoti.DynamicPolicyBuilder()
    .withIdentityProfileRequirements(identityProfileRequirements)
    .build();


const dynamicScenario = new Yoti.DynamicScenarioBuilder()
    .withCallbackEndpoint("/your-callback")
    .withPolicy(dynamicPolicy)
    .withSubject(subject)
    .build();

async function getShareUrl() {
    const shareUrlResult = await yotiClient.createShareUrl(dynamicScenario);
    const shareUrl = shareUrlResult.getShareUrl();
    return shareUrl;
}
{% /tab %}
{% tab language="java" %}
JSONObject subject = new JSONObject();
subject.put("subject_id", "subject_id_string");

JSONObject scheme = new JSONObject();
scheme.put("type", "DBS");
scheme.put("objective", "STANDARD");

JSONObject identityProfileRequirements = new JSONObject();
identityProfileRequirements.put("trust_framework", "UK_TFIDA");
identityProfileRequirements.put("scheme", scheme);

DynamicPolicy dynamicPolicy = DynamicPolicy.builder()
                                           .withIdentityProfile(identityProfileRequirements)
                                           .build();

DynamicScenario dynamicScenario = DynamicScenario.builder()
                                             .withCallbackEndpoint("/your-callback")
                                             .withSubject(subject)
                                             .withPolicy(dynamicPolicy)
                                             .build();

private String getShareUrl() {
  	String shareUrl = client.createShareUrl(dynamicScenario).getUrl();
  	return shareUrl;
}
{% /tab %}
{% tab language="php" %}
$identityProfileSample = (object)[
  'trust_framework' => 'UK_TFIDA',
  'scheme' => [
    'type' => 'DBS',
    'objective' => 'STANDARD'
  ]
];

$subjectSample = (object)[
  'subject_id' => 'SOME_STRING'
];

$dynamicPolicy = (new DynamicPolicyBuilder())
  ->withIdentityProfileRequirements($identityProfileSample)
  ->build();

$dynamicScenario = (new DynamicScenarioBuilder())
  ->withCallbackEndpoint("/your-callback")
  ->withPolicy($dynamicPolicy)
  ->withSubject($subjectSample)
  ->build();

function getShareUrl(b) {
  $shareUrl = $client->createShareUrl($dynamicScenario)->getShareUrl();
  return $$shareUrl;
}
{% /tab %}
{% tab language="csharp" %}
DynamicPolicy dynamicPolicy = new DynamicPolicyBuilder()
.WithIdentityProfileRequirements(new { 
	trust_framework = "UK_TFIDA",
	scheme = new
	{
		type = "DBS",
		objective = "STANDARD"
	}
}).Build();

DynamicScenario dynamicScenario = new DynamicScenarioBuilder()
.WithCallbackEndpoint("/your-callback")  
.WithPolicy(dynamicPolicy)
.WithSubject(new {
	subject_id = "some_subject_id_string"
})
.Build();
{% /tab %}
{% tab language="go" %}
identityProfile := []byte(`{
		"trust_framework": "UK_TFIDA",
		"scheme": {
			"type":      "DBS",
			"objective": "BASIC"
		}
	}`)

policy, err := (&dynamic.PolicyBuilder{}).
		WithIdentityProfileRequirements(identityProfile).
		Build()

subject := []byte(`{
		"subject_id": "my_subject_id"
	}`)

scenario, err := (&dynamic.ScenarioBuilder{}).
		WithPolicy(policy).
		WithSubject(subject).
		WithCallbackEndpoint("/your-callback").Build()

share, err := client.CreateShareURL(&scenario)
{% /tab %}
{% /code %}

### Identity Profile Requirements Explained

{% table widths="203,160" %}
| Field | Value | Description | 
| ---- | ---- | ---- | 
| trust_framework | String | Defines under which trust framework this identity profile should be verified. Enum: UK_TFIDA | 
| scheme | Object | Defines which scheme this identity profile should satisfy. The scheme must be supported by the specified trust framework otherwise the request is considered invalid. | 
| type | String | Defines which scheme this identity profile should satisfy. Enum: DBS, RTW, RTR, DBS_RTW | 
| objective | String | Defines the objective to be achieved for the particular scheme. It must be provided for those schemes where it is mandatory. Example, this is mandatory for DBS and the possible values are: ”BASIC”, “STANDARD”, “ENHANCED”. | 
{% /table %}

#### Subject Id Explained

{% table %}
| Field | Description | 
| ---- | ---- | 
| subject_id | allows the RP to track a subject across session creation and session retrieval | 
{% /table %}

The dynamicScenario can be used to get a shareURL which will be used by the Yoti scripts to generate a Yoti QR code.

---

## Client side view

Once you have your share URL you can send it to the frontend for it to be rendered in a Yoti QR code. Please see example below using the modal QR code.

{% code %}
{% tab language="html" %}
<!-- Simple Button Generation -->

<head>
  <script src="https://www.yoti.com/share/client/"></script>
</head>

<body>
  <!-- Yoti element will be rendered inside this DOM node -->
  <div id="xxx"></div>

  <!-- This script snippet will also be required in your HTML body -->
  <script>
    window.Yoti.Share.init({
      elements: [
        {
          domId: "xxx",
          shareUrl: "getShareUrl",
          clientSdkId: "xxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
          displayLearnMoreLink: true,
          skinId: "digital-id-uk"
        }
      ]
    });
  </script>
</body>
{% /tab %}
{% /code %}

---

## Query parameters

You can append query params to the landing page URL that displays the Yoti button. These will be added to the callback URL.

For example if you load the landing page containing the Yoti button as follows:

[https://example.com/?iso=test&user_id=6667](https://example.com/?iso=test&amp;user_id=6667)

The query parameters (iso=test&user_id=6667) will be returned in the callback URL.

---

## Response

Further details on how to use the SDK to get shared attributes can be found here:

- [Retrieve the profile](https://developers.yoti.com/digital-id/retrieve-the-profile)

In case of a successful transaction, once the profile is retrieved, the identity profile report can be accessed.

{% code %}
{% tab language="javascript" %}
yotiClient.getActivityDetails(oneTimeUseToken)
  .then((activityDetails) => {
    const rememberMeId = activityDetails.getRememberMeId();
    const parentRememberMeId = activityDetails.getParentRememberMeId();
    const receiptId = activityDetails.getReceiptId();
    const timestamp = activityDetails.getTimestamp();
 
    const profile = activityDetails.getProfile();
    const outcome = activityDetails.getOutcome();
    
    // identityProfileReport is the JSON object containing identity assertion and
    // verification report.
    const identityProfileReport = profile.getIdentityProfileReport().getValue(); 
})
{% /tab %}
{% tab language="java" %}
HumanProfile profile = yotiClient.getActivityDetails(<sharingToken>).getUserProfile();

Attribute<Map<String, Object>> identityProfileReport = profile.getIdentityProfileReport();

Map<String, Object> valueRepresentation = identityProfileReport.getValue();
{% /tab %}
{% tab language="php" %}
$activityDetails = $client->getActivityDetails($oneTimeUseToken);
rememberMeId = $activityDetails->getRememberMeId();
parentRememberMeId = $activityDetails->getParentRememberMeId();
$profile = $activityDetails->getProfile();

$identityProfileReport = $profile->getIdentityProfileReport();
{% /tab %}
{% tab language="csharp" %}
ActivityDetails activityDetails = yotiClient.GetActivityDetails(oneTimeUseToken);
YotiProfile profile = activityDetails.Profile;
YotiAttribute<Dictionary<string, JToken>> identityProfileReport = profile.IdentityProfileReport
{% /tab %}
{% tab language="go" %}
activityDetails, err := client.GetActivityDetails(yotiOneTimeUseToken)
userProfile := activityDetails.UserProfile

selfie := userProfile.Selfie()
var base64URL string
if selfie != nil {
  base64URL = selfie.Value().Base64URL()
}

dob, err := userProfile.DateOfBirth()
var dateOfBirthString string
if dob != nil {
  dateOfBirthString = dob.Value().String()
}

givenNames := userProfile.GivenNames().Value()
familyName := userProfile.FamilyName().Value()
fullName := userProfile.FullName().Value()
mobileNumber := userProfile.MobileNumber().Value()
emailAddress := userProfile.EmailAddress().Value()

identityProfileReport := userProfile.IdentityProfileReport().Value()
{% /tab %}
{% /code %}

The identity profile report contains the verified identity details and the verification report that certifies how the identity was verified and how the verification level was achieved.

---

## User experience

There will be instances where we have exhausted all available ‘routes’ to help a user achieve compliance with the requested scheme and not been successful.  In these cases the user will not be able to complete the ‘share’, and will be shown a screen which informs them that they cannot continue with the journey in our app. This will trigger a failure sharing scenario, responding back with an associated error code.