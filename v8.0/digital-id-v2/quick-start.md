---
type: page
title: Quick start
listed: true
slug: quick-start
description: 
index_title: Quick start
hidden: 
keywords: 
tags: 
---

Here is a quick reference to kickstart your SDK integration. For detailed information, we suggest you read through the step by step integration guide.

Please see below for integration code snippets and example projects.

{% callout type="warning" title="Before you start" %}
You will need to access your Yoti Hub account with an e-mail & password or using the Yoti mobile app and to have registered your business with Yoti. Check the below links for more info.

[Onboarding with Yoti](/digital-id-v2/getting-started)

[Generate Production keys](/digital-id-v2/production-keys)
{% /callout %}

---

## Integration process

An example integration will include the steps highlighted in this section. We have provided code snippets in different languages to integrate Digital ID.

{% badge type="info" text="Hint" /%} For the complete guide, we suggest you read through the full documentation.

### Install the SDK

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
// To install the Yoti NuGet package, you need to install NuGet Package Manager. After that, enter the following command in the console:

Install-Package Yoti

// For other installation methods, see https://www.nuget.org/packages/Yoti
{% /tab %}
{% tab language="go" %}
// Simply add this as an import:
import "github.com/getyoti/yoti-go-sdk/v3"

// Or add the following line to your go.mod file
require github.com/getyoti/yoti-go-sdk/v3 v3.12.0
{% /tab %}
{% tab language="python" %}
# Get the Yoti Python SDK library
pip install yoti
{% /tab %}
{% /code %}

### Client initialisation

Initialise the Yoti Digital Identity Client using your SDK ID and PEM Key file.

{% code %}
{% tab language="javascript" %}
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
{% /tab %}
{% tab language="python" %}
# Coming soon
{% /tab %}
{% /code %}

### Create share session

Use the Yoti client to configure and create a share session.

{% code %}
{% tab language="javascript" %}
const policy = new Yoti.PolicyBuilder()
    // using a predefined method to add an attribute
    .withFullName()
		.withEmail()
    // if you wish the user to prove it's them by taking a selfie on share
    .withSelfieAuthentication()
    .build();

const shareSessionConfig = new Yoti.ShareSessionConfigurationBuilder()
    .withRedirectUri("/your-callback")
    .withPolicy(policy)
    .build();

yotiClient.createShareSession(shareSessionConfig)
  .then((shareSessionResult) => {
  	const shareSession = shareSessionResult;
  	const shareSessionId = shareSession.getId();
  }).catch((error) => {
    console.error(error.message);
  });
{% /tab %}
{% tab language="java" %}
Policy policy = Policy.builder()
    // using a predefined method to add an attribute
    .withFullName()
    .withEmail()
    // if you wish the user to prove it's them by taking a selfie on share
    .withSelfieAuthentication(true)
    .build();

ShareSessionRequest shareSessionConfig = ShareSessionRequest.builder()
  	.withRedirectUri("/your-callback")
    .withPolicy(policy)
    .build();

try {
  	ShareSession shareSession = client.createShareSession(shareSessionConfig);
  	String shareSessionId = shareSession.getId();
} catch (DigitalIdentityException e) {
  	LOG.error(e.getMessage());
}
{% /tab %}
{% tab language="php" %}
<?php
  
use Yoti\Identity\Policy\PolicyBuilder;
use Yoti\Exception\DigitalIdentityException;

$policy = (new PolicyBuilder())
    // using a predefined method to add an attribute
    ->withFullName()
  	->withEmail()
    // if you wish the user to prove it's them by taking a selfie on share
    ->withSelfieAuthentication()
    ->build();

$shareSessionConfig = (new ShareSessionRequestBuilder())
  	->withRedirectUri("your-callback")
    ->withPolicy($policy)
    ->build();

try {
  	$shareSession = $client->createShareSession($shareSessionConfig);
  	$shareSessionId = $shareSession->getId();
} catch (DigitalIdentityException e) {
  	throw new DigitalIdentityException($e->getMessage());
}
{% /tab %}
{% tab language="csharp" %}
YotiPolicy policy = new YotiPolicyBuilder()
  // using a predefined method to add an attribute
  .withFullName()
  .withEmail()
  // if you wish the user to prove it's them by taking a selfie on share
  .withSelfieAuthentication()
	.Build();

ShareSessionConfiguration shareSessionConfig = new ShareSessionConfigurationBuilder()
  .WithRedirectUri("/your-callback-url")
  .WithPolicy(policy)
  .Build();

ShareSession shareSession = yotiClient.CreateShareSession(shareSessionConfig);
var shareSessionId = shareSession.Id;
{% /tab %}
{% tab language="go" %}
policy := (&digitalidentity.PolicyBuilder{})
	// using a predefined method to add an attribute
	.WithFullName()
	.WithEmail()
	// if you wish the user to prove it's them by taking a selfie on share
	.WithSelfieAuth()
	.Build()

shareSessionConfig := (&digitalidentity.ShareSessionBuilder{})
  .WithRedirectUri("/your-callback-url")
	.WithPolicy(policy)
  .Build()

shareSession, err := client.CreateShareSession(shareSessionConfig)
if err != nil {
  return nil, err
}

shareSessionId := shareSession.Id
{% /tab %}
{% tab language="python" %}
# Coming soon
{% /tab %}
{% /code %}

### Client side view

Yoti provides a client-side script that you can include in your html file to display a Yoti button or inline QR code.

In the example below, use the modal button, but please feel free to look at our examples in our integration guide.

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

### Retrieve profile

When a share is completed, the webpage where Yoti button/QR is rendered will automatically be redirected to the URL specified in the session configuration. The query parameter of **redirectId** will be attached to this URL.

You will then use use the receipt id to retrieve a user profile:

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
{% tab language="python" %}
# Coming soon
{% /tab %}
{% /code %}

---

## Web examples

Our Github links below provide examples for the Digital ID Integration. Please select your preferred language to continue.

{% table %}
| Production | Sandbox | 
| ---- | ---- | 
| [Javascript](https://github.com/getyoti/yoti-node-sdk/tree/master/examples/digital-identity) | [Javascript](https://github.com/getyoti/yoti-node-sdk-sandbox/tree/master/examples) | 
| [Java](https://github.com/getyoti/yoti-java-sdk/tree/master/yoti-sdk-spring-boot-example) | [Java](https://github.com/getyoti/yoti-java-sdk) | 
| [PHP](https://github.com/getyoti/yoti-php-sdk/tree/master/examples) | [PHP](https://github.com/getyoti/yoti-php-sdk-sandbox/tree/master/examples) | 
| [.Net C#](https://github.com/getyoti/yoti-dotnet-sdk/tree/master/src/Examples) | [.Net C#](https://github.com/getyoti/yoti-dotnet-sdk-sandbox/tree/master/Examples/Yoti.Auth.Sandbox.Examples) | 
| [Go](https://github.com/getyoti/yoti-go-sdk/tree/master/_examples/digitalidentity) | [Go](https://github.com/getyoti/yoti-go-sdk/tree/master/_examples/profilesandbox) | 
| [Python](https://github.com/getyoti/yoti-python-sdk/tree/master/examples) | [Python](https://github.com/getyoti/yoti-python-sdk-sandbox/tree/master/examples) | 
{% /table %}