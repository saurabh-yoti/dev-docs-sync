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

## Install the SDK

Once you have added the Yoti SDK dependency to your project, it’s time to initialise a Yoti client as shown in the code snippet below.

Once you have a working Yoti QR/button, you can move on to installing the SDK.

To successfully integrate you will need the following information about your application from Yoti Hub:

- SDK ID
- Your application key pair

The Yoti SDKs are available via popular dependency management systems. Further details can be found on the pages of the specific projects.

To install the Yoti SDK:

{% code %}
{% tab language="javascript" title="Node.js" %}
// Get the Yoti Node SDK library via the NPM registry
npm install -S -E yoti
{% /tab %}
{% tab language="java" %}
// If you are using Maven, add the following dependency:
<dependency>
    <groupId>com.yoti</groupId>
    <artifactId>yoti-sdk-api</artifactId>
    <version>3.8.0</version>
</dependency>

// If you are using Gradle, add the following dependency:
compile group: 'com.yoti', name: 'yoti-sdk-api', version: '3.8.0'
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
// Simply add this as an import:
import "github.com/getyoti/yoti-go-sdk/v3"

// Or add the following line to your go.mod file
require github.com/getyoti/yoti-go-sdk/v3 v3.12.0
{% /tab %}
{% /code %}

Once you have added the Yoti SDK dependency to your project, you can initialise the Yoti Digital Identity Client as shown below:

{% code %}
{% tab language="javascript" title="Node.js" %}
const Yoti = require('yoti')
const CLIENT_SDK_ID = 'YOTI_CLIENT_SDK_ID'
const PEM_PATH = 'YOTI_KEY_FILE_PATH'
const PEM_KEY = fs.readFileSync(PEM_PATH)

const yotiClient = new Yoti.DigitalIdentityClient(CLIENT_SDK_ID, PEM_KEY)
{% /tab %}
{% tab language="java" %}
import java.io.File;
import com.yoti.api.client.FileKeyPairSource;
import com.yoti.api.client.DigitalIdentityClient;

DigitalIdentityClient client = DigitalIdentityClient.builder()
    .withClientSdkId("<YOTI_CLIENT_SDK_ID>")
    .withKeyPairSource(FileKeyPairSource.fromFile(new File("<YOTI_KEY_FILE_PATH>")))
    .build();
}
{% /tab %}
{% tab language="php" %}
<?php
require_once './vendor/autoload.php';

$client = new \Yoti\DigitalIdentityClient('YOTI_CLIENT_SDK_ID', 'YOTI_KEY_FILE_PATH');
{% /tab %}
{% tab language="csharp" %}
const string SDK_ID = "YOTI_CLIENT_SDK_ID";
const string PEM_PATH = "YOTI_KEY_FILE_PATH";

var privateKeyStream = System.IO.File.OpenText(PEM_PATH);
var yotiClient = new YotiDigitalIdentityClient(SDK_ID, privateKeyStream);
{% /tab %}
{% tab language="go" %}
sdkID := "YOTI_CLIENT_SDK_ID";
pemKey, _ := ioutil.ReadFile("YOTI_KEY_FILE_PATH")

client, err := yoti.NewDigitalIdentityClient(sdkId, pemKey)
if err != nil {
    return nil, err
}
{% /tab %}
{% /code %}

---

## Using Yoti SDK

The description on how to use the SDK can be found here:

- [auto$](/digital-id/create-share-session)
- [auto$](/digital-id/retrieve-the-profile)

Please read the above for a full description and understanding, below we’ll provide examples on how those requests will expose the new functionality.

{% code %}
{% tab language="javascript" title="Node.js" %}
const identityProfileRequirements = {
  trust_framework: 'UK_TFIDA',
  scheme: {
    type: 'DBS',
    objective: 'STANDARD',
  }
};

const subject = {
		subject_id: 'subject_id_string',
};

const policy = new Yoti.PolicyBuilder()
    .withIdentityProfileRequirements(identityProfileRequirements)
    .build();

const notification = new Yoti.ShareSessionNotificationBuilder()
		.withUrl("notification-webhook")
		.withMethod("POST")
		.build();

const shareSessionConfig = new Yoti.ShareSessionConfigurationBuilder()
    .withRedirectUri("/your-callback-url")
    .withSubject(subject)
    .withPolicy(policy)
		.withNotification(notification)
    .build();

async function getShareSession() {
    const shareSession = await yotiClient.createShareSession(shareSessionConfig);
  	return shareSession;
}
{% /tab %}
{% tab language="java" %}
JSONObject scheme = new JSONObject()
    .put("type", "DBS")
    .put("objective", "STANDARD");

JSONObject identityProfileRequirements = new JSONObject()
    .put("trust_framework", "UK_TFIDA")
    .put("scheme", scheme);

JSONObject subject = new JSONObject()
    .put("subject_id", "subject_id_string");

Policy policy = Policy.builder()
    .withIdentityProfileRequirements(identityProfileRequirements)
    .build();

ShareSessionNotification notification = ShareSessionNotification.builder("notification-webhook")
    .withMethod("POST")
    .build();

ShareSessionRequest shareSessionConfig = ShareSessionRequest.builder()
  	.withRedirectUri("/your-callback-url")
  	.withSubject(subject)
    .withPolicy(policy)
  	.withNotification(notification)
    .build();

private ShareSession createShareSession() {
    try {
        ShareSession shareSession = client.createShareSession(shareSessionConfig);
        return shareSession;
    } catch (DigitalIdentityException e) {
        LOG.error(e.getMessage());
    }
    return null;
}
{% /tab %}
{% tab language="php" %}
$identityProfileRequirements = (object)[
  'trust_framework' => 'UK_TFIDA',
  'scheme' => [
    'type' => 'DBS',
    'objective' => 'STANDARD'
  ]
];

$subject = (object)[
  'subject_id' => 'subject_id_string'
];

$policy = (new PolicyBuilder())
    ->withIdentityProfileRequirements($identityProfileRequirements)
    ->build();

$notification = (new ShareSessionNotificationBuilder())
		->withUrl("notification-webhook")
		->withMethod("POST")
		->build();

$shareSessionConfig = (new ShareSessionRequestBuilder())
  	->withRedirectUri("your-callback-url")
    ->withSubject($subject)
    ->withPolicy($policy)
  	->withNotification($notification)
    ->build();

function getShareSession() {
  	$shareSession = $client->createShareSession($shareSessionConfig);
  	return $shareSession;
}
{% /tab %}
{% tab language="csharp" %}
var identityProfileRequirements = new { 
	trust_framework = "UK_TFIDA",
	scheme = new
	{
		type = "DBS",
		objective = "STANDARD"
	}
};

var subject = new {
	subject_id = "subject_id_string"
};

YotiPolicy policy = new YotiPolicyBuilder()
  .WithIdentityProfileRequirements(identityProfileRequirements)
  .Build();

var notification = new Notification
{
  Headers = { },
  Url = "notification-webhook",
  Method = "POST",
  VerifyTls = true
};

ShareSessionConfiguration shareSessionConfig = new ShareSessionConfigurationBuilder()
  .WithRedirectUri("/your-callback-url")
  .WithSubject(subject)
  .WithPolicy(policy)
  .WithNotification(notification)
  .Build();

ShareSession shareSession = yotiClient.CreateShareSession(shareSessionConfig);
{% /tab %}
{% tab language="go" %}
identityProfile := []byte(`{
		"trust_framework": "UK_TFIDA",
		"scheme": {
			"type":      "DBS",
			"objective": "STANDARD"
		}
	}`)

subject := []byte(`{
		"subject_id": "subject_id_string"
	}`)

policy := (&digitalidentity.PolicyBuilder{})
	.WithIdentityProfileRequirements(identityProfile)
	.Build()

notification := (&digitalidentity.ShareSessionNotification{})
	.WithUrl("notification-webhook")
  .WithMethod("POST")
  .Build()

shareSessionConfig := (&digitalidentity.ShareSessionBuilder{})
  .WithRedirectUri("/your-callback-url")
  .WithSubject(subject)
	.WithPolicy(policy)
  .WithNotification(notification)
  .Build()

shareSession, err := client.CreateShareSession(shareSessionConfig)
if err != nil {
  return nil, err
}
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

{% table widths="" %}
| Field | Description | 
| ---- | ---- | 
| subject_id | allows the RP to track a subject across session creation and session retrieval | 
{% /table %}

The dynamicScenario can be used to get a shareURL which will be used by the Yoti scripts to generate a Yoti QR code.

---

## Client side view

Once you have the Share session, you can use it on the frontend for it to render a Yoti QR code. Please see example below using the modal QR code.

{% code %}
{% tab language="html" %}
<head>
  <script src="https://www.yoti.com/share/client/v2"></script>
</head>

<body>
  <!-- Yoti element will be rendered inside this DOM node -->
  <div id="xxx"></div>

  <!-- This script snippet will also be required in your HTML body -->
  <script>
    async function onSessionIdResolver() {
      // Make a call to your backend, and return a 'sessionId'
      const response = await fetch('http://localhost:3000/sessions', { method: 'POST' });
      const data = await response.json();
      return data.sessionId;
    }

    function onErrorListener(...data) {
      console.warn('onErrorListener:', ...data);
    }

    const loadYoti = async () => {
      const { Yoti } = window;
      if (Yoti) {
        console.info('Waiting for Yoti...');
        await Yoti.ready()
        console.info('Yoti is now ready');
      } else {
        console.error('Yoti client was not found!');
      }
    }

    const createYotiWebShare = async () => {
      const { Yoti } = window;
      if (Yoti) {
        await Yoti.createWebShare({
          name: 'yoti-share',
          domId: 'xxx',
          sdkId: 'xxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx',
          skinId: 'digital-id-uk',
          hooks: {
            sessionIdResolver: onSessionIdResolver,
            errorListener: onErrorListener
          }
        })
      }
    }

    const start = async () => {
      await loadYoti();
      await createYotiWebShare();
    }

    start().catch((e) => console.error(`Could not create Yoti WebShare: `, e));
  </script>
</body>
{% /tab %}
{% /code %}

---

## Query parameters

You can append query params to the landing page URL that displays the Yoti QR/button. These will be added to the redirect URI.

For example if you load the landing page containing the Yoti button as follows:

[https://example.com/?iso=test&user_id=6667](https://example.com/?iso=test&amp;user_id=6667)

The query parameters (iso=test&user_id=6667) will be returned in the callback URL.

---

## Response

Further details on how to use the SDK to get shared attributes can be found here:

- [auto$](/digital-id/retrieve-the-profile)

In case of a successful transaction, once the profile is retrieved, the identity profile report can be accessed.

{% code %}
{% tab language="javascript" title="Node.js" %}
yotiClient.getShareReceipt(receiptId)
  .then((shareReceipt) => {
  	const sessionId = shareReceipt.getSessionId();
  	const rememberMeId = shareReceipt.getRememberMeId();
  	const parentRememberMeId = shareReceipt.getParentRememberMeId();

    const profile = shareReceipt.getProfile();
    const selfieImageData = profile.getSelfie().getValue();
    const base64SelfieUri = selfieImageData.getBase64Content();
  
  	const documentDetails = profile.getDocumentDetails().getValue();
    
  	const hasIdentityProfile = Boolean(profile.getIdentityProfileReport());
  	if (hasIdentityProfile) {
      const identityProfileReport = profile.getIdentityProfileReport().getValue();
    }
	})
{% /tab %}
{% tab language="java" %}
try {
  	Receipt shareReceipt = client.fetchShareReceipt(receiptId);
  
  	String sessionId = shareReceipt.getSessionId();
  	String rememberMeId = shareReceipt.getRememberMeId();
  	String parentRememberMeId = shareReceipt.getParentRememberMeId();

    HumanProfile profile = shareReceipt.getProfile();
  	Image selfieImageData = profile.getSelfie().getValue();
		String selfieBase64Content = selfieImageData.getBase64Content();
  
  	DocumentDetails documentDetails = profile.getDocumentDetails().getValue();
  
  	Attribute<Map<String, Object>> identityProfileReport = profile.getIdentityProfileReport();
  	Map<String, Object> valueRepresentation = identityProfileReport.getValue();
} catch (DigitalIdentityException e) {
  	LOG.error(e.getMessage());
}
{% /tab %}
{% tab language="php" %}
$shareReceipt = $client->fetchShareReceipt($receiptId);

$sessionId = $shareReceipt->getSessionId();
$rememberMeId = $shareReceipt->getRememberMeId();
$parentRememberMeId = $shareReceipt->getParentRememberMeId();

$profile = $shareReceipt->getProfile();
$selfieImageObj = $profile->getSelfie()->getValue();
$selfieImageBase64Content = $selfieImageObj->getBase64Content();

$documentDetails = $profile->getDocumentDetails()->getValue();

$identityProfileReport = $profile->getIdentityProfileReport()->getValue();
{% /tab %}
{% tab language="csharp" %}
ShareReceipt shareReceipt = yotiClient.GetShareReceipt(receiptId);

string sessionId = shareReceipt.SessionId;
string rememberMeId = shareReceipt.RememberMeId;
string parentRememberMeId = shareReceipt.ParentRememberMeId;


YotiProfile profile = shareReceipt.Profile;
Image selfie = profile.Selfie?.GetValue();
string selfieURI = profile.Selfie?.GetValue().GetBase64URI();

var documentDetails = profile.DocumentDetails.GetValue();

bool hasIdentityProfile = profile.IdentityProfileReport != null ? true : false;
if (hasIdentityProfile) {
	var identityProfileReport = profile.IdentityProfileReport.GetValue();
}
{% /tab %}
{% tab language="go" %}
shareReceipt, err := client.GetShareReceipt(receiptId)

sessionId := shareReceipt.SessionID
rememberMeID := shareReceipt.RememberMeID
parentRememberMeID := shareReceipt.ParentRememberMeID

profile := shareReceipt.UserContent.UserProfile
selfie := userProfile.Selfie()
selfieBase64URL := selfie.Value().Base64URL()

documentDetails = profile.DocumentDetails().Value();

identityProfileReport := userProfile.IdentityProfileReport().Value()
{% /tab %}
{% /code %}

The identity profile report contains the verified identity details and the verification report that certifies how the identity was verified and how the verification level was achieved.

---

## User experience

There will be instances where we have exhausted all available ‘routes’ to help a user achieve compliance with the requested scheme and not been successful.  In these cases the user will not be able to complete the ‘share’, and will be shown a screen which informs them that they cannot continue with the journey in our app. This will trigger a failure sharing scenario, responding back with an associated error code.