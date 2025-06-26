---
type: page
title: Integration guide
listed: true
slug: sandbox
description: 
index_title: Integration guide
hidden: 
keywords: 
tags: 
---

Welcome to the free Digital ID sandbox! The sandbox is an isolated test environment, intended to easily create test cases using dummy data where it's not feasible to test your integration with live data. 

The sandbox environment will allow you to:

- Mimic our production services in test
- Use test data bypassing using the Yoti app to share attributes.
- Double checking data formats and behaviours.
- Testing edge cases

The main difference between our Yoti production services and sandbox is the Yoti share token is completed using a production QR code whereas sandbox generates the token for you. 

{% html %}
<div class="alert-BYS">

   <div class="alert-title" id="BYS">

      Before you start

   </div>

   <div class="alert-text" >
     We recommend familiarising yourself with the Digital ID integration to understand the Yoti attribute sharing process.
You will also need some sandbox api keys.

   </div>

   <div class="alert-links"> 

      <a target="_self" href="https://developers.yoti.com/digital-id/integration-guide">Integration Guide</a> 
      <a target="_self" href="https://developers.yoti.com/digital-id/sandbox-keys">Generate Sandbox Keys</a> 
   </div>

</div>
{% /html %}

---

## Supported Languages

Just like the normal Yoti Client, the Yoti Sandbox Client SDK is available in seven languages:

- [Javascript (Node.js)](https://github.com/getyoti/yoti-node-sdk-sandbox)
- [Ruby](https://github.com/getyoti/yoti-ruby-sdk-sandbox)
- [PHP](https://github.com/getyoti/yoti-php-sdk-sandbox)
- [Python](https://github.com/getyoti/yoti-python-sdk-sandbox)
- [Java](https://github.com/getyoti/yoti-java-sdk)
- [Go](https://github.com/getyoti/yoti-go-sdk/tree/master/_examples/profilesandbox)
- [.NET](https://github.com/getyoti/yoti-dotnet-sdk-sandbox)

---

## Creating a Sandbox Request

### Installation

Once you have generated your keys, you can continue with installing the Sandbox SDK into your backend.

Just like our production integration, the Yoti Sandbox Client SDK is available in seven languages and installing is easy through popular package managers.

{% code %}
{% tab language="javascript" %}
// Yoti Client (skip if already installed)
npm install -S -E yoti

// Sandbox
npm install -S -E -D @getyoti/sdk-sandbox
{% /tab %}
{% tab language="java" %}
// If you are using Maven, add the following dependency, Sandbox is part of the Yoti Client SDK
<dependency>
    <groupId>com.yoti</groupId>
    <artifactId>yoti-sdk-api</artifactId>
    <version>M.m.p</version> // Use latest version from https://search.maven.org/artifact/com.yoti/yoti-sdk-api
</dependency>

// If you are using Gradle, add the following dependency:
compile group: 'com.yoti', name: 'yoti-sdk-api', version: 'M.m.p'

// Sandbox
<dependency>
    <groupId>com.yoti</groupId>
    <artifactId>yoti-sdk-sandbox</artifactId>
    <version>M.m.p</version> // Use latest version from https://search.maven.org/artifact/com.yoti/yoti-sdk-sandbox
</dependency>

// If you are using Gradle, add the following dependency:
compile group: 'com.yoti', name: 'yoti-sdk-sandbox', version: 'M.m.p'

// Bouncy Castle
<dependency>
    <groupId>org.bouncycastle</groupId>
    <artifactId>bcpkix-jdk15on</artifactId>
    <version>1.69</version>
</dependency>

// If you are using Gradle, add the following dependency:
compile group: 'org.bouncycastle', name: 'bcpkix-jdk15on', version: '1.69'
{% /tab %}
{% tab language="php" %}
// Get the Yoti PHP SDK library via a Composer package
composer require yoti/yoti-php-sdk

// Get the Yoti PHP SDK Sandbox library via a Composer package
composer require yoti/yoti-php-sdk-sandbox
{% /tab %}
{% tab language="python" %}
# Yoti Client (skip if already installed)
pip install yoti

# Sandbox
pip install yoti-sandbox
{% /tab %}
{% tab language="csharp" %}
// To install the Yoti NuGet package you will need to install NuGet.
// To import the latest Yoti SDK into your project, enter the following
// command from NuGet Package Manager Console in Visual Studio:

// Yoti Client (skip if already installed)
Install-Package Yoti

// Sandbox
Install-Package Yoti.Sandbox

// For other installation methods, see https://www.nuget.org/packages/Yoti
{% /tab %}
{% tab language="go" %}
// As of version 2.4.0, modules are used. This means it's not necessary to get a copy or fetch all dependencies 
// as instructed below, as the Go toolchain will fetch them as necessary. 
// You can simply add a `require github.com/getyoti/yoti-go-sdk/v2` to go.mod.
// To download and install the Yoti SDK and its dependencies, run the following command from your terminal:

go get "github.com/getyoti/yoti-go-sdk/v3”
{% /tab %}
{% tab language="ruby" %}
gem install yoti

# The gem provides a configuration generator for Ruby on Rails:

rails generate yoti:install

# To import the Yoti Sandbox SDK inside your project, add this line to your application's Gemfile:
gem 'yoti_sandbox'

# And then execute:
bundle install

# Or simply run the following command from your terminal:
gem install yoti_sandbox
{% /tab %}
{% tab language="java" title="Java v2" %}
// If you are using Maven, add the following dependency, Sandbox is part of the Yoti Client SDK
<dependency>
    <groupId>com.yoti</groupId>
    <artifactId>yoti-sdk-impl</artifactId>
    <version>2.12.0</version>
</dependency>

// If you are using Gradle, add the following dependency:
compile group: 'com.yoti', name: 'yoti-sdk-impl', version: '2.12.0'

// Sandbox
<dependency>
    <groupId>com.yoti</groupId>
    <artifactId>yoti-sdk-sandbox</artifactId>
    <version>2.9.0</version>
</dependency>

// If you are using Gradle, add the following dependency:
compile group: 'com.yoti', name: 'yoti-sdk-sandbox', version: '2.9.0'
{% /tab %}
{% /code %}

The sandbox client is packaged separately to the production Yoti client enabling it to be used as a development dependency.

### Initialising the Sandbox Client

You will need your Sandbox Client SDK ID and PEM file created from the [Yoti Hub](https://hub.yoti.com) to initialise the sandbox client.

Please do not open the pem file as this might corrupt the key and you will need to create a new sandbox key.

{% code %}
{% tab language="javascript" %}
const fs = require('fs');

const {
  SandboxProfileClientBuilder,
  SandboxAgeVerificationBuilder,
  TokenRequestBuilder,
} = require('@getyoti/sdk-sandbox');

const yoti = require('yoti');

const SANDBOX_CLIENT_SDK_ID = 'SANDBOX_CLIENT_SDK_ID';
const PEM = fs.readFileSync('/path/to/your-pem-file.pem');

const sandboxProfileClient = new SandboxProfileClientBuilder()
  .withClientSdkId(SANDBOX_CLIENT_SDK_ID)
  .withPemString(PEM)
  .build();
{% /tab %}
{% tab language="java" %}
import com.yoti.api.client.ClassPathKeySource;
import com.yoti.api.client.sandbox.YotiSandboxClient;
import com.yoti.api.client.sandbox.profile.request.YotiTokenRequest;
import com.yoti.api.client.sandbox.profile.request.attribute.SandboxAnchor;
import com.yoti.api.client.sandbox.profile.request.attribute.derivation.SandboxAgeVerification;

// Point the Yoti client at the sandbox by setting environment variable
System.setProperty("yoti.api.url", "https://api.yoti.com/sandbox/v1");

public static final String SANDBOX_URL = "https://api.yoti.com/sandbox/v1";
private static final String SANDBOX_CLIENT_SDK_ID = "SANDBOX_CLIENT_SDK_ID";
private static final String SANDOX_KEY_PAIR_FILE_NAME = "/path/to/your-pem-file.pem";

static {
    Security.insertProviderAt(new BouncyCastleProvider(), 1);
}

YotiSandboxClient yotiSandboxClient = YotiSandboxClient.builder()
                .forApplication(SANDBOX_CLIENT_SDK_ID)
                .withKeyPair(ClassPathKeySource.fromClasspath(SANDOX_KEY_PAIR_FILE_NAME))
                .build();
{% /tab %}
{% tab language="php" %}
<?php
use Yoti\Sandbox\Profile\SandboxClient;
use Yoti\Sandbox\Profile\Request\TokenRequestBuilder;
use Yoti\Sandbox\Profile\Request\Attribute\SandboxAgeVerification;

try {
    $sandboxClient = new SandboxClient('CLIENT_SDK_ID', '/path/to/your-pem-file.pem');
} catch(Exception $e) {
    // Handle unhappy path
}
{% /tab %}
{% tab language="python" %}
from yoti_python_sandbox import SandboxClientBuilder
from yoti_python_sandbox import SandboxAgeVerificationBuilder
from yoti_python_sandbox import YotiTokenRequestBuilder

sdk_id = "CLIENT_SDK_ID"
pem_file_location = "/path/to/your-pem-file.pem"

client = (SandboxClientBuilder()
          .for_application(sdk_id)
          .with_pem_file(pem_file_location)
          .build())
{% /tab %}
{% tab language="csharp" %}
Org.BouncyCastle.Crypto.AsymmetricCipherKeyPair keyPair;

using (StreamReader stream = File.OpenText("/path/to/your-pem-file.pem"))
{
	keyPair = Yoti.Auth.CryptoEngine.LoadRsaKey(stream);
}

const string sandboxClientSdkid = "CLIENT_SDK_ID";

SandboxClient sandboxClient = new SandboxClientBuilder()
	.WithClientSdkId(sandboxClientSdkid)
	.WithKeyPair(keyPair)
	.Build();
{% /tab %}
{% tab language="go" %}
import (
	"github.com/getyoti/yoti-go-sdk/v2"
	"github.com/getyoti/yoti-go-sdk/v2/cryptoutil"
	"github.com/getyoti/yoti-go-sdk/v2/file"
	"github.com/getyoti/yoti-go-sdk/v2/profile/sandbox"
)

sandboxClientSdkId := os.Getenv("SANDBOX_CLIENT_SDK_ID")
pemFileBytes, err := file.ReadFile(os.Getenv("YOTI_KEY_FILE_PATH"))
assert.NilError(t, err)	privateKey, err := cryptoutil.ParseRSAKey(pemFileBytes)
assert.NilError(t, err)	sandboxClient := sandbox.Client{
	ClientSdkID: sandboxClientSdkId,
	Key:         privateKey,
}
{% /tab %}
{% tab language="ruby" %}
require 'yoti'
require 'yoti_sandbox'

Yoti.configure do |config|
  config.client_sdk_id = 'SANDBOX_CLIENT_SDK_ID'
  config.key_file_path = '/path/to/your-pem-file.pem'
  config.api_endpoint = 'https://api.yoti.com/sandbox/v1'
end

sandbox_client = Yoti::Sandbox::Profile::Client.new
{% /tab %}
{% /code %}

### Generating a Token

To create a sandbox request, you must specify how you want your response to be provided. Below is an example of a simple sandbox request.

{% code %}
{% tab language="javascript" %}
const tokenRequest = new TokenRequestBuilder()
  .withRememberMeId('some remember me ID')
  .withGivenNames('some given names')
  .withFamilyName('some family name')
  .withFullName('some full name')
  .withDateOfBirthString('1980-01-01')
  .withGender('some gender')
  .withPhoneNumber('some phone number')
  .withNationality('some nationality')
  .withBase64Selfie('some base64 encoded selfie')
  .withEmailAddress('some@email')
  .withDocumentDetails('PASSPORT USA 1234abc')
  .build();
{% /tab %}
{% tab language="java" %}
YotiTokenRequest yotiTokenRequest = YotiTokenRequest.builder()
    .withRememberMeId("remember_me_maybe")
	  .withGivenNames("some given names")
	  .withFamilyName("some family name")
	  .withFullName("some full name")
	  .withDateOfBirth("1989-01-02")
	  .withGender("some gender")
    .withPhoneNumber("some phone number")
    .withNationality("some nationality")
    .withBase64Selfie("some base64 encoded selfie")
    .withEmailAddress("some@email")
    .withDocumentDetails("PASSPORT USA 1234abc")
    .build();
{% /tab %}
{% tab language="php" %}
<?php

$tokenRequest = (new TokenRequestBuilder())
        ->setRememberMeId('some remember me ID')
        ->setGivenNames('some given names')
        ->setFamilyName('some family name')
        ->setFullName('some full name')
        ->setDateOfBirth(new \DateTime('1980-01-01'))
        ->setGender('some gender')
        ->setPhoneNumber('some phone number')
        ->setNationality('some nationality')
        ->setBase64Selfie('some base64 encoded selfie')
        ->setEmailAddress('some@email')
        ->setDocumentDetailsWithString('PASSPORT USA 1234abc')
        ->build();
{% /tab %}
{% tab language="python" %}
import base64

selfie = base64.b46encode(b"Some Base64 Selfie Image").decode("utf-8")

token_request = (YotiTokenRequestBuilder()
                 .with_remember_me_id("some_remember_me_id")
                 .with_given_names("Some Given Names")
                 .with_family_name("Some Family Name")
                 .with_full_name("Some Full Name")
                 .with_date_of_birth("1980-01-01")
                 .with_gender("Some Gender")
                 .with_phone_number("Some Phone Number")
                 .with_nationality("Some Nationality")
                 .with_postal_address("Some Postal Address")
                 .with_base64_selfie(selfie)
                 .with_email_address("Some Email Address")
                 .with_document_details("PASSPORT USA 1234abc")
                 .build())
{% /tab %}
{% tab language="csharp" %}
YotiTokenRequest tokenRequest = new YotiTokenRequestBuilder()
	.WithRememberMeId("some Remember Me ID")
	.WithGivenNames("some given names")
	.WithFamilyName("some family name")
	.WithFullName("some full name")
	.WithDateOfBirth(new DateTime(1980, 10, 30))
	.WithGender("some gender")
	.WithPhoneNumber("some phone number")
	.WithNationality("some nationality")
	.WithBase64Selfie(Convert.ToBase64String(Encoding.UTF8.GetBytes("some base64 encoded selfie")))
	.WithEmailAddress("some@email")
	.WithDocumentDetails("PASSPORT USA 1234abc")
	.Build();
{% /tab %}
{% tab language="go" %}
tokenRequest := (&sandbox.TokenRequest{}).
	WithRememberMeID("remember_me_id_12345").
	WithAgeVerification(dateOfBirthUnder18, sandbox.Derivation{}.AgeUnder(18), nil).
	WithGivenNames("some given names", nil).
	WithFamilyName("some family name", nil).
	WithFullName("some full name", nil).
	WithDateOfBirth(dateOfBirthUnder18, nil).
	WithGender("some gender", nil).
	WithPhoneNumber("some phone number", nil).
	WithNationality("some nationality", nil).
	WithStructuredPostalAddress(
		map[string]interface{}{
			"building_number": "1",
			"address_line1":   "some street name",
		}, nil).
	WithBase64Selfie(base64.StdEncoding.EncodeToString([]byte("some_image_value")), nil).
	WithEmailAddress("some@email", nil).
	WithDocumentDetails("PASSPORT USA 1234abc", nil)
{% /tab %}
{% tab language="ruby" %}
token_request = Yoti::Sandbox::Profile::TokenRequestBuilder.new
  .with_remember_me_id('some_remember_me_id')
  .with_given_names('Some Given Names', anchors: anchors)
  .with_family_name('Some Family Name', anchors: anchors)
  .with_full_name('Some Full Name', anchors: anchors)
  .with_date_of_birth(DateTime.new(1989, 1, 2), anchors: anchors)
  .with_gender('Some Gender', anchors: anchors)
  .with_phone_number('Some Phone Number')
  .with_nationality('Some Nationality', anchors: anchors)
  .with_postal_address('Some Postal Address')
  .with_base64_selfie(Base64.strict_encode64('Some Selfie'))
  .with_email_address('some@email.address')
  .with_document_details('PASSPORT USA 1234abc', anchors: anchors)
  .build
{% /tab %}
{% /code %}

Familiarise yourself with the [auto$](/digital-id-legacy/yoti-attributes). For advanced attribute generation please see below.

---

### Reading the Request

Once you have generated a sandbox token, this can be used in the same way as the standard Web Integration.

{% code %}
{% tab language="javascript" %}
sandboxProfileClient.setupSharingProfile(tokenRequest)
  .then((response) => {
    const token = response.getToken();

    // Use token to get activity details.
    const yotiClient = new yoti.Client(SANDBOX_CLIENT_SDK_ID, PEM, {
        apiUrl: 'https://api.yoti.com/sandbox/v1' // Set client to Sandbox
    });
    yotiClient.getActivityDetails(token)
      .then((activityDetails) => {
        // Handle response here.
      });
  })
  .catch((err) => {
    // Handle unhappy path.
  });
{% /tab %}
{% tab language="java" %}
String sharingToken = yotiSandboxClient.setupSharingProfile(yotiTokenRequest);

// Point the Doc Scan client at the sandbox by setting environment variable
System.setProperty("yoti.api.url", SANDBOX_URL);

YotiClient yotiClient = YotiClient.builder()
        .withClientSdkId(SANDBOX_CLIENT_SDK_ID)
        .withKeyPair(ClassPathKeySource.fromClasspath(SANDOX_KEY_PAIR_FILE_NAME))
        .build();

HumanProfile result = yotiClient.getActivityDetails(sharingToken).getUserProfile();
{% /tab %}
{% tab language="php" %}
<?php

$token = $sandboxClient->setupSharingProfile($tokenRequest)->getToken();

$yotiClient = new YotiClient('SANDBOX_CLIENT_SDK_ID', '/path/to/your-pem-file.pem', [
    'api.url' => 'https://api.yoti.com/sandbox/v1'
]);

$activityDetails = $yotiClient->getActivityDetails($token);
{% /tab %}
{% tab language="python" %}
from yoti_python_sdk import Client
import yoti_python_sdk

yoti_python_sdk.YOTI_API_ENDPOINT = "https://api.yoti.com/sandbox/v1"

client = Client(YOTI_CLIENT_SDK_ID, YOTI_KEY_FILE_PATH)

token_response = sandboxClient.setup_sharing_profile(token_request)
token = token_response.token

activity_details = client.get_activity_details(token)
{% /tab %}
{% tab language="csharp" %}
var sandboxOneTimeUseToken = sandboxClient.SetupSharingProfile(tokenRequest);

var yotiClient = new YotiClient(new HttpClient(), sandboxClientSdkid, keyPair);

Uri sandboxUri = new UriBuilder(
	"https",
	"api.yoti.com",
	443,
	"sandbox/v1").Uri;

yotiClient.OverrideApiUri(sandboxUri);

ActivityDetails activityDetails = yotiClient.GetActivityDetails(sandboxOneTimeUseToken);

// Perform tests
Assert.AreEqual("some@email", activityDetails.Profile.EmailAddress.GetValue());
{% /tab %}
{% tab language="go" %}
sandboxToken, err := sandboxClient.SetupSharingProfile(tokenRequest)
assert.NilError(t, err)	yotiClient := yoti.Client{
	Key:   pemFileBytes,
	SdkID: sandboxClientSdkId,
}
yotiClient.OverrideAPIURL("https://api.yoti.com/sandbox/v1")	activityDetails, errStrings := yotiClient.GetActivityDetails(sandboxToken)
if len(errStrings) > 0 {
	log.Fatalf("%v", errStrings)
}	assert.Equal(t, "some@email", activityDetails.UserProfile.EmailAddress().Value())
{% /tab %}
{% tab language="ruby" %}
# Initilise Yoti Client with Sandbox URL
Yoti.configure do |config|
  config.client_sdk_id = ENV['YOTI_SANDBOX_CLIENT_SDK_ID']
  config.key_file_path = ENV['YOTI_KEY_FILE_PATH']
  config.api_endpoint = 'https://api.yoti.com/sandbox/v1'
end

token = sandbox_client.setup_sharing_profile(token_request)

activity_details = Yoti::Client.get_activity_details(token)
{% /tab %}
{% tab language="java" title="Java v2" %}
String sharingToken = yotiSandboxClient.setupSharingProfile(yotiTokenRequest);

// Point the Doc Scan client at the sandbox by setting environment variable
System.setProperty("yoti.api.url", "https://api.yoti.com/sandbox/v1");

YotiClient yotiClient = YotiClientBuilder.newInstance()
    .forApplication(<YOTI_CLIENT_SDK_ID>)
    .withKeyPair(FileKeyPairSource.fromFile(new File("<YOTI_KEY_FILE_PATH>")))
    .build();

HumanProfile result = yotiClient.getActivityDetails(sharingToken).getUserProfile();
{% /tab %}
{% /code %}

{% html %}
<div class="alert-GTK">

    <div class="alert-title" id="GTK">

        Good to know

    </div>

    <div class="alert-text">

        Guidance or a refresher on the full Yoti client, please see our web integration section.

    </div>

    <div class="alert-links"> 

        <a href="https://developers.yoti.com/digital-id/retrieve-the-profile">Retrieve a profile</a>


   </div>

</div>
{% /html %}

This concludes the basic Sandbox Integration for the Digital ID.

---

## Advanced Test cases

Now that you're familiar with creating a simple sandbox request it's important to know that there are some additional features in the SDK which can be utilised to create powerful tests. In this section we'll cover:

- Source and verifiers
- Address
- Age verification

### Source and verifiers

If you're familiar with a Yoti app share, you'll recognise that an attribute contains additional data, such as the **Source** of the **Attribute** and the **Verifier**. These are known as **Anchors**. Please see below for an example of attaching Anchors to your sandbox attributes.

{% code %}
{% tab language="javascript" %}
const {
    YotiDate,
  } = require('yoti');

const {
    SandboxAnchorBuilder,
    TokenRequestBuilder,
} = require('@getyoti/sdk-sandbox');

const anchors = [
    new SandboxAnchorBuilder()
        .withType('SOURCE')
        .withSubType('')
        .withTimestamp(YotiDate.fromDateString('2020-01-01T00:00:00Z'))
        .withValue('PASSPORT')
        .build(),
    new SandboxAnchorBuilder()
        .withType('VERIFIER')
        .withSubType('')
        .withTimestamp(YotiDate.fromDateString('2020-01-01T00:00:00Z'))
        .withValue('YOTI_ADMIN')
        .build(),
];

const tokenRequest = new TokenRequestBuilder()
    .withDocumentDetails('PASSPORT USA 1234abc', anchors)
    .build();
{% /tab %}
{% tab language="java" title="Java v2" %}
import static java.util.Arrays.asList;

...

TIME_VALUE = TimeValue.builder()
            .withHour(15)
            .withMinute(59)
            .withSecond(23)
            .withMicrosecond(654321)
            .build();

DATE_VALUE = DateValue.builder()
            .withYear(1966)
            .withMonth(7)
            .withDay(30)
            .build();

SandboxAnchor SOURCE_ANCHOR = SandboxAnchor.builder()
    .withType("SOURCE")
    .withSubType("")
    .withTimestamp(new DateTimeValue(DATE_VALUE, TIME_VALUE))
    .withValue("PASSPORT")
    .build();

SandboxAnchor VERIFIER_ANCHOR = SandboxAnchor.builder()
    .withType("VERIFIER")
    .withSubType("")
    .withTimestamp(UTC_CALENDAR.getTimeInMillis())
    .withValue("YOTI_ADMIN")
    .build();

YotiTokenRequest yotiTokenRequest = YotiTokenRequest.builder()
    .withDocumentDetails('PASSPORT USA 1234abc', asList(SOURCE_ANCHOR, VERIFIER_ANCHOR))
    .build();

...
{% /tab %}
{% tab language="php" %}
use Yoti\Sandbox\Profile\Request\Attribute\SandboxAnchor;
use Yoti\Sandbox\Profile\Request\TokenRequestBuilder;

$anchors = [
    new SandboxAnchor('SOURCE', 'PASSPORT', '', new \DateTime()),
    new SandboxAnchor('VERIFIER', 'YOTI_ADMIN', '', new \DateTime()),
];

$tokenRequest = (new TokenRequestBuilder())
    ->setDocumentDetailsWithString('PASSPORT USA 1234abc', $anchors)
    ->build();
{% /tab %}
{% tab language="python" %}
from datetime import datetime

from yoti_python_sandbox import YotiTokenRequestBuilder
from yoti_python_sandbox.anchor import SandboxAnchor

TIMESTAMP_VALUE = datetime.utcnow()

SOURCE_ANCHOR = SandboxAnchor.builder()\
    .with_type("SOURCE")\
    .with_sub_type("")\
    .with_timestamp(TIMESTAMP_VALUE)\
    .with_value("PASSPORT")\
    .build()

VERIFIER_ANCHOR = SandboxAnchor.builder()\
    .with_type("VERIFIER")\
    .with_sub_type("")\
    .with_timestamp(TIMESTAMP_VALUE)\
    .with_value("YOTI_ADMNIN")\
    .build()

token_request = (YotiTokenRequestBuilder()
                 .with_document_details("PASSPORT USA 1234abc", [SOURCE_ANCHOR, VERIFIER_ANCHOR])
                 .build())
{% /tab %}
{% tab language="csharp" %}
List<SandboxAnchor> anchors = new List<SandboxAnchor> { SandboxAnchor.Builder().Build() };

YotiTokenRequest yotiTokenRequest = YotiTokenRequest.Builder()
                    .WithDocumentDetails("PASSPORT USA 1234abc", anchors)
                    .Build();
{% /tab %}
{% tab language="go" %}
import (
    "time"
    "github.com/getyoti/yoti-go-sdk/v2/profile/sandbox"
)

sourceAnchor := sandbox.SourceAnchor("NFC", time.Now().UTC(), "PASSPORT")
verifierAnchor := sandbox.VerifierAnchor("", time.Now().UTC(), "YOTI_ADMIN")

tokenRequest := sandbox.TokenRequest{}.
    WithDocumentDetails("PASSPORT USA 1234abc", []sandbox.Anchor{sourceAnchor, verifierAnchor})
{% /tab %}
{% tab language="ruby" %}
require 'yoti_sandbox'

anchors = [
    Yoti::Sandbox::Profile::Anchor.source('PASSPORT'),
    Yoti::Sandbox::Profile::Anchor.verifier('YOTI_ADMIN')
]

token_request = Yoti::Sandbox::Profile::TokenRequestBuilder.new
    .with_document_details('PASSPORT USA 1234abc', anchors: anchors)
    .build
{% /tab %}
{% tab language="java" %}
import static java.util.Arrays.asList;
import com.yoti.api.client.Date;
import com.yoti.api.client.Time;
import com.yoti.api.client.DateTime;

...

Time TIME_VALUE = Time.builder()
    .withHour(15)
    .withMinute(59)
    .withSecond(23)
    .withMicrosecond(654321)
    .build();

Date DATE_VALUE = Date.builder()
    .withYear(1966)
    .withMonth(7)
    .withDay(30)
    .build();

SandboxAnchor SOURCE_ANCHOR = SandboxAnchor.builder()
   .withType("SOURCE")
   .withSubType("")
   .withTimestamp(new DateTime(DATE_VALUE, TIME_VALUE))
   .withValue("PASSPORT")
    .build();

final Calendar UTC_CALENDAR = Calendar.getInstance(TimeZone.getTimeZone("UTC"));
SandboxAnchor VERIFIER_ANCHOR = SandboxAnchor.builder()
    .withType("VERIFIER")
    .withSubType("")
    .withTimestamp(UTC_CALENDAR.getTimeInMillis())
    .withValue("YOTI_ADMIN")
    .build();

YotiTokenRequest yotiTokenRequest = YotiTokenRequest.builder()
    .withDocumentDetails("PASSPORT USA 1234abc", asList(SOURCE_ANCHOR, VERIFIER_ANCHOR))
    .build();

...
{% /tab %}
{% /code %}

### Address

Yoti use a set format depending on the **Address** region. In order to create tests for the structured postal address, we recommended referring to the Yoti formats below.

An example of building a structured postal address is shown below:

{% code %}
{% tab language="javascript" %}
const tokenRequest = new TokenRequestBuilder()
    .withStructuredPostalAddress(
        JSON.stringify({
            building_number: 46,
            building_name: 'Shelley Court',
            sub_building: 'Flat 2',
            address_line1: 'Flat 2',
            address_line2: 'Shelley Court',
            address_line3: '46 Nowhere',
            locality: 'Nowhere Town',
            administrative_area_l1: 'Nowhere',
            postal_code: 'RG1 5DG',
            country: 'GBR',
            formatted_address: 'Flat 2 Shelley Court 46 Nowhere Town Nowhere RG1 5DG GBR',
        }),
    )
    .build();
{% /tab %}
{% tab language="java" %}
public static final Map<String, String> STRUCTURED_POSTAL_ADDRESS_ATTRIBUTE_VALUE;

static {
        STRUCTURED_POSTAL_ADDRESS_ATTRIBUTE_VALUE = new HashMap<>();
        STRUCTURED_POSTAL_ADDRESS_ATTRIBUTE_VALUE.put("building_number", "46");
        STRUCTURED_POSTAL_ADDRESS_ATTRIBUTE_VALUE.put("building_name", "Shelley Court");
        STRUCTURED_POSTAL_ADDRESS_ATTRIBUTE_VALUE.put("sub_building", "Flat 2");
        STRUCTURED_POSTAL_ADDRESS_ATTRIBUTE_VALUE.put("address_line1", "Flat 2");
        STRUCTURED_POSTAL_ADDRESS_ATTRIBUTE_VALUE.put("address_line2", "Shelley Court");
        STRUCTURED_POSTAL_ADDRESS_ATTRIBUTE_VALUE.put("address_line3", "46 Nowhere");
        STRUCTURED_POSTAL_ADDRESS_ATTRIBUTE_VALUE.put("locality", "Nowhere Town");
        STRUCTURED_POSTAL_ADDRESS_ATTRIBUTE_VALUE.put("administrative_area_l1", "Nowhere");
        STRUCTURED_POSTAL_ADDRESS_ATTRIBUTE_VALUE.put("postal_code", "RG1 5DG");
        STRUCTURED_POSTAL_ADDRESS_ATTRIBUTE_VALUE.put("country", "GBR");
        STRUCTURED_POSTAL_ADDRESS_ATTRIBUTE_VALUE.put("formatted_address", "Flat 2 Shelley Court 46 Nowhere Town Nowhere RG1 5DG GBR ");
    }

YotiTokenRequest yotiTokenRequest = YotiTokenRequest.builder()
                .withStructuredPostalAddress(toJson(STRUCTURED_POSTAL_ADDRESS_ATTRIBUTE_VALUE))
                .build();
{% /tab %}
{% tab language="php" %}
<?php

$tokenRequest = (new TokenRequestBuilder())
	->setStructuredPostalAddress(json_encode([
	        'building_number' => 46,
            'building_name' => 'Shelley Court',
            'sub_building' => 'Flat 2',
            'address_line1' => 'Flat 2',
            'address_line2' => 'Shelley Court',
            'address_line3' => '46 Nowhere',
            'locality' => 'Nowhere Town',
            'administrative_area_l1' => 'Nowhere',
            'postal_code' => 'RG1 5DG',
            'country' => 'GBR',
            'formatted_address' => 'Flat 2 Shelley Court 46 Nowhere Town Nowhere RG1 5DG GBR',
	]))
->build();
{% /tab %}
{% tab language="python" %}
token_request = (YotiTokenRequestBuilder()
.with_structured_postal_address(json.dumps({
  "building_number":46,
  "building_name":"Shelley Court",
  "sub_building":"Flat 2",
  "address_line1":"Flat 2",
  "address_line2":"Shelley Court",
  "address_line3":"46 Nowhere",
  "locality":"Nowhere Town",
  "administrative_area_l1":"Nowhere",
  "postal_code":"RG1 5DG",
  "country":"GBR",
  "formatted_address":"Flat 2 Shelley Court 46 Nowhere Town Nowhere RG1 5DG GBR"
}))
.build())
{% /tab %}
{% tab language="csharp" %}
YotiTokenRequest tokenRequest = new YotiTokenRequestBuilder()
	.WithStructuredPostalAddress(Newtonsoft.Json.JsonConvert.SerializeObject(new
	{
        building_number = 46,
        building_name = 'Shelley Court',
        sub_building = 'Flat 2',
        address_line1 = 'Flat 2',
        address_line2 = 'Shelley Court',
        address_line3 = '46 Nowhere',
        locality = 'Nowhere Town',
        administrative_area_l1 = 'Nowhere',
        postal_code = 'RG1 5DG',
        country = 'GBR',
        formatted_address = 'Flat 2 Shelley Court 46 Nowhere Town Nowhere RG1 5DG GBR'
	}))
	.Build();
{% /tab %}
{% tab language="go" %}
tokenRequest := (&sandbox.TokenRequest{}).
	WithStructuredPostalAddress(
		map[string]interface{}{
			"building_number": "1",
			"address_line1":   "some street name",
		}, nil)
{% /tab %}
{% tab language="ruby" %}
token_request = Yoti::Sandbox::Profile::TokenRequestBuilder.new
      .with_structured_postal_address(
        {
          'building_number' => 1,
          'address_line1' => 'Some Address'
        },
        anchors: anchors
      )
      .build
{% /tab %}
{% /code %}

### Age Verification

A common use case with the Yoti app is using the **Age Over** attribute. Testing this with the Sandbox involves creating an **Age Verification** sandbox attribute.

{% code %}
{% tab language="javascript" %}
const {
  SandboxAgeVerificationBuilder,
  TokenRequestBuilder,
} = require('@getyoti/sdk-sandbox');

const ageVerification = new SandboxAgeVerificationBuilder()
  .withDateOfBirthString('1980-01-01')
  .withAgeOver(18)
  .build();

const tokenRequest = new TokenRequestBuilder()
  .withAgeVerification(ageVerification)
  .build();
{% /tab %}
{% tab language="java" %}
import com.yoti.api.client.spi.remote.DateValue;

import com.yoti.api.client.sandbox.profile.request.attribute.derivation.SandboxAgeVerification;
import com.yoti.api.client.sandbox.profile.request.YotiTokenRequest;

SandboxAgeVerification sandboxAgeVerification = SandboxAgeVerification.builder()
        .withDateOfBirth(DateValue.parseFrom("1989-01-02"))
        .withAgeOver(18)
        .build();
YotiTokenRequest yotiTokenRequest = YotiTokenRequest.builder()
        .withAgeVerification(sandboxAgeVerification)
        .build();
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\Sandbox\Profile\Request\TokenRequestBuilder;
use Yoti\Sandbox\Profile\Request\Attribute\SandboxAgeVerification;

    $ageVerification = SandboxAgeVerification::forAgeOver(
        18,
        new \DateTime('1980-01-01')
    );

    $tokenRequest = (new TokenRequestBuilder())
        ->setAgeVerification($ageVerification)
        ->build();
{% /tab %}
{% tab language="python" %}
from yoti_python_sandbox import SandboxAgeVerificationBuilder
from yoti_python_sandbox import YotiTokenRequestBuilder

age_verification = (SandboxAgeVerificationBuilder()
                    .with_date_of_birth("1989-01-02")
                    .with_age_over(18)
                    .build())

token_request = (YotiTokenRequestBuilder()
                 .with_age_verification(age_verification)
                 .build())
{% /tab %}
{% tab language="csharp" %}
SandboxAgeVerification ageVerification = new SandboxAgeVerificationBuilder()
	.WithDateOfBirth(new DateTime(2001, 12, 31))
	.WithAgeOver(18)
	.Build();

YotiTokenRequest tokenRequest = new YotiTokenRequestBuilder()
	.WithAgeVerification(ageVerification)
	.Build();
{% /tab %}
{% tab language="go" %}
var dateOfBirthUnder18 = time.Now().AddDate(-10, 0, 0)

tokenRequest := (&sandbox.TokenRequest{}).
	WithAgeVerification(dateOfBirthUnder18, sandbox.Derivation{}.AgeUnder(18), nil).
{% /tab %}
{% tab language="ruby" %}
age_verification = Yoti::Sandbox::Profile::AgeVerificationBuilder.new
      .with_date_of_birth(DateTime.new(1989, 1, 2))
      .with_age_over(18)
      .build

token_request = Yoti::Sandbox::Profile::TokenRequestBuilder.new
      .build
{% /tab %}
{% /code %}

---

## Go Live

Once you have tested our sandbox please return to our integration guide.

If you have any other questions please do not hesitate to contact us through our [support form](https://support.yoti.com/yotisupport/s/contactsupport)

_Once we have answered your question we may contact you again to discuss Yoti products and services. If you’d prefer us not to do this, please let us know when you e-mail._