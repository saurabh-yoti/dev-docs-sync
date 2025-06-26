---
type: page
title: Digital ID V2 SDK Migration
listed: true
slug: v2-sdk-migration
description: 
index_title: Digital ID V2 SDK Migration
hidden: 
keywords: 
tags: 
---

This acts as a short quick start guide for migrating from the original Digital ID SDK, to the new 'V2' SDK.

{% callout type="info" title="Info" %}
Scenarios created via the Hub are no longer compatible with the newly launched Digital ID SDK. To offer an improved user experience, we've transitioned to 'Sessions' which can provide granular session states throughout the entire user journey.

Should you require support on migrating from a scenario to the V2 SDK, or general support during the migration process, please get in touch through our [support website](https://support.yoti.com).
{% /callout %}

## Install the SDK

You will need to ensure the latest version of the Yoti backend SDK is installed.

{% code %}
{% tab language="javascript" %}
// Get the Yoti Node SDK library via the NPM registry
npm install -S -E yoti
{% /tab %}
{% tab language="java" %}
// If you are using Maven, add the following dependency:
<dependency>
    <groupId>com.yoti</groupId>
    <artifactId>yoti-sdk-api</artifactId>
    <version>3.7.0</version>
</dependency>

// If you are using Gradle, add the following dependency:
compile group: 'com.yoti', name: 'yoti-sdk-api', version: '3.7.0'
{% /tab %}
{% tab language="php" %}
// Get the Yoti PHP SDK library via a Composer package
composer require yoti/yoti-php-sdk
{% /tab %}
{% tab language="csharp" %}
// To install the Yoti NuGet package, you need to install NuGet Package Manager. After that, enter the following command in the console:

Install-Package Yoti

// For other installation methods, see https://www.nuget.org/packages/Yoti
{% /tab %}
{% tab language="go" %}
// Simply add this as an import:
import "github.com/getyoti/yoti-go-sdk/v3"

// Or add the following line to your go.mod file
require github.com/getyoti/yoti-go-sdk/v3 v3.10.0
{% /tab %}
{% /code %}

## Client Initialisation

The Class in the V1 client is referred to as Client.

{% code %}
{% tab language="javascript" %}
const Yoti = require('yoti')
const CLIENT_SDK_ID = 'YOTI_CLIENT_SDK_ID'
const PEM_PATH = 'YOTI_KEY_FILE_PATH'
const PEM_KEY = fs.readFileSync(PEM_PATH)
// For SDK version < 3
const yotiClient = new Yoti(CLIENT_SDK_ID, PEM)
// For SDK version >= 3
const yotiClient = new Yoti.Client(CLIENT_SDK_ID, PEM_KEY)
{% /tab %}
{% tab language="java" %}
import java.io.File;
import com.yoti.api.client.FileKeyPairSource;
import com.yoti.api.client.YotiClient;

YotiClient client = YotiClient.builder()
    .withClientSdkId("<YOTI_CLIENT_SDK_ID>")
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
pemKey, _ := ioutil.ReadFile("YOTI_KEY_FILE_PATH")

client, err := yoti.NewClient(sdkId, pemKey)
{% /tab %}
{% /code %}

This has now been renamed to the Digital Identity Client. Your current PEM Key and SDK ID are still valid. There's no obligation to generate a new set of keys, but you might consider doing so if you wish to segregate different instances.

{% code %}
{% tab language="javascript" %}
const Yoti = require('yoti')
const CLIENT_SDK_ID = 'YOTI_CLIENT_SDK_ID'
const PEM_PATH = 'YOTI_KEY_FILE_PATH'
const PEM_KEY = fs.readFileSync(PEM_PATH)

// For SDK version >= 3
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
{% /tab %}
{% /code %}

## Dynamic QR

The current SDK enables integrators to dynamically create policies, which are sets of requested attributes or schemes, during the sharing process. This offers a more flexible approach compared to having a static policy pre-configured in the Yoti Hub, or attempting to maintain multiple scenarios per policy.

### Creating a policy

A policy is used to define what attributes are requested from the user. You can use the builder to define what attributes are needed.

In the V1 API, you would create a dynamic policy like this:

{% code %}
{% tab language="javascript" %}
const requirements = {
  trust_framework: 'UK_TFIDA',
  scheme: {
    type: 'DBS_RTW',
    objective: 'ENHANCED',
  }
};

const dynamicPolicy = new Yoti.DynamicPolicyBuilder()
    // if you wish to carry out DBS and/or RTW check
    .withIdentityProfileRequirements(requirements)
    //using a predefined method to add an attribute
    .withFullName()
		.withEmail()
    //if you wish the user to prove it's them by taking a selfie on share
    .withSelfieAuthentication()
    .build();
{% /tab %}
{% tab language="java" %}
DynamicPolicy dynamicPolicy = DynamicPolicy.builder()
    //using a predefined method to add an attribute
    .withFullName()
  	.withEmail()
    //if you wish the user to prove it's them by taking a selfie on share
    .withSelfieAuthentication(true)
    .build();
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\ShareUrl\Policy\DynamicPolicyBuilder;

$dynamicPolicy = (new DynamicPolicyBuilder())
    //using a predefined method to add an attribute
    ->withFullName()
  	->withEmail()
    //if you wish the user to prove it's them by taking a selfie on share
    ->withSelfieAuthentication()
    ->build();
{% /tab %}
{% tab language="csharp" %}
var requirements = new { 
	trust_framework = "UK_TFIDA",
	scheme = new
	{
		type = "DBS_RTW",
		objective = "ENHANCED"
	}
};

DynamicPolicy dynamicPolicy = new DynamicPolicyBuilder()
  // if you wish to carry out DBS and/or RTW check
	.WithIdentityProfileRequirements(requirements)
  .withFullName()
  .withEmail()
  // if you wish the user to prove it's them by taking a selfie on share
  .withSelfieAuthentication()
	.Build();
{% /tab %}
{% tab language="go" %}
dynamicPolicy := (&dynamic.PolicyBuilder{})
	//using a predefined method to add an attribute
	.WithFullName()
	.WithEmail()
	//if you wish the user to prove it's them by taking a selfie on share
	.WithSelfieAuth()
	.Build()
{% /tab %}
{% /code %}

In the V2 API, you have to create a policy like this:

{% code %}
{% tab language="javascript" %}
const requirements = {
  trust_framework: 'UK_TFIDA',
  scheme: {
    type: 'DBS_RTW',
    objective: 'ENHANCED',
  }
};

const policy = new Yoti.PolicyBuilder()
		// if you wish to carry out DBS and/or RTW check
    .withIdentityProfileRequirements(requirements)
    //using a predefined method to add an attribute
    .withFullName()
		.withEmail()
    //if you wish the user to prove it's them by taking a selfie on share
    .withSelfieAuthentication()
    .build();
{% /tab %}
{% tab language="java" %}
Policy policy = Policy.builder()
    //using a predefined method to add an attribute
    .withFullName()
    .withEmail()
    //if you wish the user to prove it's them by taking a selfie on share
    .withSelfieAuthentication(true)
    .build();
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\Identity\Policy\PolicyBuilder;

$policy = (new PolicyBuilder())
    //using a predefined method to add an attribute
    ->withFullName()
  	->withEmail()
    //if you wish the user to prove it's them by taking a selfie on share
    ->withSelfieAuthentication()
    ->build();
{% /tab %}
{% tab language="csharp" %}
var requirements = new { 
	trust_framework = "UK_TFIDA",
	scheme = new
	{
		type = "DBS_RTW",
		objective = "ENHANCED"
	}
};

YotiPolicy policy = new YotiPolicyBuilder()
  // if you wish to carry out DBS and/or RTW check
	.WithIdentityProfileRequirements(requirements)
  .withFullName()
  .withEmail()
  // if you wish the user to prove it's them by taking a selfie on share
  .withSelfieAuthentication()
	.Build();
{% /tab %}
{% tab language="go" %}
policy := (&digitalidentity.PolicyBuilder{})
	//using a predefined method to add an attribute
	.WithFullName()
	.WithEmail()
	//if you wish the user to prove it's them by taking a selfie on share
	.WithSelfieAuth()
	.Build()
{% /tab %}
{% /code %}

### Specify a Scenario/Session request

The Scenario/Session request is built using:

- The policy.
- A callback/redirect URL for share completion. The provided URL is where the user will be redirected to  after the share is completed. A token or receiptId will be added to the URL. You can use this to retrieve the user profile from the share.
- Any extensions.

In the V1 API, you would specify a scenario:

{% code %}
{% tab language="javascript" %}
const subject = {
		subject_id: 'subject_id_string',
};

const dynamicScenario = new Yoti.DynamicScenarioBuilder()
    .withCallbackEndpoint("/your-callback")
    .withPolicy(dynamicPolicy)
		.withSubject(subject)
    .build();
{% /tab %}
{% tab language="java" %}
DynamicScenario dynamicScenario = DynamicScenario.builder()
    .withCallbackEndpoint("/your-callback")
    .withPolicy(dynamicPolicy)
    .build();
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\ShareUrl\Policy\DynamicScenarioBuilder;

$dynamicScenario = (new DynamicScenarioBuilder())
    ->withCallbackEndpoint("/your-callback")
    ->withPolicy(dynamicPolicy)
    ->build();
{% /tab %}
{% tab language="csharp" %}
var subject = new {
	subject_id = "some_subject_id_string"
};

DynamicScenario dynamicScenario = new DynamicScenarioBuilder()
  .WithCallbackEndpoint("/your-callback")  
  .WithPolicy(dynamicPolicy)
  .WithSubject(subject)
  .Build();
{% /tab %}
{% tab language="go" %}
dynamicScenario := (&dynamic.DynamicScenarioBuilder{})
	.WithCallbackEndpoint("/your-callback")
	.WithPolicy(dynamicPolicy)
	.Build()
{% /tab %}
{% /code %}

In the V2 API, you have to specify a session configuration instead of a scenario. It also introduces the capability to subscribe to webhook notifications:

{% code %}
{% tab language="javascript" %}
const subject = {
  	subject_id: 'some_subject_id_string',
};

const notification = new Yoti.ShareSessionNotificationBuilder()
		.withUrl("notification-webhook")
		.withMethod("POST")
		.build();

const shareSessionConfig = new Yoti.ShareSessionConfigurationBuilder()
    .withRedirectUri("/your-callback")
    .withPolicy(policy)
    .withSubject(subject)
		.withNotification(notification)
    .build();
{% /tab %}
{% tab language="java" %}
Map<String, Object> subject = new HashMap<>();
subject.put("subject_id", "some_subject_id_string");

ShareSessionNotification notification = ShareSessionNotification.builder("notification-webhook")
    .withMethod("POST")
    .build();

ShareSessionRequest shareSessionConfig = ShareSessionRequest.builder()
  	.withRedirectUri("/your-callback")
    .withPolicy(policy)
  	.withSubject(subject)
  	.withNotification(notification)
    .build();
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\Identity\ShareSessionRequestBuilder;

$subject = (object)[
  'subject_id' => 'some_subject_id_string'
];

$notification = (new ShareSessionNotificationBuilder())
		->withUrl("notification-webhook")
		->withMethod("POST")
		->build();

$shareSessionConfig = (new ShareSessionRequestBuilder())
  	->withRedirectUri("your-callback")
    ->withPolicy($policy)
  	->withSubject($subject)
  	->withNotification($notification)
    ->build();
{% /tab %}
{% tab language="csharp" %}
var subject = new {
	subject_id = "some_subject_id_string"
};

var notification = new ShareSessionNotificationBuilder()
  .WithUrl("notification-webhook")
  .WithMethod("POST")
  .Build();

ShareSessionConfiguration shareSessionConfig = new ShareSessionConfigurationBuilder()
  .WithRedirectUri("/your-callback-url")
  .WithPolicy(policy)
  .WithSubject(subject)
  .WithNotification(notification)
  .Build();
{% /tab %}
{% tab language="go" %}
subject := []byte(`{
	"subject_id": "my_subject_id"
}`)

notification := (&digitalidentity.ShareSessionNotification{})
	.WithUrl("notification-webhook")
  .WithMethod("POST")
  .Build()     
                 
shareSessionConfig := (&digitalidentity.ShareSessionBuilder{})
  .WithRedirectUri("/your-callback-url")
	.WithPolicy(policy)
  .WithSubject(subject)
  .WithNotification(notification)
  .Build()
{% /tab %}
{% /code %}

### Create a Share URL/Session

Using the scenario/session request you need to get create a Share URL/Session which will be used by the Yoti scripts to generate a Yoti QR.

In the V1 API, you would create a Share URL like this:

{% code %}
{% tab language="javascript" %}
yotiClient.createShareUrl(dynamicScenario)
  .then((shareUrlResult) => {
  	const shareURL =  shareUrlResult.getShareUrl();
  }).catch((error) => {
    console.error(error.message);
  });
{% /tab %}
{% tab language="java" %}
try {
  	String shareUrl = client.createShareUrl(dynamicScenario).getUrl();
} catch (DynamicShareException e) {
  	LOG.error(e.getMessage());
}
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\Exception\ShareUrlException;

try {
  	$shareUrlResult = $yotiClient->createShareUrl($dynamicScenario);
  	$shareUrl = $shareUrlResult->getShareUrl();
} catch (ShareUrlException e) {
  	throw new ShareUrlException($e->getMessage());
}
{% /tab %}
{% tab language="csharp" %}
ShareUrlResult shareUrlResult = yotiClient.CreateShareUrl(dynamicScenario);
Uri shareURL = ShareUrlResult.Url;
{% /tab %}
{% tab language="go" %}
shareUrlResult, err := client.CreateShareURL(dynamicScenario)
shareUrl := shareUrlResult.ShareURL
{% /tab %}
{% /code %}

In the V2 API, you have to create a session instead of a Share URL like this:

{% code %}
{% tab language="javascript" %}
yotiClient.createShareSession(shareSessionConfig)
  .then((shareSessionResult) => {
  	const shareSession = shareSessionResult;
  	const shareSessionId = shareSession.getId();
  }).catch((error) => {
    console.error(error.message);
  });
{% /tab %}
{% tab language="java" %}
try {
  	ShareSession shareSession = client.createShareSession(shareSessionConfig);
  	String shareSessionId = shareSession.getId();
} catch (DigitalIdentityException e) {
  	LOG.error(e.getMessage());
}
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\Exception\DigitalIdentityException;

try {
  	$shareSession = $client->createShareSession($shareSessionConfig);
  	$shareSessionId = $shareSession->getId();
} catch (DigitalIdentityException e) {
  	throw new DigitalIdentityException($e->getMessage());
}
{% /tab %}
{% tab language="csharp" %}
ShareSession shareSession = yotiClient.CreateShareSession(shareSessionConfig);
var shareSessionId = shareSession.Id;
{% /tab %}
{% tab language="go" %}
shareSession, err := client.CreateShareSession(shareSessionConfig)
shareSessionId := shareSession.Id
{% /tab %}
{% /code %}

## Client Side View

Yoti provides a client-side script that you can include in your html file to display a Yoti button or QR code.

In the V1 API, you would display a modal QR button using a Share URL:

{% code %}
{% tab language="html" %}
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
          shareUrl: "shareURL",
          clientSdkId: "xxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
          displayLearnMoreLink: true,
        }
      ]
    });
  </script>
</body>
{% /tab %}
{% /code %}

In the V2 API, you will display the same modal QR button using a Session ID:

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
          name: 'test',
          domId: 'xxx',
          sdkId: 'xxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx',
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

## Retrieve Profile

This step involves using a one-time-use token (v1) or a receipt id (v2), and decrypting it to get a user profile.

In the V1 API, you would retrieve a user profile with a token:

{% code %}
{% tab language="javascript" %}
yotiClient.getActivityDetails(oneTimeUseToken)
  .then((activityDetails) => {
    const rememberMeId = activityDetails.getRememberMeId();
    const profile = activityDetails.getProfile();

    const selfieImageData = profile.getSelfie().getValue();
    const base64SelfieUri = profile.getSelfie().getValue().getBase64Content();
    const fullName = profile.getFullName().getValue();
    const familyName = profile.getFamilyName().getValue();
    const givenNames = profile.getGivenNames().getValue();
    const phoneNumber = profile.getPhoneNumber().getValue();
    const emailAddress = profile.getEmailAddress().getValue();
    const dateOfBirth = profile.getDateOfBirth().getValue();
    const postalAddress = profile.getPostalAddress().getValue();
    const structuredPostalAddress = profile.getStructuredPostalAddress().getValue();
    const gender = profile.getGender().getValue();
    const nationality = profile.getNationality().getValue();
    const ageVerifications = profile.getAgeVerifications();
    const ageVerified = profile.findAgeVerification('age_over:', 18).getValue(); // or 'age_under:'
    const documentDetails = profile.getDocumentDetails().getValue();
  })
{% /tab %}
{% tab language="java" %}
ActivityDetails activityDetails = client.getActivityDetails(oneTimeUseToken);

String rememberMeId = activityDetails.getRememberMeId();
HumanProfile profile = activityDetails.getUserProfile();

Image selfie = profile.getSelfie().getValue();
String selfieBase64Content = selfie.getBase64Content();
String fullName = profile.getFullName().getValue();
String givenNames = profile.getGivenNames().getValue();
String familyName = profile.getFamilyName().getValue();
String phoneNumber = profile.getPhoneNumber().getValue();
String emailAddress = profile.getEmailAddress().getValue();
Date dateOfBirth = profile.getDateOfBirth().getValue();
String gender = profile.getGender().getValue();
String address = profile.getPostalAddress().getValue();
String nationality = profile.getNationality().getValue();

AgeVerification over18Verification = profile.findAgeOverVerification(18);
if (over18Verification != null) {
  	boolean isAgedOver18 = over18Verification.getResult();
}

AgeVerification under55Verification = profile.findAgeUnderVerification(55);
if (under55Verification != null) {
  	boolean isAgedUnder55 = under55Verification.getResult();
}

Map<?,?> structuredPostalAddress = profile.getStructuredPostalAddress().getValue();
DocumentDetails documentDetails = profile.getDocumentDetails().getValue();
{% /tab %}
{% tab language="php" %}
<?php
  
$activityDetails = $client->getActivityDetails($oneTimeUseToken);

$rememberMeId = $activityDetails->getRememberMeId();
$parentRememberMeId = $activityDetails->getParentRememberMeId();

$applicationProfile = $activityDetails->getApplicationProfile();
$applicationName = $applicationProfile->getApplicationName()->getValue();

$profile = $activityDetails->getProfile();

$selfieImageObj = $profile->getSelfie()->getValue();
$selfieImageBase64Content = $selfieImageObj->getBase64Content();
$fullName = $profile->getFullName()->getValue();
$givenNames = $profile->getGivenNames()->getValue();
$familyName = $profile->getFamilyName()->getValue();
$phoneNumber = $profile->getPhoneNumber()->getValue();
$emailAddress = $profile->getEmailAddress()->getValue();
$dateOfBirth = $profile->getDateOfBirth()->getValue();
$postalAddress = $profile->getPostalAddress()->getValue();
$structuredPostalAddress = $profile->getStructuredPostalAddress()->getValue();
$gender = $profile->getGender()->getValue();
$nationality = $profile->getNationality()->getValue();
$ageVerifications = $profile->getAgeVerifications();
$ageUnderVerification = $profile->findAgeUnderVerification($age);
$ageOverVerification = $profile->findAgeOverVerification($age);
$documentDetails = $profile->getDocumentDetails()->getValue();
{% /tab %}
{% tab language="csharp" %}
ActivityDetails activityDetails = yotiClient.GetActivityDetails(oneTimeUseToken);

string RememberMeID = activityDetails.RememberMeId;

YotiProfile profile = activityDetails.Profile;
Image selfie = profile.Selfie?.GetValue();
string selfieURI = profile.Selfie?.GetValue().GetBase64URI();

string fullName = profile.FullName?.GetValue();
string emailAddress = profile.EmailAddress?.GetValue();

DateTime? dateOfBirth = profile.DateOfBirth?.GetValue(); 
string nationality = profile.Nationality?.GetValue();
string address = profile.Address?.GetValue();

bool hasIdentityProfile = profile.IdentityProfileReport != null ? true : false;

if (hasIdentityProfile) {
	var identityProfileReport = profile.IdentityProfileReport.GetValue();
}
{% /tab %}
{% tab language="go" %}
activityDetails, err := client.GetActivityDetails(yotiOneTimeUseToken)

rememberMeID := activityDetails.RememberMeID
parentRememberMeID := activityDetails.ParentRememberMeID

userProfile := activityDetails.UserProfile
selfie := userProfile.Selfie().Value().Data()
fullName := userProfile.FullName().Value()
givenNames := userProfile.GivenNames().Value()
familyName := userProfile.FamilyName().Value()
mobileNumber := userProfile.MobileNumber().Value()
emailAddress := userProfile.EmailAddress().Value()

var dateOfBirth *time.Time
dobAttr, err := userProfile.DateOfBirth()

if err != nil {
		// handle error
} else {
  dateOfBirth = dobAttr.Value()
}

gender := userProfile.Gender().Value()
address := userProfile.Address().Value()
nationality := userProfile.Nationality().Value()
{% /tab %}
{% /code %}

In the V2 API, you will use the receipt id to retrieve a user profile:

{% code %}
{% tab language="javascript" %}
yotiClient.getShareReceipt(receiptId)
  .then((shareReceipt) => {
  	const sessionId = shareReceipt.getSessionId();
  	const rememberMeId = shareReceipt.getRememberMeId();
  	const parentRememberMeId = shareReceipt.getParentRememberMeId();

    const profile = shareReceipt.getProfile();
  
    const fullName = profile.getFullName().value;
    const dateOfBirth = profile.getDateOfBirth().getValue();
    const gender = profile.getGender().getValue();
    const nationality = profile.getNationality().getValue();
  	const postalAddress = profile.getPostalAddress().getValue();
    const emailAddress = profile.getEmailAddress().getValue();
    const phoneNumber = profile.getPhoneNumber().getValue();
    const selfieImageData = profile.getSelfie().getValue();
    const base64SelfieUri = selfieImageData.getBase64Content();
    
    const documentDetails = profile.getDocumentDetails().getValue();
  })
{% /tab %}
{% tab language="java" %}
try {
  	Receipt shareReceipt = client.fetchShareReceipt(receiptId);
  
  	String sessionId = shareReceipt.getSessionId();
  	String rememberMeId = shareReceipt.getRememberMeId();
  	String parentRememberMeId = shareReceipt.getParentRememberMeId();

    HumanProfile profile = shareReceipt.getProfile();
  
    String fullName = profile.getFullName().getValue();
		Date dateOfBirth = profile.getDateOfBirth().getValue();
		String gender = profile.getGender().getValue();
		String nationality = profile.getNationality().getValue();
  	String postalAddress = profile.getPostalAddress().getValue();
  	String emailAddress = profile.getEmailAddress().getValue();
  	String phoneNumber = profile.getPhoneNumber().getValue();

  	Image selfieImageData = profile.getSelfie().getValue();
		String selfieBase64Content = selfieImageData.getBase64Content();
  
  	DocumentDetails documentDetails = profile.getDocumentDetails().getValue();
} catch (DigitalIdentityException e) {
  	LOG.error(e.getMessage());
}
{% /tab %}
{% tab language="php" %}
<?php
  
$shareReceipt = $client->fetchShareReceipt($receiptId);

$sessionId = $shareReceipt->getSessionId();
$rememberMeId = $shareReceipt->getRememberMeId();
$parentRememberMeId = $shareReceipt->getParentRememberMeId();

$applicationProfile = $shareReceipt->getApplicationContent()->getProfile();
$applicationName = $applicationProfile->getApplicationName();

$profile = $shareReceipt->getProfile();

$fullName = $profile->getFullName()->getValue();
$dateOfBirth = $profile->getDateOfBirth()->getValue();
$nationality = $profile->getNationality()->getValue();
$postalAddress = $profile->getPostalAddress()->getValue();
$structuredPostalAddress = $profile->getStructuredPostalAddress()->getValue();
$selfieImageObj = $profile->getSelfie()->getValue();
$selfieImageBase64Content = $selfieImageObj->getBase64Content();

$documentDetails = $profile->getDocumentDetails()->getValue();
{% /tab %}
{% tab language="csharp" %}
ShareReceipt shareReceipt = yotiClient.GetShareReceipt(receiptId);

DateTime? timestamp = shareReceipt.Timestamp;
string sessionId = shareReceipt.SessionId;
string rememberMeId = shareReceipt.RememberMeId;

YotiProfile profile = shareReceipt.Profile;
Image selfie = profile.Selfie?.GetValue();
string selfieURI = profile.Selfie?.GetValue().GetBase64URI();

string fullName = profile.FullName?.GetValue();
string emailAddress = profile.EmailAddress?.GetValue();

DateTime? dateOfBirth = profile.DateOfBirth?.GetValue(); 
string nationality = profile.Nationality?.GetValue();
string address = profile.Address?.GetValue();

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

userProfile := shareReceipt.UserContent.UserProfile
selfie := userProfile.Selfie()
selfieBase64URL := selfie.Value().Base64URL()
fullName := userProfile.FullName().Value()
givenNames := userProfile.GivenNames().Value()
familyName := userProfile.FamilyName().Value()
mobileNumber := userProfile.MobileNumber().Value()
emailAddress := userProfile.EmailAddress().Value()

var dateOfBirth *time.Time
dobAttr, err := userProfile.DateOfBirth()

if err != nil {
		// handle error
} else {
  dateOfBirth = dobAttr.Value()
}

gender := userProfile.Gender().Value()
address := userProfile.Address().Value()
nationality := userProfile.Nationality().Value()
{% /tab %}
{% /code %}

## New Functionality (v2 SDK)

In the Share v2 SDK, we have introduced new functionality to fetch the Session details and to configure Webhook notifications. The SDK includes the following relevant methods for these endpoints.

### Fetch a Session

To retrieve a Share v2 session, use the following method:

{% code %}
{% tab language="javascript" %}
yotiClient.getShareSession(sessionId)
  .then((shareSession) => {
  	const sessionId = shareSession.getId();
		const sessionStatus = shareSession.getStatus();	
		const sessionExpiry = shareSession.getExpiry();

		const qrCodeId = shareSession.getScannedQrCodeId();
		const receiptId = shareSession.getReceiptId();
  }).catch((error) => {
    console.error(error.message);
  });
{% /tab %}
{% tab language="java" %}
try {
  	ShareSession shareSession = client.fetchShareSession(sessionId);
  
  	String sessionId = shareSession.getId();
		String sessionStatus = shareSession.getStatus();	
		String sessionExpiry = shareSession.getExpiry();

		String qrCodeId = shareSession.getQrCodeId();
		String receiptId = shareSession.getReceiptId();
} catch (DigitalIdentityException e) {
  	LOG.error(e.getMessage());
}
{% /tab %}
{% tab language="php" %}
// Coming soon
{% /tab %}
{% tab language="csharp" %}
ShareSession shareSession = yotiClient.GetShareSession(sessionId);

string sessionId = shareSession.GetId();
string sessionStatus = shareSession.GetStatus();
DateTime? sessionExpiry = shareSession.GetExpiry();

string qrCodeId = shareSession.GetScannedQrCodeId();
string receiptId = shareSession.GetReceiptId();
{% /tab %}
{% tab language="go" %}
shareSession := client.GetSession(sessionId)

sessionId := shareSession.Id
sessionStatus := shareSession.Status
sessionExpiry := shareSession.Expiry

qrCodeId := shareSession.QrCode.Id
receiptId := shareSession.Receipt.Id
{% /tab %}
{% /code %}

Each session has a status associated with it, that will be one of the following:

{% table widths="218" %}
| Status | Description | 
| ---- | ---- | 
| CREATED | Session created but no QR Code has been generated. | 
| QR_CODE_CREATED | At least one QR code has been created for the session and mobile app has not yet "scanned" it. | 
| QR_CODE_SCANNED | The mobile app has “scanned” the QR Code (i.e. a QR code was locked to a mobile app token) and system is waiting for user to complete (or cancel) the share. | 
| CANCELLED | Mobile app requested the session to be cancelled (before share was completed). | 
| EXPIRED | The share associated with the session was never completed (no receipt available). | 
| COMPLETED | The share associated with the session was completed (with success receipt available). | 
| FAILED | The share associated with the session was completed (with failure receipt available). | 
| ERROR | A "catch-all" status for unexpected/unrecoverable errors that might happen during execution (e.g. we get a receipt but the service fails to parse it, required parameter not present). | 
{% /table %}

### Webhook notifications

Briefly described above, you can configure Webhook notifications for a Share v2 session as following:

{% code %}
{% tab language="javascript" %}
const notification = new Yoti.ShareSessionNotificationBuilder()
		.withUrl("webhook-url")
		.withMethod("POST")
		.withHeader("Authorization", "<Bearer_token>") // Optional
		.withVerifiedTls(true) 	// Optional
		.build();
{% /tab %}
{% tab language="java" %}
ShareSessionNotification notification = ShareSessionNotification.builder("webhook-url")
    .withMethod("POST")
  	.withHeader("Authorization", "<Bearer_token>") // Optional
		.withVerifyTls(true) 	// Optional
    .build();
{% /tab %}
{% tab language="php" %}
$notification = (new ShareSessionNotificationBuilder())
		->withUrl("webhook-url")
		->withMethod("POST")
  	->withHeader("Authorization", "<Bearer_token>") // Optional
  	->withVerifyTls(true) // Optional
		->build();
{% /tab %}
{% tab language="csharp" %}
var notification = new ShareSessionNotificationBuilder()
  .WithUrl("webhook-url")
  .WithMethod("POST")
  .WithHeader("Authorization", "<Bearer_token>") // Optional
	.WithVerifiedTls(true) 	// Optional
  .build();
{% /tab %}
{% tab language="go" %}
headers := []byte(`{
	"Authorization": "<Bearer_token>"
}`)

notification, err := (&digitalidentity.ShareSessionNotification{})
	.WithUrl("webhook-url")
  .WithMethod("POST")
	.WithHeaders(headers) // Optional
	.WithVerifyTls(true) 	// Optional
  .Build()
{% /tab %}
{% /code %}

#### Example notifications

The notifications will be sent in the following format:

**COMPLETED:**

{% code %}
{% tab language="json" %}
{
    "id": "ss.v2.ChZV8h5GZTlLT1JrSzc5QkVMc1F0a9JR3gkyLmxkNS5nYnI=",
    "status": "COMPLETED",
    "created": "2023-08-01T13:21:06.389Z",
    "updated": "2023-08-01T13:22:48.284Z",
    "receipt": {
        "id": "RPA4ZvOZ/xIRhIeHh9Jw9HNpEK//610kEpCbZmQwNZlZ6H6w41VUlDQWn+4p7Lk"
    }
}
{% /tab %}
{% /code %}

**FAILED:**

{% code %}
{% tab language="json" %}
{
    "id": "ss.v2.ChYwYk5mSG9sdlJSbWNFQ1VJHw4kYlZ3EgkzLmxkNS5nYnI=",
    "status": "FAILED",
    "created": "2023-08-02T08:33:23.326Z",
    "updated": "2023-08-02T08:34:40.885Z",
    "receipt": {
      "id": "FYWI8nE8GAo8xMBVprPCG78J4TaWsW+prX5DEj9WN0eEROlg7avAP/ZAlJmlP3C1",
      "error": "MANDATORY_DOCUMENT_NOT_PROVIDED"
    }
}
{% /tab %}
{% /code %}