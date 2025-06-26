---
type: page
title: Create a session
listed: true
slug: create-a-session
description: 
index_title: Create a session
hidden: 
keywords: 
tags: 
---

There are four steps to follow to integrate the Identity verification SDK:

1. Install the SDK
2. Create the session
3. Launch the user view
4. Retrieve the results

This section will explain how to install the SDK and create a session.

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      You will need the Yoti App on your phone and to have registered your business with Yoti. Click here for more info.
   </div>
   <div class="alert-links"> 
         <a target="_self" href="https://developers.yoti.com/yoti/identity-verification/getting-started">View Onboarding with Yoti</a>
   </div>
</div>
{% /html %}

---

## Installing the SDK

Please use our Yoti SDKs to automatically build the relevant session. You will need the following information about your application from the Yoti Hub:

- Yoti SDK ID 
- Your application key pair

The Yoti SDKs are available via popular dependency management systems.

{% code %}
{% tab language="javascript" title="Node.js" %}
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
composer require yoti/yoti-php-sdk// Click to edit code
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

go get "github.com/getyoti/yoti-go-sdk/v3"
{% /tab %}
{% /code %}

---

## Create a session

Once you have added the Yoti SDK dependency to your project, you can use it to build and create your session as shown in the code snippet below:

{% code %}
{% tab language="javascript" title="Node.js" %}
const path = require('path');
const fs = require("fs");

const {
    IDVClient,
    SessionSpecificationBuilder,
    SdkConfigBuilder,
    NotificationConfigBuilder,
} = require('yoti');

const CLIENT_SDK_ID = 'YOTI_CLIENT_SDK_ID'
const PEM_PATH = 'YOTI_KEY_FILE_PATH'
const PEM_KEY = fs.readFileSync(path.join(__dirname, PEM_PATH));

const idvClient = new IDVClient(
    CLIENT_SDK_ID,
    PEM_KEY
 );

 idvClient
    .createSession(sessionSpec)
    .then((session) => {
        const sessionId = session.getSessionId();
        const clientSessionToken = session.getClientSessionToken();
        const clientSessionTokenTtl = session.getClientSessionTokenTtl();
        console.log(sessionId);
    })
    .catch((err) => {
        console.log(err)
    });
{% /tab %}
{% tab language="java" %}
import com.yoti.api.client.ClassPathKeySource;
import com.yoti.api.client.docs.DocScanClient;
import com.yoti.api.client.docs.DocScanException;
import com.yoti.api.client.docs.session.create.CreateSessionResult;

...
DocScanClient docScanClient = DocScanClient.builder()
        .withClientSdkId("YOTI_CLIENT_SDK_ID")
        .withKeyPairSource(ClassPathKeySource.fromClasspath("/path/to/pem"))
        .build();

CreateSessionResult sessionResult = docScanClient.createSession(sessionSpec);

string sessionId = createSessionResult.getSessionId();
string clientSessionToken = createSessionResult.getClientSessionToken();
...
{% /tab %}
{% tab language="php" %}
<?php

require_once './vendor/autoload.php';

use Yoti\DocScan\DocScanClient;
use Yoti\DocScan\Session\Create\SdkConfigBuilder;
use Yoti\DocScan\Session\Create\SessionSpecificationBuilder;
use Yoti\DocScan\Session\Create\NotificationConfigBuilder;

$YOTI_CLIENT_SDK_ID = 'YOTI_CLIENT_SDK_ID';
$YOTI_PEM = '/path/to/pem';

$docScanClient = new DocScanClient($YOTI_CLIENT_SDK_ID, $YOTI_PEM);

$session = $docScanClient->createSession($sessionSpec);

$sessionId = $session->getSessionId();
$clientSessionToken = $session->getClientSessionToken();
{% /tab %}
{% tab language="csharp" %}
using System.IO;
using System.Net.Http;
using Yoti.Auth;
using Yoti.Auth.DocScan;
using Yoti.Auth.DocScan.Session.Create;
using Yoti.Auth.DocScan.Session.Create.Check;

...
const string YOTI_CLIENT_SDK_ID = "YOTI_CLIENT_SDK_ID";
const string PEM_PATH = "/path/to/pem";

StreamReader privateKeyStream = System.IO.File.OpenText(PEM_PATH);
var key = CryptoEngine.LoadRsaKey(privateKeyStream);

var docScanClient = new DocScanClient(YOTI_CLIENT_SDK_ID, key, new HttpClient());

CreateSessionResult createSessionResult = docScanClient.CreateSession(sessionSpec);

string sessionId = createSessionResult.SessionId;
string clientSessionToken = createSessionResult.ClientSessionToken;
...
{% /tab %}
{% tab language="go" %}
sdkID := "YOTI_CLIENT_SDK_ID";
key, _ := ioutil.ReadFile("YOTI_KEY_FILE_PATH")

client, err := docscan.NewClient(sdkId, key)

createSessionResult, err = client.CreateSession(sessionSpec)
sessionId = createSessionResult.SessionID
clientSessionToken = createSessionResult.ClientSessionToken
{% /tab %}
{% /code %}

Your session can be configured with the following: 

- Preferences 
- Scheme 
- Notifications

{% html %}
<div class="alert-know">
    <div class="alert-title" id="know">
      Recommendation
    </div>
    <div class="alert-text">
      Yoti strongly recommends you to use notifications for each session status.
  	</div>
    <div class="alert-links"> 
      <a href="https://developers.yoti.com/identity-verification/notifications">Notifications</a>
    </div>
</div>
{% /html %}

---

## Client Preferences

To create a session, please start by setting your preferences. For this purpose, the method sdkConfig builder is explained below. If parameters are not defined the default below will be set:

{% code %}
{% tab language="javascript" title="Node.js" %}
.withSdkConfig(
        new SdkConfigBuilder()
          .withAllowsCamera()
          .withPrimaryColour('#2d9fff')
          .withSecondaryColour('#FFFFFF')
          .withFontColour('#FFFFFF')
          .withPresetIssuingCountry('GBR')
          .withSuccessUrl(`${process.env.YOTI_APP_BASE_URL}/index`)
          .withErrorUrl(`${process.env.YOTI_APP_BASE_URL}/profile`)
          .withAllowHandoff(true)
          .build()
      )
{% /tab %}
{% tab language="java" %}
SdkConfig sdkConfig = SdkConfig.builder()
                .withAllowsCamera()
                .withPrimaryColour("#2d9fff")
                .withSecondaryColour("#FFFFFF")
                .withFontColour("#FFFFFF")
                .withPresetIssuingCountry("GBR")
                .withSuccessUrl("https://localhost:8443/success")
                .withErrorUrl("https://localhost:8443/error")
                .build();
{% /tab %}
{% tab language="php" %}
$sdkConfig =
    (new SdkConfigBuilder())
    ->withAllowsCamera()
    ->withPrimaryColour('#2d9fff')
    ->withSecondaryColour('#FFFFFF')
    ->withFontColour('#FFFFFF')
    ->withPresetIssuingCountry('GBR')
    ->withSuccessUrl('/your/success/url')
    ->withErrorUrl('/your/error/url')
    ->withAllowHandoff(true)
    ->build()
{% /tab %}
{% tab language="csharp" %}
var sdkConfig = new SdkConfigBuilder()
                .WithAllowsCamera()
                .WithPrimaryColour("#2d9fff")
                .WithSecondaryColour("#FFFFFF")
                .WithFontColour("#FFFFFF")
                .WithPresetIssuingCountry("GBR")
                .WithSuccessUrl("/your/success/url")
                .WithErrorUrl("/your/error/url")
                .WithAllowHandoff(false)
                .Build()
{% /tab %}
{% tab language="go" %}
var sdkConfig *create.SDKConfig
sdkConfig, err = create.NewSdkConfigBuilder().
	WithAllowsCamera().
	WithPrimaryColour("#2d9fff").
	WithSecondaryColour("#FFFFFF").
	WithFontColour("#FFFFFF").
	WithLocale("en-GB").
	WithPresetIssuingCountry("GBR").
	WithSuccessUrl("https://localhost:8080/success").
	WithErrorUrl("https://localhost:8080/error").
	withAllowHandoff(true).
	Build()
{% /tab %}
{% /code %}

{% table widths="" %}
| Type | Parameter (examples) | Description | 
| ---- | ---- | ---- | 
| withPrimaryColour | #2d9fff(default), #ff0000 | Colours of the button provided in the frontend client as a hexadecimal RGB value. | 
| withPresetIssuingCountry | USA, GBR | The user must select the issuing country of the document they are uploading. This setting determines which issuing country is selected by default.\n\n\n\nNOTE: Must be a 3 letter ISO 3166 code. | 
| withSuccessUrl | [https://yourdomain.com/success](https://yourdomain.com/success) | If the upload/photo is successfully captured redirect your users here. Yoti will then begin to carry out the requested checks and tasks. If undefined, the page will not redirect and you can listen to Yoti's post messages on the same page. | 
| withErrorUrl | [https://yourdomain.com/error](https://yourdomain.com/error) | If the upload/photo is unsuccessfully captured redirect your users here. If undefined, the user view will display an error screen, with the error code as a query parameter and won't redirect. (Details on the error codes can be found in [Client side user view](Client side user view)) | 
| withAllowHandoff | true, false | if enabled will offer the user to transfer flow from desktop to a mobile device by scanning a QR code. | 
{% /table %}

---

## Session Requirements

After that, specify the desired scheme in the identity profile requirements. 

{% code %}
{% tab language="javascript" title="Node.js" %}
const identityProfileRequirements = {
  trust_framework: 'UK_TFIDA',
  scheme: {
    type: 'DBS',
    objective: 'STANDARD',
  },
};
{% /tab %}
{% tab language="java" %}
JSONObject scheme = new JSONObject();
scheme.put("type", "DBS");
scheme.put("objective", "STANDARD");

JSONObject identityProfileRequirements = new JSONObject();
identityProfileRequirements.put("trust_framework", "UK_TFIDA");
identityProfileRequirements.put("scheme", scheme);
{% /tab %}
{% tab language="php" %}
$identityProfileRequirements = (object)[
  'trust_framework' => 'UK_TFIDA',
  'scheme' => [
    'type' => 'DBS',
    'objective' => 'STANDARD'
  ]
];
{% /tab %}
{% tab language="csharp" %}
string identityProfileRequirementsString = @"{
  trust_framework: 'UK_TFIDA',
  scheme: {
  	type: 'DBS',
    objective: 'STANDARD'
	}
}";

JObject identityProfileRequirements = JObject.Parse(identityProfileRequirementsString);
{% /tab %}
{% tab language="go" %}
identityProfile := []byte(`{
	"trust_framework": "UK_TFIDA",
	"scheme": {
		"type": "DBS",
		"objective": "BASIC"
	}
}`)
{% /tab %}
{% /code %}

### Identity Profile Requirements Explained

{% table widths="157,0,0" %}
| Field | Value | Description | Mandatory | 
| ---- | ---- | ---- | ---- | 
| trust_framework | String | Defines under which trust framework this identity profile should be verified. Enum: UK_TFIDA | Yes | 
| scheme | Object | Defines which scheme this identity profile should satisfy. The scheme must be supported by the specified trust framework otherwise the request is considered invalid. | Yes | 
| type | String | Defines which scheme this identity profile should satisfy. Enum: DBS, RTW, RTR, DBS_RTW | Yes | 
| objective | String | Defines the objective to be achieved for the particular scheme. It must be provided for those schemes where it is mandatory. Example, this is mandatory for DBS and the possible values are: ”BASIC”, “STANDARD”, “ENHANCED”. | Yes \n\n(in case of DBS) | 
{% /table %}

---

## System Preferences

Then, specify the subject id and set the system preferences for your session.

{% code %}
{% tab language="javascript" title="Node.js" %}
const subject = {
  subject_id: 'subject_id_string',
};

const sessionSpec = new SessionSpecificationBuilder()
    .withClientSessionTokenTtl(600)
    .withResourcesTtl(90000)
    .withUserTrackingId('some-user-tracking-id')
    .withSubject(subject)
    .withIdentityProfileRequirements(identityProfileRequirements)
    .withSdkConfig(sdkConfig)
    .withNotifications(notificationConfig)
    .build();
{% /tab %}
{% tab language="java" %}
JSONObject subject = new JSONObject();
subject.put("subject_id", "subject_id_string");

SessionSpec sessionSpec = SessionSpec.builder()
                .withClientSessionTokenTtl(600)
                .withResourcesTtl(604800)
                .withNotifications(notificationConfig)
                .withSdkConfig(sdkConfig)
                .withSubject(subject)
                .withIdentityProfileRequirements(identityProfileRequirements)
                .build();
{% /tab %}
{% tab language="php" %}
$subject = (object)[
	'subject_id' => 'subject_id_string',
];

$sessionSpec = (new SessionSpecificationBuilder())
    ->withClientSessionTokenTtl(600)
    ->withResourcesTtl(90000)
    ->withSubject($subject)
    ->withIdentityProfileRequirements($identityProfileRequirements)
    ->withSdkConfig($sdkConfig)
    ->withNotifications($notificationConfig)
    ->build();
{% /tab %}
{% tab language="csharp" %}
string subjectString = @"{
  subject_id: 'subject_id_string',
}";

JObject subject = JObject.Parse(subjectString);

var sessionSpec = new SessionSpecificationBuilder()
                .WithClientSessionTokenTtl(600)
                .WithResourcesTtl(90000)
                .WithSubject(subject)
                .WithIdentityProfileRequirements(identityProfileRequirements)
                .WithNotifications(notificationConfig)
                .WithSdkConfig(sdkConfig)
                .Build();
{% /tab %}
{% tab language="go" %}
subject := []byte(`{
	"subject_id": "subject-id-string"
}`)

sessionSpec, err = create.NewSessionSpecificationBuilder().
	WithClientSessionTokenTTL(6000).
	WithResourcesTTL(900000).
	WithUserTrackingID("some-tracking-id").
	WithSDKConfig(sdkConfig).
	WithIdentityProfileRequirements(identityProfile).
	WithSubject(subject).
	Build()
{% /tab %}
{% /code %}

The table below explains the optional parameters for the session and data retention configuration.

{% table widths="0,503" %}
| Parameters | Description | Optional | 
| ---- | ---- | ---- | 
| withClientSessionTokenTtl | This is how long the full Identity verification session is open for in seconds. This must be longer than 300s (5 minutes). | ✅ | 
| withResourcesTtl | Retention period ("time to live") for uploaded documents/images in number of seconds. Default is one week (`60_60_24*7=604800`). This can be a minimum of 24 hours and must be at least 24 hours longer than the `client_session_token_ttl`_._ It starts from the first media upload.\n\n\n\nNote: This config may result in additional charges. Please get in touch with support if considering a TTL longer than three months. | ✅ | 
| withUserTrackingId | Allows the relying business backend to track the same user across multiple sessions. **Note:** This should not contain any personal identifiable information. | ✅ | 
| WithSubject | Allows to track the same user across multiple sessions. Should not contain any personal identifiable information. | ✅ | 
{% /table %}