---
type: page
title: Create a Session
listed: true
slug: generating-a-session
description: 
index_title: Create a Session
hidden: 
keywords: 
tags: 
---

Every time an end user elects to supply a document(s) on the relying party app/website/custom product, you will need to create a  [session](/yoti/terminology) with Yoti to perform the ID checks.

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      You will need the Yoti App on your phone and to have registered your business with Yoti.
   </div>
   <div class="alert-links"> 
      <a  target="_self" href="https://developers.yoti.com/yoti/getting-started-hub"> Onboarding with Yoti </a>
      <a  target="_self" href="https://developers.yoti.com/yoti/generate-api-keys"> Generate API keys </a>
   </div>
</div>
{% /html %}

This section covers:

- [Quick Start](https://developers.yoti.com/yoti/generating-a-session#quick-start) configuration 

OR

- [Installing the SDK](https://developers.yoti.com/yoti/generating-a-session#installing-our-sdk)
- [Creating the session](https://developers.yoti.com/yoti/generating-a-session#creating-the-session) - Step by step guide.

---

## Quick Start

Below is an example of a complete request snippet in different languages. The documentation continues to outline the full request in step by step detail.

**Installing the SDK**

{% code %}
{% tab language="javascript" %}
npm install -S -E yoti
{% /tab %}
{% tab language="java" %}
// If you are using Maven, add the following dependency:
<dependency>
    <groupId>com.yoti</groupId>
    <artifactId>yoti-sdk-impl</artifactId>
    <version>2.9.0</version>
</dependency>

// If you are using Gradle, add the following dependency:
compile group: 'com.yoti', name: 'yoti-sdk-impl', version: '2.9.0'
{% /tab %}
{% tab language="php" %}
// Get the Yoti PHP SDK library via a Composer package
composer require yoti/yoti-php-sdk
{% /tab %}
{% tab language="python" %}
pip install yoti
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
// You can simply add a `require github.com/getyoti/yoti-go-sdk/v2` to go.mod.
// To download and install the Yoti SDK and its dependencies, run the following command from your terminal:

go get "github.com/getyoti/yoti-go-sdk/v3"
{% /tab %}
{% tab language="ruby" %}
gem install yoti

# The gem provides a configuration generator for Ruby on Rails:

rails generate yoti:install
{% /tab %}
{% /code %}

**Full example**

{% code %}
{% tab language="javascript" %}
const path = require('path');
const fs = require('fs');

const {
    DocScanClient,
    SessionSpecificationBuilder,
    RequestedDocumentAuthenticityCheckBuilder,
    RequestedLivenessCheckBuilder,
    RequestedTextExtractionTaskBuilder,
    RequestedFaceMatchCheckBuilder,
    SdkConfigBuilder,
    NotificationConfigBuilder,
} = require('yoti');

const YOTI_CLIENT_SDK_ID = 'YOTI_CLIENT_SDK_ID';
const YOTI_PEM = fs.readFileSync(path.join(__dirname, '/path/to/pem'));
const docScanClient = new DocScanClient(YOTI_CLIENT_SDK_ID, YOTI_PEM);
const documentAuthenticityCheck = new RequestedDocumentAuthenticityCheckBuilder().build();
const livenessCheck = new RequestedLivenessCheckBuilder()
    .forZoomLiveness()
    .withMaxRetries(3)
    .build();

const faceMatchCheck = new RequestedFaceMatchCheckBuilder()
    .withManualCheckFallback()
    .build();

const textExtractionTask = new RequestedTextExtractionTaskBuilder()
    .withManualCheckFallback()
    .build();

const sdkConfig = new SdkConfigBuilder()
    .withAllowsCameraAndUpload()
    .withPrimaryColour('#2d9fff')
    .withSecondaryColour('#FFFFFF')
    .withFontColour('#FFFFFF')
    .withLocale('en-GB')
    .withPresetIssuingCountry('GBR')
    .withSuccessUrl('/success')
    .withErrorUrl('/error')
    .build();

const notificationConfig = new NotificationConfigBuilder()
    .withEndpoint('https://yourdomain.example/idverify/updates')
    .withAuthToken('username:password')
    .forResourceUpdate()
    .forTaskCompletion()
    .forCheckCompletion()
    .forSessionCompletion()
    .build();

const sessionSpec = new SessionSpecificationBuilder()
    .withClientSessionTokenTtl(600)
    .withResourcesTtl(90000)
    .withUserTrackingId('some-user-tracking-id')
    .withRequestedCheck(documentAuthenticityCheck)
    .withRequestedCheck(livenessCheck)
    .withRequestedCheck(faceMatchCheck)
    .withRequestedTask(textExtractionTask)
    .withSdkConfig(sdkConfig)
    .withNotifications(notificationConfig)
    .build();

docScanClient
    .createSession(sessionSpec)
    .then((session) => {
        const sessionId = session.getSessionId();
        const clientSessionToken = session.getClientSessionToken();
        const clientSessionTokenTtl = session.getClientSessionTokenTtl();
    })
    .catch((err) => {
        // handle err
    });
{% /tab %}
{% tab language="java" %}
import com.yoti.api.client.ClassPathKeySource;
import com.yoti.api.client.docs.DocScanClient;
import com.yoti.api.client.docs.DocScanClientBuilder;
import com.yoti.api.client.docs.DocScanException;
import com.yoti.api.client.docs.session.create.*;
import com.yoti.api.client.docs.session.create.check.RequestedCheckBuilderFactory;
import com.yoti.api.client.docs.session.create.task.RequestedTaskBuilderFactory;

...
DocScanClient docScanClient = DocScanClientBuilder.newInstance()
        .withClientSdkId("YOUR_SDK_ID")
        .withKeyPairSource(ClassPathKeySource.fromClasspath("/path/to/pem"))
        .build();

SdkConfigBuilderFactory SDK_CONFIG_BUILDER_FACTORY = SdkConfigBuilderFactory.newInstance();
SessionSpecBuilderFactory SESSION_SPEC_BUILDER_FACTORY = SessionSpecBuilderFactory.newInstance();
RequestedCheckBuilderFactory REQUESTED_CHECK_BUILDER_FACTORY = RequestedCheckBuilderFactory.newInstance();
RequestedTaskBuilderFactory REQUESTED_TASK_BUILDER_FACTORY = RequestedTaskBuilderFactory.newInstance();
NotificationConfigBuilderFactory NOTIFICATION_CONFIG_BUILDER_FACTORY = NotificationConfigBuilderFactory.newInstance();

SdkConfig sdkConfig = SDK_CONFIG_BUILDER_FACTORY.create()
        .withAllowsCameraAndUpload()
        .withPrimaryColour("#2d9fff")
        .withSecondaryColour("#FFFFFF")
        .withFontColour("#FFFFFF")
        .withLocale("en-GB")
        .withPresetIssuingCountry("GBR")
        .withSuccessUrl("https://localhost:8443/success")
        .withErrorUrl("https://localhost:8443/error")
        .build();

SessionSpec sessionSpec = SESSION_SPEC_BUILDER_FACTORY.create()
        .withClientSessionTokenTtl(600)
        .withResourcesTtl(90000)
        .withUserTrackingId("some-user-tracking-id")
        .withSdkConfig(sdkConfig)
        .withRequestedCheck(
                REQUESTED_CHECK_BUILDER_FACTORY
                        .forDocumentAuthenticityCheck()
                        .build()
        )
        .withRequestedCheck(
                REQUESTED_CHECK_BUILDER_FACTORY
                        .forFaceMatchCheck()
                        .withManualCheckFallback()
                        .build()
        )
        .withRequestedCheck(
                REQUESTED_CHECK_BUILDER_FACTORY
                        .forLivenessCheck()
                        .forZoomLiveness()
                        .withMaxRetries(1)
                        .build()
        )
        .withRequestedTask(
                REQUESTED_TASK_BUILDER_FACTORY
                        .forTextExtractionTask()
                        .withManualCheckAlways()
                        .build()
        )
        .withNotifications(
                NOTIFICATION_CONFIG_BUILDER_FACTORY.create()
                        .withEndpoint("https://yourdomain.example/idverify/updates")
                        .withAuthToken("some_auth_token")
                        .forResourceUpdate()
                        .forTaskCompletion()
                        .forCheckCompletion()
                        .forSessionCompletion()
                        .build()
        )
        .build();

CreateSessionResult sessionResult = docScanClient.createSession(sessionSpec);
...
{% /tab %}
{% tab language="php" %}
<?php

require_once './vendor/autoload.php';

use Yoti\DocScan\DocScanClient;
use Yoti\DocScan\Session\Create\Check\RequestedDocumentAuthenticityCheckBuilder;
use Yoti\DocScan\Session\Create\Check\RequestedFaceMatchCheckBuilder;
use Yoti\DocScan\Session\Create\Check\RequestedLivenessCheckBuilder;
use Yoti\DocScan\Session\Create\SdkConfigBuilder;
use Yoti\DocScan\Session\Create\SessionSpecificationBuilder;
use Yoti\DocScan\Session\Create\Task\RequestedTextExtractionTaskBuilder;
use Yoti\DocScan\Session\Create\NotificationConfigBuilder;

$YOTI_CLIENT_SDK_ID = 'YOTI_CLIENT_SDK_ID';
$YOTI_PEM = '/path/to/pem';

$client = new DocScanClient($YOTI_CLIENT_SDK_ID, $YOTI_PEM);

$sessionSpec = (new SessionSpecificationBuilder())
    ->withClientSessionTokenTtl(600)
    ->withResourcesTtl(90000)
    ->withUserTrackingId('some-user-tracking-id')
    ->withRequestedCheck(
        (new RequestedDocumentAuthenticityCheckBuilder())
            ->build()
    )
    ->withRequestedCheck(
        (new RequestedLivenessCheckBuilder())
            ->forZoomLiveness()
            ->build()
    )
    ->withRequestedCheck(
        (new RequestedFaceMatchCheckBuilder())
            ->withManualCheckFallback()
            ->build()
    )
    ->withRequestedTask(
        (new RequestedTextExtractionTaskBuilder())
            ->withManualCheckAlways()
            ->build()
    )
    ->withSdkConfig(
        (new SdkConfigBuilder())
            ->withAllowsCameraAndUpload()
            ->withPrimaryColour('#2d9fff')
            ->withSecondaryColour('#FFFFFF')
            ->withFontColour('#FFFFFF')
            ->withLocale('en-GB')
            ->withPresetIssuingCountry('GBR')
            ->withSuccessUrl('/your/success/url')
            ->withErrorUrl('/your/error/url')
            ->build()
    )
    ->withNotifications(
        (new NotificationConfigBuilder())
            ->withEndpoint('https://yourdomain.example/idverify/updates')
            ->withAuthToken('username:password')
            ->forResourceUpdate()
            ->forTaskCompletion()
            ->forCheckCompletion()
            ->forSessionCompletion()
            ->build()
    )
    ->build();

$session = $client->createSession($sessionSpec);
{% /tab %}
{% tab language="python" %}
from yoti_python_sdk.doc_scan import (
    DocScanClient,
    RequestedDocumentAuthenticityCheckBuilder,
    RequestedFaceMatchCheckBuilder,
    RequestedLivenessCheckBuilder,
    RequestedTextExtractionTaskBuilder,
    SdkConfigBuilder,
    SessionSpecBuilder,
    NotificationConfigBuilder
)

YOTI_CLIENT_SDK_ID = 'YOTI_CLIENT_SDK_ID'
YOTI_PEM = '/path/to/pem'

doc_scan_client = DocScanClient(YOTI_CLIENT_SDK_ID, YOTI_PEM)

sdk_config = (
    SdkConfigBuilder()
    .with_allows_camera_and_upload()
    .with_primary_colour("#2d9fff")
    .with_secondary_colour("#FFFFFF")
    .with_font_colour("#FFFFFF")
    .with_locale("en-GB")
    .with_preset_issuing_country("GBR")
    .with_success_url("/your/success/url")
    .with_error_url("/your/error/url")
    .build()
)

notification_config = (
    NotificationConfigBuilder()
    .with_endpoint('https://yourdomain.example/idverify/updates')
    .with_auth_token('username:password')
    .for_resource_update()
    .for_task_completion()
    .for_check_completion()
    .for_session_completion()
    .build()
)

session_spec = (
    SessionSpecBuilder()
    .with_client_session_token_ttl(600)
    .with_resources_ttl(90000)
    .with_user_tracking_id("some-user-tracking-id")
    .with_requested_check(RequestedDocumentAuthenticityCheckBuilder().build())
    .with_requested_check(
        RequestedLivenessCheckBuilder()
        .for_zoom_liveness()
        .with_max_retries(1)
        .build()
    )
    .with_requested_check(
        RequestedFaceMatchCheckBuilder().with_manual_check_fallback().build()
    )
    .with_requested_task(
        RequestedTextExtractionTaskBuilder().with_manual_check_always().build()
    )
    .with_sdk_config(sdk_config)
    .with_notifications(notification_config)
    .build()
)

session = doc_scan_client.create_session(session_spec)
{% /tab %}
{% tab language="csharp" %}
using System.IO;
using System.Net.Http;
using Yoti.Auth;
using Yoti.Auth.DocScan;
using Yoti.Auth.DocScan.Session.Create;
using Yoti.Auth.DocScan.Session.Create.Check;
using Yoti.Auth.DocScan.Session.Create.Task;

...
const string YOTI_CLIENT_SDK_ID = "YOTI_CLIENT_SDK_ID";
const string PEM_PATH = "/path/to/pem";

StreamReader privateKeyStream = System.IO.File.OpenText(PEM_PATH);
var key = CryptoEngine.LoadRsaKey(privateKeyStream);

var docScanClient = new DocScanClient(YOTI_CLIENT_SDK_ID, key, new HttpClient());

var sessionSpec = new SessionSpecificationBuilder()
    .WithClientSessionTokenTtl(600)
    .WithResourcesTtl(90000)
    .WithUserTrackingId("some-user-tracking-id")
    .WithRequestedCheck(
        new RequestedDocumentAuthenticityCheckBuilder()
        .Build()
    )
    .WithRequestedCheck(
        new RequestedLivenessCheckBuilder()
        .ForZoomLiveness()
        .Build()
    )
    .WithRequestedCheck(
        new RequestedFaceMatchCheckBuilder()
        .WithManualCheckFallback()
        .Build()
    )
    .WithRequestedTask(
        new RequestedTextExtractionTaskBuilder()
        .WithManualCheckAlways()
        .Build()
    )
    .WithNotifications(
        new NotificationConfigBuilder()
        .WithEndpoint("https://yourdomain.example/idverify/updates")
        .WithAuthToken("username:password")
        .ForResourceUpdate()
        .ForTaskCompletion()
        .ForCheckCompletion()
        .ForSessionCompletion()
        .Build()
    )
    .WithSdkConfig(
        new SdkConfigBuilder()
        .WithAllowsCameraAndUpload()
        .WithPrimaryColour("#2d9fff")
        .WithSecondaryColour("#FFFFFF")
        .WithFontColour("#FFFFFF")
        .WithLocale("en-GB")
        .WithPresetIssuingCountry("GBR")
        .WithSuccessUrl(Path.Combine("/success"))
        .WithErrorUrl(Path.Combine("/error"))
        .Build()
        )
        .Build();

CreateSessionResult createSessionResult = docScanClient.CreateSession(sessionSpec);
...
{% /tab %}
{% tab language="go" %}
// COMING SOON
{% /tab %}
{% tab language="ruby" %}
require 'Yoti'

Yoti.configure do | config |
    config.client_sdk_id = "YOTI_CLIENT_SDK_ID"
    config.key_file_path = "/path/to/pem"
end

session_spec = Yoti::DocScan::Session::Create::SessionSpecification
  .builder
  .with_client_session_token_ttl(600)
  .with_resources_ttl(90_000)
  .with_user_tracking_id('some-user-tracking-id')
  .with_requested_check(
    Yoti::DocScan::Session::Create::RequestedDocumentAuthenticityCheck
    .builder
    .build
  )
  .with_requested_check(
    Yoti::DocScan::Session::Create::RequestedLivenessCheck
    .builder
    .for_zoom_liveness
    .build
  )
  .with_requested_check(
    Yoti::DocScan::Session::Create::RequestedFaceMatchCheck
    .builder
    .with_manual_check_never
    .build
  )
  .with_requested_task(
    Yoti::DocScan::Session::Create::RequestedTextExtractionTask
    .builder
    .with_manual_check_never
    .with_chip_data_desired
    .build
  )
  .with_sdk_config(
    Yoti::DocScan::Session::Create::SdkConfig
    .builder
    .with_allows_camera_and_upload
    .with_primary_colour('#2d9fff')
    .with_secondary_colour('#FFFFFF')
    .with_font_colour('#FFFFFF')
    .with_locale('en-GB')
    .with_preset_issuing_country('GBR')
    .with_success_url("/your/success/url")
    .with_error_url("/your/error/url")
    .build
  )
  .build

create_session = Yoti::DocScan::Client.create_session(session_spec)
{% /tab %}
{% /code %}

{% html %}
<div class="alert-SAND">
    <div class="alert-title" id="SAND">
      Sandbox
    </div>
    <div class="alert-text">
       If you have understood the quick start you can jump straight to testing on our sandbox.
    </div>
    <div class="alert-links"> 
        <a href="https://developers.yoti.com/yoti/sandbox-docscan">Sandbox</a>
    </div>
</div>
{% /html %}

---

## Installing our SDK

Please use our Yoti SDKs to automatically build the relevant session for you. First you will need the following [information about your application](https://developers.yoti.com/yoti/generate-api-keys) from [Yoti Hub](https://hub.yoti.com/login):

**SDK ID**

This is generated by Yoti when you publish your Yoti application in [Yoti Hub.](https://hub.yoti.com/login) You can find it labelled as Yoti Client SDK ID under the Keys tab within your application. The SDK ID is necessary to initialise the Yoti SDK and it is passed in each call to our system.

**Your application key pair**

This is the private key (in .pem format) associated with the Yoti application you created in [Yoti Hub](https://hub.yoti.com/login). The purpose for this PEM file is to sign requests to our system.

The Yoti SDKs are available via popular dependency management systems. Further details can be found on the pages of the [specific projects](https://developers.yoti.com/yoti/getting-started-docscan#web-examples).

{% code %}
{% tab language="javascript" %}
npm install -S -E yoti
{% /tab %}
{% tab language="java" %}
// If you are using Maven, add the following dependency:
<dependency>
    <groupId>com.yoti</groupId>
    <artifactId>yoti-sdk-impl</artifactId>
    <version>2.9.0</version>
</dependency>

// If you are using Gradle, add the following dependency:
compile group: 'com.yoti', name: 'yoti-sdk-impl', version: '2.9.0'
{% /tab %}
{% tab language="php" %}
// Get the Yoti PHP SDK library via a Composer package
composer require yoti/yoti-php-sdk
{% /tab %}
{% tab language="python" %}
pip install yoti
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
// You can simply add a `require github.com/getyoti/yoti-go-sdk/v2` to go.mod.
// To download and install the Yoti SDK and its dependencies, run the following command from your terminal:

go get "github.com/getyoti/yoti-go-sdk/v3"
{% /tab %}
{% tab language="ruby" %}
gem install yoti

# The gem provides a configuration generator for Ruby on Rails:

rails generate yoti:install
{% /tab %}
{% /code %}

Once you have added the Yoti SDK dependency to your project, you can use it to build and send your session as shown in the code snippet below:

{% code %}
{% tab language="javascript" %}
const path = require('path');
const fs = require("fs");

const {
    DocScanClient,
    SessionSpecificationBuilder,
    RequestedDocumentAuthenticityCheckBuilder,
    RequestedLivenessCheckBuilder,
    RequestedTextExtractionTaskBuilder,
    RequestedFaceMatchCheckBuilder,
    SdkConfigBuilder,
    NotificationConfigBuilder,
} = require('yoti');

const CLIENT_SDK_ID = 'YOTI_CLIENT_SDK_ID'
const PEM_PATH = 'YOTI_KEY_FILE_PATH'
const PEM_KEY = fs.readFileSync(path.join(__dirname, PEM_PATH));

const docScanClient = new DocScanClient(
    CLIENT_SDK_ID,
    PEM_KEY
 );

 docScanClient
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
import com.yoti.api.client.docs.DocScanClientBuilder;
import com.yoti.api.client.docs.DocScanException;
import com.yoti.api.client.docs.session.create.*;
import com.yoti.api.client.docs.session.create.check.RequestedCheckBuilderFactory;
import com.yoti.api.client.docs.session.create.check.RequestedDocumentAuthenticityCheck;
import com.yoti.api.client.docs.session.create.check.RequestedFaceMatchCheck;
import com.yoti.api.client.docs.session.create.check.RequestedLivenessCheck;
import com.yoti.api.client.docs.session.create.task.RequestedTaskBuilderFactory;
import com.yoti.api.client.docs.session.create.task.RequestedTextExtractionTask;

...
DocScanClient docScanClient = DocScanClientBuilder.newInstance()
        .withClientSdkId("YOTI_CLIENT_SDK_ID")
        .withKeyPairSource(ClassPathKeySource.fromClasspath("/path/to/pem"))
        .build();

CreateSessionResult sessionResult = docScanClient.createSession(sessionSpec);
...
{% /tab %}
{% tab language="php" %}
<?php

require_once './vendor/autoload.php';

use Yoti\DocScan\DocScanClient;
use Yoti\DocScan\Session\Create\Check\RequestedDocumentAuthenticityCheckBuilder;
use Yoti\DocScan\Session\Create\Check\RequestedFaceMatchCheckBuilder;
use Yoti\DocScan\Session\Create\Check\RequestedLivenessCheckBuilder;
use Yoti\DocScan\Session\Create\SdkConfigBuilder;
use Yoti\DocScan\Session\Create\SessionSpecificationBuilder;
use Yoti\DocScan\Session\Create\Task\RequestedTextExtractionTaskBuilder;
use Yoti\DocScan\Session\Create\NotificationConfigBuilder;

$YOTI_CLIENT_SDK_ID = 'YOTI_CLIENT_SDK_ID';
$YOTI_PEM = '/path/to/pem';

$docScanClient = new DocScanClient($YOTI_CLIENT_SDK_ID, $YOTI_PEM);

$session = $docScanClient->createSession($sessionSpec);
{% /tab %}
{% tab language="python" %}
from yoti_python_sdk.doc_scan import (
    DocScanClient,
    RequestedDocumentAuthenticityCheckBuilder,
    RequestedFaceMatchCheckBuilder,
    RequestedLivenessCheckBuilder,
    RequestedTextExtractionTaskBuilder,
    SdkConfigBuilder,
    SessionSpecBuilder,
    NotificationConfigBuilder
)

YOTI_CLIENT_SDK_ID = 'YOTI_CLIENT_SDK_ID'
YOTI_PEM = '/path/to/pem'

doc_scan_client = DocScanClient(YOTI_CLIENT_SDK_ID, YOTI_PEM)

session = doc_scan_client.create_session(session_spec)
{% /tab %}
{% tab language="csharp" %}
using System.IO;
using System.Net.Http;
using Yoti.Auth;
using Yoti.Auth.DocScan;
using Yoti.Auth.DocScan.Session.Create;
using Yoti.Auth.DocScan.Session.Create.Check;
using Yoti.Auth.DocScan.Session.Create.Task;

...
const string YOTI_CLIENT_SDK_ID = "YOTI_CLIENT_SDK_ID";
const string PEM_PATH = "/path/to/pem";

StreamReader privateKeyStream = System.IO.File.OpenText(PEM_PATH);
var key = CryptoEngine.LoadRsaKey(privateKeyStream);

var docScanClient = new DocScanClient(YOTI_CLIENT_SDK_ID, key, new HttpClient());

CreateSessionResult createSessionResult = docScanClient.CreateSession(sessionSpec);
...
{% /tab %}
{% tab language="go" %}
// COMING SDOON
{% /tab %}
{% tab language="ruby" %}
// COMING SOON
{% /tab %}
{% /code %}

 See  below for explanations and examples of how to construct the full session piece by piece.

{% html %}
<div class="alert-SAND">
    <div class="alert-title" id="SAND">
      Sandbox
    </div>
    <div class="alert-text">
       Yoti Doc Scan has a sandbox environment, please see installing the sandbox SDK section. 
    </div>
    <div class="alert-links"> 
        <a href="https://developers.yoti.com/yoti/sandbox-docscan#generating-a-sandbox-session">Generating a Sandbox session</a>
    </div>
</div>
{% /html %}

---

## Creating the session

When creating a session you will need to configure the following functions within your session:

{% image url="https://image-archive.developerhub.io/image/upload/29767/r9f5pdidbrwwqt8sty2z/1592238006.png" mode="responsive" height="1126" width="1865" %}
{% /image %}

{% table %}
| Name | Acts on | Type | Manual/Auto | Comment | 
| ---- | ---- | ---- | ---- | ---- | 
| [Document authenticity](https://developers.yoti.com/yoti/generating-a-session#document-authenticity) | 1x Document Resource | Asynchronous check | Manual | To determine the validity of the ID document.\n\nMust wait for the TextDataCheck, if there is one. | 
| [Liveness](https://developers.yoti.com/yoti/generating-a-session#liveness) | 1x Liveness Resource | Synchronous check | Auto | A check to assess whether the document scan is being performed by a real person and not someone wearing a mask or an automated system.\n\nRuns as soon as the FaceMap is uploaded.  Can be repeated until it succeeds, but only one successful _Check_ is allowed in each _Session._ | 
| [Face match](https://developers.yoti.com/yoti/generating-a-session#face-match) | 1x Doc Resource & 1x Liveness Resource | Asynchronous check | Auto & / or Manual | A request to assess whether the user's face matches the face on the ID document. The user's facial image is obtained from the liveness check, which must be performed first.\n\nMust wait for the TextDataCheck, if there is one. | 
| [Text Extraction](https://developers.yoti.com/yoti/generating-a-session#text-extraction) | 1 x Document Resource | Asynchronous task | Auto &/or Manual | Used to recover a failed TextExtractionTask | 
| [Client preferences](https://developers.yoti.com/yoti/generating-a-session#preferences) | N/A | N/A | N/A | Camera and preset country options and where the user should be directed after the user journey (success/error redirect URL). | 
| [System preferences](https://developers.yoti.com/yoti/generating-a-session#preferences) | N/A | N/A | N/A | Doc Scan session length (seconds) and user tracking. | 
| [Notifications](https://developers.yoti.com/yoti/generating-a-session#notifications) | N/A | N/A | N/A | An update notification when the session state changes, based on the selected subscription topics. | 
{% /table %}

---

### Document Authenticity

A request to assess the characteristics of a document, to determine the validity of the ID document.

{% code %}
{% tab language="javascript" %}
const documentAuthenticityCheck = new RequestedDocumentAuthenticityCheckBuilder()
   .build();
{% /tab %}
{% tab language="java" %}
RequestedDocumentAuthenticityCheck documentAuthenticityCheck = RequestedCheckBuilderFactory.newInstance().forDocumentAuthenticityCheck().build();
{% /tab %}
{% tab language="php" %}
<?php

$documentAuthenticityCheck = (new RequestedDocumentAuthenticityCheckBuilder())->build();
{% /tab %}
{% tab language="python" %}
documentAuthenticityCheck = RequestedDocumentAuthenticityCheckBuilder().build()
{% /tab %}
{% tab language="csharp" %}
var documentAuthenticityCheck = new RequestedDocumentAuthenticityCheckBuilder().Build();
{% /tab %}
{% /code %}

This requires there to be image media attached to the resource (images of the front and back of the document – the back of the document is not always required).

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
       Jump to.. 
    </div>
    <div class="alert-text">
       On successful completion, the check outputs a report  which can be found in the ‘retrieve results’ section.
      Details of the report can be found in 'Understanding the report' section.
      
     
    </div>
    <div class="alert-links"> 
        <a href="https://developers.yoti.com/yoti/results#retrieve-id-document-information">Retrieve results</a>
        <a target="_self" href="https://developers.yoti.com/yoti/understanding-the-report#document-authenticity-report">Understanding the report</a> 
   </div>
</div>
{% /html %}

---

### Liveness

A requested check to assess whether the document scan is being performed by a real person and not someone wearing a mask or an automated system.

You must provide the max number of retries your users can have before the liveness is failed. This must be minimum 1. Yoti recommends 3 as a max retry number. 

{% code %}
{% tab language="javascript" %}
const livenessCheck = new RequestedLivenessCheckBuilder()
    .forZoomLiveness()
    .withMaxRetries(3)
    .build();
{% /tab %}
{% tab language="java" %}
RequestedLivenessCheck livenessCheck = RequestedCheckBuilderFactory.newInstance().forLivenessCheck()
                .forZoomLiveness().withMaxRetries(3).build();
{% /tab %}
{% tab language="php" %}
<?php

$livenessCheck = (new RequestedLivenessCheckBuilder())->forZoomLiveness()->build();
{% /tab %}
{% tab language="python" %}
livenessCheck = RequestedLivenessCheckBuilder().for_zoom_liveness().with_max_retries(1).build()
{% /tab %}
{% tab language="csharp" %}
var livenessCheck = new RequestedLivenessCheckBuilder()
                .ForZoomLiveness()
                .WithMaxRetries(3)
                .Build();
{% /tab %}
{% /code %}

An "attempt" is a completed liveness check that is either rejected or approved. If the user does not complete the liveness check this does not count as an attempt and the user will be prompted to try again.

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
       Jump to.. 
    </div>
    <div class="alert-text">
       On successful completion, the check outputs a report  which can be found in the ‘retrieve results’ section.
      Details of the report can be found in 'Understanding the report' section.
      
     
    </div>
    <div class="alert-links"> 
        <a href="https://developers.yoti.com/yoti/results#results-of-checks">Retrieve results</a>
        <a target="_self" href="https://developers.yoti.com/yoti/understanding-the-report#liveness-report">Understanding the report</a> 
   </div>
</div>
{% /html %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
       Note
    </div>
    <div class="alert-text">
If you require biometric consent for liveness please see how to configure this in session creation preferences.      
    </div>
    <div class="alert-links"> 
        <a href="https://developers.yoti.com/yoti/generating-a-session#preferences">Preferences</a>
   </div>
</div>
{% /html %}

---

### Face Match

A request to assess whether the user's face matches the face on the ID document. The user's facial image is obtained from the liveness check, which must be performed first.

{% code %}
{% tab language="javascript" %}
const faceMatchCheck = new RequestedFaceMatchCheckBuilder()
    .withManualCheckFallback()
    .build();
{% /tab %}
{% tab language="java" %}
RequestedFaceMatchCheck faceMatchCheck = RequestedCheckBuilderFactory.newInstance().forFaceMatchCheck()
        .withManualCheckFallback().build();
{% /tab %}
{% tab language="php" %}
<?php

$faceMatchCheck = (new RequestedFaceMatchCheckBuilder())->withManualCheckFallback()->build();
{% /tab %}
{% tab language="python" %}
faceMatchCheck = RequestedFaceMatchCheckBuilder().with_manual_check_fallback().build()
{% /tab %}
{% tab language="csharp" %}
var faceMatchCheck = new RequestedFaceMatchCheckBuilder()
                .WithManualCheckFallback()
                .Build();
{% /tab %}
{% /code %}

This is performed as an automated check, however you can configure whether the check is passed on to our Security Centre for a manual check by qualified Yoti staff. This can be set to always, fallback or never.

{% table %}
| Manual Check | Explanation | 
| ---- | ---- | 
| withManualCheckAlways | The requested check will always go to the Security Centre regardless of the success of the automated check. | 
| withManualCheckNever | The requested check will never go to the Security Centre. | 
| withManualCheckFallback | The requested check will only go to the Security Centre if the machine check fails. | 
{% /table %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
       Jump to.. 
    </div>
    <div class="alert-text">
       On successful completion, the check outputs a report  which can be found in the ‘retrieve results’ section.
      Details of the report can be found in 'Understanding the report' section.
      
     
    </div>
    <div class="alert-links"> 
        <a href="https://developers.yoti.com/yoti/results#results-of-checks">Retrieve results</a>
        <a target="_self" href="https://developers.yoti.com/yoti/understanding-the-report#face-match-report">Understanding the report</a> 
   </div>
</div>
{% /html %}

---

### Text Extraction

A request to obtain the data printed visually on a document, in structured form.

If machine data extraction is not successful, there is an option (selected at session creation) to fall back to manual data extraction. This generates a ‘text data check’ automatically, and the document is reviewed by one of our document processing experts.

{% code %}
{% tab language="javascript" %}
const textExtractionTask = new RequestedTextExtractionTaskBuilder()
    .withManualCheckFallback()
    .build();
{% /tab %}
{% tab language="java" %}
RequestedTextExtractionTask textExtractionTask = RequestedTaskBuilderFactory.newInstance().forTextExtractionTask()
        .withManualCheckFallback()
        .build();
{% /tab %}
{% tab language="php" %}
<?php

$textExtractionTask = (new RequestedTextExtractionTaskBuilder())->withManualCheckAlways()->build();
{% /tab %}
{% tab language="python" %}
textExtractionTask = RequestedTextExtractionTaskBuilder().with_manual_check_always().build()
{% /tab %}
{% tab language="csharp" %}
var textExtractionTask = new RequestedTextExtractionTaskBuilder()
                .WithManualCheckFallback()
                .Build();
{% /tab %}
{% /code %}

{% table %}
| Manual Data Extraction | Explanation | 
| ---- | ---- | 
| withManualCheckFallback | This will initiate manual data extraction only if the automatic extraction fails. We strongly recommend this option. | 
| withManualCheckNever | If the ID fails on automatic extraction, Yoti will not attempt manual extraction and will return a failure in the report. | 
| withManualCheckAlways | The document is always referred for manual review at Yoti's Security Centre, regardless of whether machine data extraction has succeeded or failed. | 
{% /table %}

**US Clients**

If you expect US driving licences, state IDs, Canadian driving licences, or any document with a non-human-readable element on the rear of the document, we recommend that you set your manual_check configuration to 'ALWAYS' or ' FALLBACK" for security reasons.

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
       Jump to.. 
    </div>
    <div class="alert-text">
       On successful completion, the check outputs a report  which can be found in the ‘retrieve results’ section.
      Details of the report can be found in 'Understanding the report' section.
      
     
    </div>
    <div class="alert-links"> 
        <a href="https://developers.yoti.com/yoti/results#results-of-checks">Retrieve results</a>
        <a target="_self" href="https://developers.yoti.com/yoti/understanding-the-report#text-extraction-report">Understanding the report</a> 
   </div>
</div>
{% /html %}

---

### Preferences

**Client Preferences**

The method sdkConfig builder is explained below. If parameters are not defined the default below will be set:

{% code %}
{% tab language="javascript" %}
.withSdkConfig(
        new SdkConfigBuilder()
          .withAllowsCameraAndUpload()
          .withPrimaryColour('#2d9fff')
          .withSecondaryColour('#FFFFFF')
          .withFontColour('#FFFFFF')
          .withLocale('en-GB')
          .withPresetIssuingCountry('GBR')
          .withSuccessUrl(`${process.env.YOTI_APP_BASE_URL}/index`)
          .withErrorUrl(`${process.env.YOTI_APP_BASE_URL}/profile`)
          .build()
      )
{% /tab %}
{% tab language="java" %}
SdkConfig sdkConfig = SdkConfigBuilderFactory.newInstance().create()
                .withAllowsCameraAndUpload()
                .withPrimaryColour("#2d9fff")
                .withSecondaryColour("#FFFFFF")
                .withFontColour("#FFFFFF")
                .withLocale("en-GB")
                .withPresetIssuingCountry("GBR")
                .withSuccessUrl("https://localhost:8443/success")
                .withErrorUrl("https://localhost:8443/error")
                .build();
{% /tab %}
{% tab language="php" %}
<?php

$sdkConfig =
    (new SdkConfigBuilder())
    ->withAllowsCameraAndUpload()
    ->withPrimaryColour('#2d9fff')
    ->withSecondaryColour('#FFFFFF')
    ->withFontColour('#FFFFFF')
    ->withLocale('en-GB')
    ->withPresetIssuingCountry('GBR')
    ->withSuccessUrl('/your/success/url')
    ->withErrorUrl('/your/error/url')
    ->build();
{% /tab %}
{% tab language="python" %}
sdk_config = (
    SdkConfigBuilder()
    .with_allows_camera_and_upload()
    .with_primary_colour("#2d9fff")
    .with_secondary_colour("#FFFFFF")
    .with_font_colour("#FFFFFF")
    .with_locale("en-GB")
    .with_preset_issuing_country("GBR")
    .with_success_url("/your/success/url")
    .with_error_url("/your/error/url")
    .build()
)
{% /tab %}
{% tab language="csharp" %}
var sdkConfig = new SdkConfigBuilder()
                .WithAllowsCameraAndUpload()
                .WithPrimaryColour("#2d9fff")
                .WithSecondaryColour("#FFFFFF")
                .WithFontColour("#FFFFFF")
                .WithLocale("en-GB")
                .WithPresetIssuingCountry("GBR")
                .WithSuccessUrl("/your/success/url")
                .WithErrorUrl("/your/error/url")
                .Build();
{% /tab %}
{% /code %}

{% table %}
| Type | Parameters (examples) | Description | Required | 
| ---- | ---- | ---- | ---- | 
| Allowed capture methods | withAllowsCameraAndUpload\n\nwithAllowsCamera | Whether the  user must only use the camera on their device to take a photo of their ID document, or whether they can also upload an existing image of the document from a file. | optional | 
| withPrimaryColour | #2d9fff(default), #ff0000 | Colours of the button provided in the frontend client as a hexadecimal RGB value. | optional | 
| withLocale | en-GB(default) | Force language locale for the frontend client. Full list shown below. | optional | 
| withPresetIssuingCountry | USA, GBR | The user must select the issuing country of the document they are uploading. This setting determines which \n\nissuing country is selected by default.\n\n\n\nNOTE: Must be a 3 letter ISO 3166 code. | optional | 
| withSuccessUrl | [https://yourdomain.com/success](https://yourdomain.com/success) | If the upload/photo is successfully captured redirect your users here. Yoti will then begin to carry out the requested checks and tasks. If undefined, the page will not redirect and you can listen to Yoti's post messages on the same page. | optional | 
| withErrorUrl | [https://yourdomain.com/error](https://yourdomain.com/error) | If the upload/photo is unsuccessfully captured redirect your users here. If undefined, the user view will display an error screen, with the error code as a query parameter and won't redirect. (Details on the error codes can be found [here](/yoti/render-the-user-view#error-codes).) | optional | 
{% /table %}

**Translated languages support - withLocale**

Yoti offers the ability to force a language locale for the front end client - see list here:

{% table %}
| Language | Parameter | 
| ---- | ---- | 
| English | en-GB (default) | 
| French  (Français) | fr | 
| Spanish (Español) | es | 
| Thai (ภาษาไทย) | th | 
| Russian (русский) | ru | 
| Brazilian Portuguese (português brasileiro) | pt | 
| Turkish (Türkçe) | tr | 
| Vietnamese (Tiếng Việt) | vi | 
| Czech (čeština) | cs | 
| German (Deutsch) | de | 
| Canadian | en-CA | 
{% /table %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
       Jump to.. 
    </div>
    <div class="alert-text">
If a success URL or error URL is supplied as part of the session creation, check out Yoti's recommendation on using POST messaging to be notified on the if an error occurs in the flow or completion.    
     
    </div>
    <div class="alert-links"> 
        <a href="https://developers.yoti.com/yoti/render-the-user-view#event-notifications">Event Notifications</a>
   </div>
</div>
{% /html %}

**System**

{% code %}
{% tab language="javascript" %}
const sessionSpec = new SessionSpecificationBuilder()
    .withClientSessionTokenTtl(600)
    .withResourcesTtl(90000)
    .withUserTrackingId('some-user-tracking-id')
    .withRequestedCheck(documentAuthenticityCheck)
    .withRequestedCheck(livenessCheck)
    .withRequestedCheck(faceMatchCheck)
    .withRequestedTask(textExtractionTask)
    .withSdkConfig(sdkConfig)
    .withNotifications(notificationConfig)
		.withBlockBiometricConsent(false)
    .build();
{% /tab %}
{% tab language="java" %}
SessionSpec sessionSpec = SessionSpecBuilderFactory.newInstance().create()
                .withClientSessionTokenTtl(600)
                .withResourcesTtl(604800)
                .withUserTrackingId("<YOUR_USER_ID>")
                .withNotifications(notificationConfig)
                .withSdkConfig(sdkConfig)
                .withRequestedCheck(documentAuthenticityCheck)
                .withRequestedCheck(livenessCheck)
                .withRequestedCheck(faceMatchCheck)
                .withRequestedTask(textExtractionTask)
  							.withBlockBiometricConsent(false)
                .build();
{% /tab %}
{% tab language="php" %}
<?php

$sessionSpec = (new SessionSpecificationBuilder())
    ->withClientSessionTokenTtl(600)
    ->withResourcesTtl(90000)
    ->withUserTrackingId('some-user-tracking-id')
    ->withRequestedCheck($documentAuthenticityCheck)
    ->withRequestedCheck($livenessCheck)
    ->withRequestedCheck($faceMatchCheck)
    ->withRequestedTask($textExtractionTask)
    ->withSdkConfig($sdkConfig)
    ->withNotifications($notificationConfig)
  	->withBlockBiometricConsent(false)
    ->build();
{% /tab %}
{% tab language="python" %}
session_spec = (
    SessionSpecBuilder()
    .with_client_session_token_ttl(600)
    .with_resources_ttl(90000)
    .with_user_tracking_id("some-user-tracking-id")
    .with_requested_check(documentAuthenticityCheck)
    .with_requested_check(livenessCheck)
    .with_requested_check(faceMatchCheck)
    .with_requested_task(textExtractionTask)
    .with_sdk_config(sdk_config)
    .with_notifications(notification_config)
  	.with_block_biometric_consent(false)
    .build()
)
{% /tab %}
{% tab language="csharp" %}
var sessionSpec = new SessionSpecificationBuilder()
                .WithClientSessionTokenTtl(600)
                .WithResourcesTtl(90000)
                .WithUserTrackingId("some-user-tracking-id")
                .WithRequestedCheck(documentAuthenticityCheck)
                .WithRequestedCheck(livenessCheck)
                .WithRequestedCheck(faceMatchCheck)
                .WithRequestedTask(textExtractionTask)
                .WithNotifications(notificationConfig)
                .WithSdkConfig(sdkConfig)
  							.WithBlockBiometricConsent(false)
                .Build();
{% /tab %}
{% /code %}

The table below explains the optional parameters for the session and data retention configuration.

{% table %}
| Parameters | Description | Required | 
| ---- | ---- | ---- | 
| withClientSessionTokenTtl | This is how long the full Yoti Doc Scan session is open for in seconds. This must be longer than 300s (5 minutes). | optional | 
| withResourcesTtl | Retention period ("time to live") for uploaded documents/images in number of seconds. Default is one week (`60*60*24*7=604800`). This can be a minimum of 24 hours and must be at least 24 hours longer than the client_session_token_ttl. This starts once the `client_session_token_ttl` is completed. | optional | 
| withUserTrackingId | Allows the relying business backend to track the same user across multiple sessions. **Note:** This should not contain any personal identifiable information. | optional | 
| WithBlockBiometricConsent | For several American states (Texas, Illinois and Washington US states) , Yoti will need the user’s consent to collect their biometric details for our liveness feature to be compliant with legislations in the US. We have implemented a toggle on / off box for users to give biometric consent before starting the liveness process. | optional | 
{% /table %}

---

### Notifications

Yoti Doc Scan optionally posts an update notification every time the session state changes, based on the selected subscription topics. 

{% code %}
{% tab language="javascript" %}
const notificationConfig = new NotificationConfigBuilder()
    .withEndpoint('https://yourdomain.example/idverify/updates')
    .withAuthToken('username:password')
    .forResourceUpdate()
    .forTaskCompletion()
    .forCheckCompletion()
    .forSessionCompletion()
    .build();
{% /tab %}
{% tab language="java" %}
NotificationConfig notificationConfig = NotificationConfigBuilderFactory.newInstance().create()
                .withEndpoint("https://yourdomain.example/idverify/updates")
                .withAuthToken("username:password")
                .forResourceUpdate()
                .forTaskCompletion()
                .forCheckCompletion()
                .forSessionCompletion()
                .build();
{% /tab %}
{% tab language="php" %}
<?php

$notificationConfig = (new NotificationConfigBuilder())
    ->withEndpoint('https://yourdomain.example/idverify/updates')
    ->withAuthToken('username:password')
    ->forResourceUpdate()
    ->forTaskCompletion()
    ->forCheckCompletion()
    ->forSessionCompletion()
    ->build();
{% /tab %}
{% tab language="python" %}
notification_config = (
    NotificationConfigBuilder()
    .with_endpoint('https://yourdomain.example/idverify/updates')
    .with_auth_token('username:password')
    .for_resource_update()
    .for_task_completion()
    .for_check_completion()
    .for_session_completion()
    .build()
)
{% /tab %}
{% tab language="csharp" %}
var notificationConfig = new NotificationConfigBuilder()
                .WithEndpoint("https://yourdomain.example/idverify/updates")
                .WithAuthToken("username:password")
                .ForResourceUpdate()
                .ForTaskCompletion()
                .ForCheckCompletion()
                .ForSessionCompletion()
                .Build();
{% /tab %}
{% /code %}

Below are the different updates Yoti can provide:

{% table %}
| Notification | Description | 
| ---- | ---- | 
| withEndpoint | Endpoint for notifications to be sent to. Only HTTPS endpoints with TLS 1.2 are supported. A POST message will be sent. Exposing this endpoint is not mandatory but highly recommended as it would avoid a continuous polling on the session retrieval endpoint. | 
| withAuthToken | Allows the relying business backend to define an authorisation token, if they have secured API endpoints, allowing Yoti to call endpoints. We recommend protecting any exposed routes with basic authorisation. You may specify a basic auth token to the Yoti Doc Scan API to be used when sending notifications to your endpoint. Credentials are automatically encoded as base64 and sent in the Authorisation header. For example "auth_token": "username:password" would result in Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQ= being sent into the request header from Yoti. | 
| forResourceUpdate | Update received whenever there are changes to **resources** in the Yoti Doc Scan session. For example, a user uploading a new document. | 
| forTaskCompletion | Sent when a task is completed. If you require TEXT_EXTRACTION and the check has been fulfilled, Yoti will send this through as an update to your endpoint. | 
| forSessionCompletion | Triggered when all tasks and all checks inside of a given session have been completed. | 
| forCheckCompletion | Sent when a check completes – for example a document authenticity check being performed. | 
{% /table %}

Optionally, it is possible to specify a Webhook URL when creating a Yoti Doc Scan request to be informed of any changes that occur within the session. This avoids the need to poll for updates. Here is an example object that can be provided to the Doc Scan API which specifies a notifications endpoint, and a list of topics to be subscribed to.

**Example response for notifications**

{% code %}
{% tab language="json" %}
{
    // Always provided
    "session_id" : "<uuid>",
    "topic" : "resource_update", // | "task_completion" | "check_completion" | "session_completion"
    // Optional and present only when "topic" is "task_completion"
    "task_id" : "<uuid>",
    // Optional and present only when "topic" is "resource_update"
    "resource_id" : "<uuid>",
    // Optional and present only when "topic" is "check_completion"
    "check_id" : "<uuid>"
  }
{% /tab %}
{% /code %}

---

## Example response

If the request is successful and a session is generated the API will send a response in the form:

{% code %}
{% tab language="javascript" %}
const sessionId = session.getSessionId();
const clientSessionToken = session.getClientSessionToken();
const clientSessionTokenTtl = session.getClientSessionTokenTtl();
{% /tab %}
{% tab language="java" %}
String sessionId = sessionResult.getSessionId();
String clientSessionToken = sessionResult.getClientSessionToken();
int clientSessionTokenTtl = sessionResult.getClientSessionTokenTtl();
{% /tab %}
{% tab language="php" %}
<?php

$YOTI_SESSION_ID = $session->getSessionId();
$CLIENT_SESSION_TOKEN = $session->getClientSessionToken();
$CLIENT_SESSION_TOKEN_TTL= $session->getClientSessionTokenTtl();
{% /tab %}
{% tab language="python" %}
session_id = session.session_id
client_session_token = session.client_session_token
client_session_token_ttl = session.client_session_token_ttl
{% /tab %}
{% tab language="csharp" %}
var sessionId = createSessionResult.SessionId;
var clientSessionToken = createSessionResult.ClientSessionToken;
var clientSessionTokenTtl = createSessionResult.ClientSessionTokenTtl;
{% /tab %}
{% /code %}

{% table %}
| Response | Description | 
| ---- | ---- | 
| clientSessionTokenTtl | Time in seconds until the client session expires | 
| clientSessionToken | Used to authenticate the session | 
| sessionId | ID of the session | 
{% /table %}

{% html %}
<div class="alert-SAND">
    <div class="alert-title" id="SAND">
      Sandbox
    </div>
    <div class="alert-text">
       Yoti Doc Scan has a sandbox environment, please see responses section. 
    </div>
    <div class="alert-links"> 
        <a href="https://developers.yoti.com/yoti/sandbox-docscan#configure-the-responses">Sandbox responses</a>
    </div>
</div>
{% /html %}

---

## Extras

### Supported Documents

To see all documents that are supported for Yoti Doc Scan please see the code snippet below.  

{% code %}
{% tab language="javascript" %}
const path = require('path');
const fs = require('fs');

const { DocScanClient } = require('yoti');

const YOTI_CLIENT_SDK_ID = 'YOUR_SDK_ID';
const YOTI_PEM = fs.readFileSync(path.join(__dirname, '/path/to/pem'));
const docScanClient = new DocScanClient(YOTI_CLIENT_SDK_ID, YOTI_PEM);

docScanClient.getSupportedDocuments().then((supportedDocuments) => {
    supportedCountries = supportedDocuments.getSupportedCountries();
    supportedCountries.map((country) => {
        countryCode = country.getCode();
        documents = country.getSupportedDocuments();
    });
});
{% /tab %}
{% tab language="java" %}
import com.yoti.api.client.docs.DocScanClient;
import com.yoti.api.client.docs.DocScanClientBuilder;
import com.yoti.api.client.docs.support.SupportedCountry;
import com.yoti.api.client.docs.support.SupportedDocument;
import com.yoti.api.client.docs.support.SupportedDocumentsResponse;

DocScanClient docScanClient = DocScanClientBuilder.newInstance()
        .withClientSdkId("YOUR_CLIENT_SDK_ID")
        .withKeyPairSource(ClassPathKeySource.fromClasspath("/path/to/pem"))
        .build();

SupportedDocumentsResponse supportedDocuments = docScanClient.getSupportedDocuments();
List<? extends SupportedCountry> supportedCountries = supportedDocuments.getSupportedCountries();

for (SupportedCountry country : supportedCountries) {

   String countryCode = country.getCode();
   List<? extends SupportedDocument> documents = country.getSupportedDocuments();

}
{% /tab %}
{% tab language="php" %}
<?php

require_once './vendor/autoload.php';

use Yoti\DocScan\DocScanClient;

$YOTI_CLIENT_SDK_ID = 'YOUR_SDK_ID';
$YOTI_PEM = '/path/to/pem';

$client = new DocScanClient($YOTI_CLIENT_SDK_ID, $YOTI_PEM);

$supportedDocuments = $client->getSupportedDocuments();
$supportedCountries = $supportedDocuments->getSupportedCountries();

foreach($supportedCountries as $country) {
  
    $countryCode = $country->getCode();
    $documents = $country->getSupportedDocuments();
  
}
{% /tab %}
{% tab language="python" %}
from yoti_python_sdk.doc_scan import (
    DocScanClient
)

YOTI_CLIENT_SDK_ID = 'YOUR_SDK_ID'
YOTI_PEM = '/path/to/pem'

doc_scan_client = DocScanClient(YOTI_CLIENT_SDK_ID, YOTI_PEM)

supported_documents = doc_scan_client.get_supported_documents()
supported_countries = supported_documents.supported_countries

for country in supported_countries:
    country_code = country.code
    documents = country.supported_documents
{% /tab %}
{% tab language="csharp" %}
// COMING SOON
{% /tab %}
{% /code %}

Yoti will return a list of countries listed by ISO 3166 country code. Each country will list an array of supported documents from that country. 

---

### Filtering documents and countries

If you do not wish to accept all documents or countries you can configure your Doc Scan session to add / remove which countries and document types are displayed to the user on the user view.

We provide 2 ways to customise countries or documents displayed:

1) **ORTHOGONAL_RESTRICTION**

Allow (whitelist) or remove (blacklist) by _country_ and _document type_ independently.

If you create a WHITELIST for one country / document and also a BLACKLIST for the other, then the BLACKLIST will overrule the WHITELIST.

{% code %}
{% tab language="javascript" %}
const {
    SessionSpecificationBuilder,
    RequiredIdDocumentBuilder,
    OrthogonalRestrictionsFilterBuilder
} = require('yoti');

const filter = new OrthogonalRestrictionsFilterBuilder()
    // Allow from specific countries
    .withWhitelistedCountries(['GBR', 'JPN'])

    // Deny from specific countries
    .withBlacklistedCountries(['FRA'])

    // Allow specific documents
    .withWhitelistedDocumentTypes(['PASSPORT'])

    // Deny certain documents
    .withBlacklistedDocumentTypes(['DRIVING_LICENCE'])
    .build();

const requiredDocument = new RequiredIdDocumentBuilder()
    .withFilter(filter)
    .build();

const sessionSpec = new SessionSpecificationBuilder()
    // New method in addition to existing create session methods
    .withRequiredDocument(requiredDocument)
    .build();
{% /tab %}
{% tab language="java" %}
import com.yoti.api.client.docs.session.create.*;
import com.yoti.api.client.docs.session.create.filters.*;

import java.util.Arrays;
import java.util.Collections;

DocumentFilterBuilderFactory ORTHOGONAL_FILTER_FACTORY = DocumentFilterBuilderFactory.newInstance();

OrthogonalRestrictionsFilter filter = ORTHOGONAL_FILTER_FACTORY.forOrthogonalRestrictionsFilter()
        // Allow from specific countries
        .withWhitelistedCountries(Arrays.asList("GBR", "JPN"))

        // Deny from specific countries
        .withBlacklistedCountries(Collections.singletonList("FRA"))

        // Allow specific documents
        .withWhitelistedDocumentTypes(Collections.singletonList("PASSPORT"))

        // Deny certain documents
        .withBlacklistedDocumentTypes(Collections.singletonList("DRIVING_LICENCE"))
        .build();

RequiredDocument requiredDocument = RequiredDocumentBuilderFactory.newInstance()
        .forIdDocument()
        .withFilter(filter)
        .build();

SessionSpec sessionSpec = SessionSpecBuilderFactory.newInstance().create()
        // New method in addition to existing create session methods
        .withRequiredDocument(requiredDocument)
        .build();
{% /tab %}
{% tab language="php" %}
<? php
  
use Yoti\DocScan\Session\Create\SessionSpecificationBuilder;
use Yoti\DocScan\Session\Create\Filters\Orthogonal\OrthogonalRestrictionsFilterBuilder;
use Yoti\DocScan\Session\Create\Filters\RequiredIdDocumentBuilder;

$filter = (new OrthogonalRestrictionsFilterBuilder())
    // Allow from specific countries
    ->withWhitelistedCountries(['GBR', 'JPN'])

    // Deny from specific countries
    ->withBlacklistedCountries(['FRA'])

    // Allow specific documents
    ->withWhitelistedDocumentTypes(['PASSPORT'])

    // Deny certain documents
    ->withBlacklistedDocumentTypes(['DRIVING_LICENCE'])
    ->build();

$requiredDocument = (new RequiredIdDocumentBuilder())
    ->withFilter($filter)
    ->build();

$sessionSpec = (new SessionSpecificationBuilder())
    // New method in addition to existing create session methods
    ->withRequiredDocument($requiredDocument)
    ->build();
{% /tab %}
{% tab language="python" %}
from yoti_python_sdk.doc_scan import (
    SessionSpecBuilder
)

from yoti_python_sdk.doc_scan.session.create.filter import (
    OrthogonalRestrictionsFilterBuilder,
    RequiredIdDocumentBuilder
)

filter = (
    OrthogonalRestrictionsFilterBuilder()
    # Allow from specific countries
    .with_whitelisted_country_codes(['GBR', 'JPN'])

    # Deny from specific countries
    .with_blacklisted_country_codes(['FRA'])

    # Allow specific documents
    .with_whitelisted_document_types(['PASSPORT'])

    # Deny certain documents
    .with_blacklisted_document_types(['DRIVING_LICENCE'])
    .build()
)

required_document = RequiredIdDocumentBuilder().with_filter(filter).build()

session_spec = (
    SessionSpecBuilder()
    # New method in addition to existing create session methods
    .with_required_document(required_document)
    .build()
)
{% /tab %}
{% tab language="csharp" %}
//COMING SOON
{% /tab %}
{% /code %}

**2) DOCUMENT_RESTRICTION**

This filter allows greater precision but is more verbose to use. It provides multiple restrictions that filter by _country_ and _document type_ together. 

{% code %}
{% tab language="javascript" %}
const {
    SessionSpecificationBuilder,
    DocumentRestrictionsFilterBuilder,
    DocumentRestrictionBuilder,
    RequiredIdDocumentBuilder
} = require('yoti');

const documentRestriction = new DocumentRestrictionBuilder()
    // Set countries
    .withCountries(['GBR'])

    // Set document types
    .withDocumentTypes(['PASSPORT'])
    .build();

const filter = new DocumentRestrictionsFilterBuilder()
    // Set document restriction
    .withDocumentRestriction(documentRestriction)

    // Specify if this filter is an allowed list, or denied list
    .forWhitelist() // or forBlacklist() if disallowing this filter
    .build();

const requiredDocument = new RequiredIdDocumentBuilder()
    .withFilter(filter)
    .build();

const sessionSpec = new SessionSpecificationBuilder()
    // New method in addition to existing create session methods
    .withRequiredDocument(requiredDocument)
    .build();
{% /tab %}
{% tab language="java" %}
import com.yoti.api.client.docs.session.create.*;
import com.yoti.api.client.docs.session.create.filters.*;

import java.util.Collections;

DocumentRestriction documentRestriction = DocumentRestrictionBuilderFactory.newInstance().forDocumentRestriction()
        // Set countries
        .withCountries(Collections.singletonList("GBR"))

        // Set document types
        .withDocumentTypes(Collections.singletonList("PASSPORT"))
        .build();

DocumentRestrictionsFilter filter = DocumentFilterBuilderFactory.newInstance().forDocumentRestrictionsFilter()
        // Set document restriction
        .withDocumentRestriction(documentRestriction)

        // Specify if this filter is an allowed list, or denied list
        .forWhitelist() // or forBlacklist() if disallowing this filter
        .build();

RequiredDocument requiredDocument = RequiredDocumentBuilderFactory.newInstance()
        .forIdDocument()
        .withFilter(filter)
        .build();

SessionSpec sessionSpec = SessionSpecBuilderFactory.newInstance().create()
        // New method in addition to existing create session methods
        .withRequiredDocument(requiredDocument)
        .build();
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\DocScan\Session\Create\SessionSpecificationBuilder;
use Yoti\DocScan\Session\Create\Filters\Document\DocumentRestrictionBuilder;
use Yoti\DocScan\Session\Create\Filters\Document\DocumentRestrictionsFilterBuilder;
use Yoti\DocScan\Session\Create\Filters\RequiredIdDocumentBuilder;

$documentRestriction = (new DocumentRestrictionBuilder())
    // Set countries
    ->withCountries(['GBR'])

    // Set document types
    ->withDocumentTypes(['PASSPORT'])
    ->build();

$filter = (new DocumentRestrictionsFilterBuilder())
    // Set document restriction
    ->withDocumentRestriction($documentRestriction)

    // Specify if this filter is an allowed list, or denied list
    ->forWhitelist() // or forBlacklist() if disallowing this filter
    ->build();

$requiredDocument = (new RequiredIdDocumentBuilder())
    ->withFilter($filter)
    ->build();

$sessionSpec = (new SessionSpecificationBuilder())
    // New method in addition to existing create session methods
    ->withRequiredDocument($requiredDocument)
    ->build();
{% /tab %}
{% tab language="python" %}
from yoti_python_sdk.doc_scan import (
    SessionSpecBuilder
)

from yoti_python_sdk.doc_scan.session.create.filter import (
    DocumentRestrictionBuilder,
    DocumentRestrictionsFilterBuilder,
    RequiredIdDocumentBuilder
)

document_restriction = (
    DocumentRestrictionBuilder()
    # Set countries
    .with_country_codes(['GBR'])

    # Set document types
    .with_document_types(['PASSPORT'])
    .build()
)

filter = (
    DocumentRestrictionsFilterBuilder()
    # Set document restriction
    .with_document_restriction(document_restriction)

    # Specify if this filter is an allowed list, or denied list
    .for_whitelist() # or for_blacklist() if disallowing this filter
    .build()
)

required_document = RequiredIdDocumentBuilder().with_filter(filter).build()

session_spec = (
    SessionSpecBuilder()
    # New method in additional to existing create session methods
    .with_required_document(required_document)
    .build()
)
{% /tab %}
{% tab language="csharp" %}
//COMING SOON
{% /tab %}
{% /code %}

---

### Request multiple documents

It is possible to ask for more than one document from the user in one session using an array.

{% html %}
<div class="alert-GTK">

    <div class="alert-title" id="GTK">

        Good to know

    </div>

    <div class="alert-text">

        If you are requesting multiple documents from your users you must make sure that you avoid creating sessions where the same document would be used to satisfy multiple selections.

    </div>

    <div class="alert-links"> 

   </div>

</div>
{% /html %}

{% code %}
{% tab language="javascript" %}
const {
    SessionSpecificationBuilder,
    DocumentRestrictionsFilterBuilder,
    DocumentRestrictionBuilder,
    RequiredIdDocumentBuilder
} = require('yoti');

const documentRestriction = new DocumentRestrictionBuilder()
    .withCountries(['GBR'])
    .withDocumentTypes(['PASSPORT'])
    .build();

const filter = new DocumentRestrictionsFilterBuilder()
    .withDocumentRestriction(documentRestriction)
    .forWhitelist()
    .build();

const requiredDocument = new RequiredIdDocumentBuilder()
    .withFilter(filter)
    .build();

const anotherDocumentRestriction = new DocumentRestrictionBuilder()
    .withCountries(['GBR'])
    .withDocumentTypes(['DRIVING_LICENCE'])
    .build();

const anotherFilter = new DocumentRestrictionsFilterBuilder()
    .withDocumentRestriction(anotherDocumentRestriction)
    .forWhitelist()
    .build();

const anotherRequiredDocument = new RequiredIdDocumentBuilder()
    .withFilter(anotherFilter)
    .build();

const sessionSpec = new SessionSpecificationBuilder()
    // Additional required document
    .withRequiredDocument(requiredDocument)
    .withRequiredDocument(anotherRequiredDocument)
    .build();
{% /tab %}
{% tab language="java" %}
import com.yoti.api.client.docs.session.create.*;
import com.yoti.api.client.docs.session.create.filters.*;

import java.util.Collections;

DocumentRestriction documentRestriction = DocumentRestrictionBuilderFactory.newInstance().forDocumentRestriction()
        // Set countries
        .withCountries(Collections.singletonList("GBR"))

        // Set document types
        .withDocumentTypes(Collections.singletonList("PASSPORT"))
        .build();

DocumentRestrictionsFilter filter = DocumentFilterBuilderFactory.newInstance().forDocumentRestrictionsFilter()
        // Set document restriction
        .withDocumentRestriction(documentRestriction)

        // Specify if this filter is an allowed list, or denied list
        .forWhitelist() // or forBlacklist() if disallowing this filter
        .build();

RequiredDocument requiredDocument = RequiredDocumentBuilderFactory.newInstance()
        .forIdDocument()
        .withFilter(filter)
        .build();

DocumentRestriction anotherDocumentRestriction = DocumentRestrictionBuilderFactory.newInstance().forDocumentRestriction()
        // Set countries
        .withCountries(Collections.singletonList("GBR"))

        // Set document types
        .withDocumentTypes(Collections.singletonList("DRIVING_LICENCE"))
        .build();

DocumentRestrictionsFilter anotherFilter = DocumentFilterBuilderFactory.newInstance().forDocumentRestrictionsFilter()
        // Set document restriction
        .withDocumentRestriction(anotherDocumentRestriction)

        // Specify if this filter is an allowed list, or denied list
        .forWhitelist() // or forBlacklist() if disallowing this filter
        .build();

RequiredDocument anotherRequiredDocument = RequiredDocumentBuilderFactory.newInstance()
        .forIdDocument()
        .withFilter(anotherFilter)
        .build();

SessionSpec sessionSpec = SessionSpecBuilderFactory.newInstance().create()
        // Additional required document
        .withRequiredDocument(requiredDocument)
        .withRequiredDocument(anotherRequiredDocument)
        .build();
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\DocScan\Session\Create\SessionSpecificationBuilder;
use Yoti\DocScan\Session\Create\Filters\Document\DocumentRestrictionBuilder;
use Yoti\DocScan\Session\Create\Filters\Document\DocumentRestrictionsFilterBuilder;
use Yoti\DocScan\Session\Create\Filters\RequiredIdDocumentBuilder;

$documentRestriction = (new DocumentRestrictionBuilder())
    ->withCountries(['GBR'])
    ->withDocumentTypes(['PASSPORT'])
    ->build();

$filter = (new DocumentRestrictionsFilterBuilder())
    ->withDocumentRestriction($documentRestriction)
    ->forWhitelist()
    ->build();

$requiredDocument = (new RequiredIdDocumentBuilder())
    ->withFilter($filter)
    ->build();

$anotherDocumentRestriction = (new DocumentRestrictionBuilder())
    ->withCountries(['GBR'])
    ->withDocumentTypes(['DRIVING_LICENCE'])
    ->build();

$anotherFilter = (new DocumentRestrictionsFilterBuilder())
    ->withDocumentRestriction($anotherDocumentRestriction)
    ->forWhitelist()
    ->build();

$anotherRequiredDocument = (new RequiredIdDocumentBuilder())
    ->withFilter($anotherFilter)
    ->build();

$sessionSpec = (new SessionSpecificationBuilder())
    // Additional required document
    ->withRequiredDocument($requiredDocument)
    ->withRequiredDocument($anotherRequiredDocument)
    ->build();
{% /tab %}
{% tab language="python" %}
from yoti_python_sdk.doc_scan import (
    SessionSpecBuilder
)

from yoti_python_sdk.doc_scan.session.create.filter import (
    DocumentRestrictionBuilder,
    DocumentRestrictionsFilterBuilder,
    RequiredIdDocumentBuilder
)

document_restriction = (
    DocumentRestrictionBuilder()
    .with_country_codes(['GBR'])
    .with_document_types(['PASSPORT'])
    .build()
)

filter = (
    DocumentRestrictionsFilterBuilder()
    .with_document_restriction(document_restriction)
    .for_whitelist()
    .build()
)

required_document = RequiredIdDocumentBuilder().with_filter(filter).build()

another_document_restriction = (
    DocumentRestrictionBuilder()
    .with_country_codes(['GBR'])
    .with_document_types(['DRIVING_LICENCE'])
    .build()
)

another_filter = (
    DocumentRestrictionsFilterBuilder()
    .with_document_restriction(another_document_restriction)
    .for_whitelist()
    .build()
)

another_required_document = RequiredIdDocumentBuilder().with_filter(another_filter).build()

session_spec = (
    SessionSpecBuilder()
    # Additional required document
    .with_required_document(required_document)
    .with_required_document(another_required_document)
    .build()
)
{% /tab %}
{% tab language="csharp" %}
// Click to edit code
{% /tab %}
{% /code %}