---
type: page
title: Quick Start
listed: true
slug: quick-start
description: 
index_title: Quick Start
hidden: 
keywords: 
tags: 
---

We suggest you read through the step by step integration guide to understand the integration in detail. Please see below for example code snippets and examples projects.

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      You will need the Yoti App on your phone and to have registered your business with Yoti. Click here for more info.
   </div>
   <div class="alert-links"> 
         <a target="_self" href="https://developers.yoti.com/yoti/getting-started-hub">View Onboarding with Yoti</a>
      <a target="_self" href="https://developers.yoti.com/yoti/generate-api-keys-hub">View Generate API Keys</a> 
   </div>
</div>
{% /html %}

---

## 💻Web examples

If we don't support your language please [get in touch](https://developers.yoti.com/yoti/get-in-touch) with us.

- [Javascript (node.js)](https://github.com/getyoti/yoti-node-sdk/tree/master/examples/doc-scan)
- [Java](https://github.com/getyoti/yoti-java-sdk/tree/master/examples/doc-scan)
- [PHP](https://github.com/getyoti/yoti-php-sdk/tree/master/examples/doc-scan)
- [Python](https://github.com/getyoti/yoti-python-sdk/tree/master/examples/doc_scan)
- [.NET](https://github.com/getyoti/yoti-dotnet-sdk/tree/master/src/Examples/DocScan/DocScanExample)
- [Go](https://github.com/getyoti/doc-scan-examples/tree/master/go)
- [Ruby](https://github.com/getyoti/yoti-ruby-sdk/tree/master/examples/doc_scan)

---

## 📱Mobile integration examples

The mobile integrations that we currently support are listed below. Please select your preferred language to continue. You will need to also review the web examples above.

- [iOS](https://github.com/getyoti/yoti-doc-scan-ios)
- [Android](https://github.com/getyoti/yoti-doc-scan-android)
- [React Native](https://github.com/getyoti/yoti-doc-scan-react-native)

---

## 🏖Sandbox examples

Just like the normal Yoti Client, the Yoti Sandbox Client SDK is available in the following languages:

- [Javascript (Node.js)](https://github.com/getyoti/yoti-node-sdk-sandbox/tree/master/examples/doc_scan)
- [Ruby](https://github.com/getyoti/yoti-ruby-sdk-sandbox/tree/master/examples)
- [PHP](https://github.com/getyoti/yoti-php-sdk-sandbox/tree/master/examples/doc-scan)
- [Python](https://github.com/getyoti/yoti-python-sdk-sandbox/tree/master/examples)
- [.NET](https://github.com/getyoti/yoti-dotnet-sdk-sandbox/tree/master/Examples/Yoti.Auth.Sandbox.Examples)

{% html %}
<div class="alert-SAND">
    <div class="alert-title" id="SAND">
      Sandbox
    </div>
    <div class="alert-text">
       We offer a sandbox for the SDK integration. If you wish to integrate sandbox please click the link below.
    </div>
    <div class="alert-links"> 
        <a href="https://developers.yoti.com/yoti-doc-scan/sandbox">Sandbox</a> 
    </div>
</div>
{% /html %}

---

## 🛠Example code

Below is an example complete request snippet in different languages. The documentation continues to outline the full request in step by step detail. Please have a read of the documentation for clarity on creating a session. 

This is a basic example showing:

- One document authenticity check 
- Text extraction
- Liveness
- Face match.

### Install the SDK

{% code %}
{% tab language="javascript" %}
npm install -S -E yoti
{% /tab %}
{% tab language="java" %}
// If you are using Maven, add the following dependency:
<dependency>
    <groupId>com.yoti</groupId>
    <artifactId>yoti-sdk-api</artifactId>
    <version>3.0.0</version>
</dependency>

// If you are using Gradle, add the following dependency:
compile group: 'com.yoti', name: 'yoti-sdk-api', version: '3.0.0'
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
// You can simply add a `require github.com/getyoti/yoti-go-sdk/v3` to go.mod.
// To download and install the Yoti SDK and its dependencies, run the following command from your terminal:

go get "github.com/getyoti/yoti-go-sdk/v3"
{% /tab %}
{% tab language="ruby" %}
gem install yoti

# The gem provides a configuration generator for Ruby on Rails:

rails generate yoti:install
{% /tab %}
{% tab language="java" title="Java v2" %}
// If you are using Maven, add the following dependency:
<dependency>
    <groupId>com.yoti</groupId>
    <artifactId>yoti-sdk-impl</artifactId>
    <version>2.12.0</version>
</dependency>

// If you are using Gradle, add the following dependency:
compile group: 'com.yoti', name: 'yoti-sdk-impl', version: '2.12.0'
{% /tab %}
{% /code %}

### Simple session

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
    SdkConfigBuilder

} = require('yoti');

const YOTI_CLIENT_SDK_ID = 'YOTI_CLIENT_SDK_ID';
const YOTI_PEM = fs.readFileSync(path.join(__dirname, '/path/to/pem'));
const docScanClient = new DocScanClient(YOTI_CLIENT_SDK_ID, YOTI_PEM);

    //Document Authenticity Check
const documentAuthenticityCheck = new RequestedDocumentAuthenticityCheckBuilder().build();

    //Liveness check with 3 retries
const livenessCheck = new RequestedLivenessCheckBuilder()
    .forZoomLiveness()
    .withMaxRetries(3)
    .build();

    //Face Match Check with manual check set to fallback
const faceMatchCheck = new RequestedFaceMatchCheckBuilder()
    .withManualCheckFallback()
    .build();

    //ID Document Text Extraction Task with manual check set to fallback
const textExtractionTask = new RequestedTextExtractionTaskBuilder()
    .withManualCheckFallback()
    .build();

    //Configuration for the client SDK (Frontend)
const sdkConfig = new SdkConfigBuilder()
    .withAllowsCameraAndUpload()
    .withPresetIssuingCountry('GBR')
    .withSuccessUrl('/success')
    .withErrorUrl('/error')
    .build();

    //Buiding the Session with defined specification from above
const sessionSpec = new SessionSpecificationBuilder()
    .withClientSessionTokenTtl(600)
    .withResourcesTtl(604800) 
    .withUserTrackingId('some-user-tracking-id')
    .withRequestedCheck(documentAuthenticityCheck)
    .withRequestedCheck(livenessCheck)
    .withRequestedCheck(faceMatchCheck)
    .withRequestedTask(textExtractionTask)
    .withSdkConfig(sdkConfig)
    .build();

    //Create Session
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
import com.yoti.api.client.docs.DocScanException;
import com.yoti.api.client.docs.session.create.CreateSessionResult;
import com.yoti.api.client.docs.session.create.SdkConfig;
import com.yoti.api.client.docs.session.create.SessionSpec;
import com.yoti.api.client.docs.session.create.check.RequestedDocumentAuthenticityCheck;
import com.yoti.api.client.docs.session.create.check.RequestedFaceMatchCheck;
import com.yoti.api.client.docs.session.create.check.RequestedLivenessCheck;
import com.yoti.api.client.docs.session.create.task.RequestedIdDocTextExtractionTask;

...
DocScanClient docScanClient = DocScanClient.builder()
        .withClientSdkId("YOTI_CLIENT_SDK_ID")
        .withKeyPairSource(ClassPathKeySource.fromClasspath("/path/to/pem"))
        .build();

        //Configuration for the client SDK (Frontend)
SdkConfig sdkConfig = SdkConfig.builder()
        .withAllowsCameraAndUpload()
        .withPrimaryColour("#2d9fff")
        .withSecondaryColour("#FFFFFF")
        .withFontColour("#FFFFFF")
        .withLocale("en-GB")
        .withPresetIssuingCountry("GBR")
        .withSuccessUrl("https://localhost:8443/success")
        .withErrorUrl("https://localhost:8443/error")
        .withBlockBiometricConsent(false)
        .build();

        //Buiding the Session with defined specification
SessionSpec sessionSpec = SessionSpec.builder()
        .withClientSessionTokenTtl(600)
        .withResourcesTtl(90000)
        .withUserTrackingId("some-user-tracking-id")
        .withSdkConfig(sdkConfig)
        //Document Authenticity Check
        .withRequestedCheck(
                RequestedDocumentAuthenticityCheck.builder()
                        .build()
        )
        //Face Match Check with manual check set to fallback
        .withRequestedCheck(
                RequestedFaceMatchCheck.builder()
                        .withManualCheckFallback()
                        .build()
        )
        //Liveness check with 3 retries
        .withRequestedCheck(
                RequestedLivenessCheck.builder()
                        .forZoomLiveness()
                        .withMaxRetries(3)
                        .build()

        //ID Document Text Extraction Task with manual check set to fallback
        .withRequestedTask(
                RequestedIdDocTextExtractionTask.builder()
                        .withManualCheckFallback()
                        .build()
        )
        .build();

        //Create session
CreateSessionResult sessionResult = docScanClient.createSession(sessionSpec);
{% /tab %}
{% tab language="php" %}
<?php

require_once './vendor/autoload.php';

use Yoti\DocScan\DocScanClient;
use Yoti\DocScan\Session\Create\Check\RequestedDocumentAuthenticityCheckBuilder;
use Yoti\DocScan\Session\Create\Check\RequestedFaceMatchCheckBuilder;
use Yoti\DocScan\Session\Create\Check\RequestedLivenessCheckBuilder;
use Yoti\DocScan\Session\Create\Task\RequestedTextExtractionTaskBuilder;
use Yoti\DocScan\Session\Create\SdkConfigBuilder;
use Yoti\DocScan\Session\Create\SessionSpecificationBuilder;

$YOTI_CLIENT_SDK_ID = 'YOTI_CLIENT_SDK_ID';
$YOTI_PEM = '/path/to/pem';

$client = new DocScanClient($YOTI_CLIENT_SDK_ID, $YOTI_PEM);

$sessionSpec = (new SessionSpecificationBuilder())
    ->withClientSessionTokenTtl(600)
    ->withResourcesTtl(604800)
    ->withUserTrackingId('some-user-tracking-id')
    
    //Document Authenticity Check
    ->withRequestedCheck(
        (new RequestedDocumentAuthenticityCheckBuilder())
            ->build()
    )
    //Liveness check with 3 retries
    ->withRequestedCheck(
        (new RequestedLivenessCheckBuilder())
            ->forZoomLiveness()
            ->build()
    )
    //Face Match Check with manual check set to fallback
    ->withRequestedCheck(
        (new RequestedFaceMatchCheckBuilder())
            ->withManualCheckFallback()
            ->build()
    )

    //ID Document Text Extraction Task with manual check set to fallback
    ->withRequestedTask(
        (new RequestedTextExtractionTaskBuilder())
            ->withManualCheckAlways()
            ->build()
    )
    //Configuration for the client SDK (Frontend)
    ->withSdkConfig(
        (new SdkConfigBuilder())
            ->withAllowsCameraAndUpload()
            ->withPresetIssuingCountry('GBR')
            ->withSuccessUrl('/your/success/url')
            ->withErrorUrl('/your/error/url')
            ->build()
    )
    ->build();

$session = $client->createSession($sessionSpec);
{% /tab %}
{% tab language="python" %}
# Coming soon
{% /tab %}
{% tab language="csharp" %}
// Coming soon
{% /tab %}
{% tab language="go" %}
// Coming soon
{% /tab %}
{% tab language="ruby" %}
# Coming soon
{% /tab %}
{% /code %}

### Full session

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
    ProofOfAddressObjectiveBuilder,
    RequiredSupplementaryDocumentBuilder,
  	RequiredIdDocumentBuilder,
    OrthogonalRestrictionsFilterBuilder

} = require('yoti');

const YOTI_CLIENT_SDK_ID = 'YOTI_CLIENT_SDK_ID';
const YOTI_PEM = fs.readFileSync(path.join(__dirname, '/path/to/pem'));
const docScanClient = new DocScanClient(YOTI_CLIENT_SDK_ID, YOTI_PEM);

const filter = new OrthogonalRestrictionsFilterBuilder()
    // Allow from specific countries
    .withWhitelistedCountries(['GBR', 'JPN'])
    // Allow specific documents
    .withWhitelistedDocumentTypes(['PASSPORT'])
    .build();

    // First required document - with filter
const requiredDocument = new RequiredIdDocumentBuilder()
    .withFilter(filter)
    .build();

    //Second required document - no filter
const anotherRequiredDocument = new RequiredIdDocumentBuilder()
    .build();

    // Requesting a supporting document to aqquire proof of address
const supportingDocumentObjective = new ProofOfAddressObjectiveBuilder().build();

const supportingDocument = new RequiredSupplementaryDocumentBuilder()
    .withObjective(supportingDocumentObjective)
    .build();

    //Document Authenticity Check
const documentAuthenticityCheck = new RequestedDocumentAuthenticityCheckBuilder().build();

    //Compare the details on both documents are the same - only if 2 ID documents are required
const documentComparisonCheck = new RequestedIdDocumentComparisonCheckBuilder().build();

    //Liveness check with 3 retries
const livenessCheck = new RequestedLivenessCheckBuilder()
    .forZoomLiveness()
    .withMaxRetries(3)
    .build();

    //Face Match Check with manual check set to fallback
const faceMatchCheck = new RequestedFaceMatchCheckBuilder()
    .withManualCheckFallback()
    .build();

    //ID Document Text Extraction Task with manual check set to fallback
const textExtractionTask = new RequestedTextExtractionTaskBuilder()
    .withManualCheckFallback()
    .build();

    //Configuration for the client SDK (Frontend)
const sdkConfig = new SdkConfigBuilder()
    .withAllowsCameraAndUpload()
    .withPrimaryColour('#2d9fff')
    .withSecondaryColour('#FFFFFF')
    .withFontColour('#FFFFFF')
    .withLocale('en-GB')
    .withPresetIssuingCountry('GBR')
    .withSuccessUrl('/success')
    .withErrorUrl('/error')
    .withBlockBiometricConsent(false)
    .build();

    //Notifications config 
const notificationConfig = new NotificationConfigBuilder()
    .withEndpoint('https://yourdomain.example/idverify/updates')
    .withAuthToken('username:password')
    .forSessionCompletion()
    .build();

    //Buiding the Session with defined specification from above
const sessionSpec = new SessionSpecificationBuilder()
    .withClientSessionTokenTtl(600)
    .withResourcesTtl(604800) 
    .withUserTrackingId('some-user-tracking-id')
    .withRequiredDocument(requiredDocument)
    .withRequiredDocument(anotherRequiredDocument)   
    .withRequiredDocument(supportingDocument)
    .withRequestedCheck(documentAuthenticityCheck)
    .withRequestedCheck(documentComparisonCheck)
    .withRequestedCheck(livenessCheck)
    .withRequestedCheck(faceMatchCheck)
    .withRequestedTask(textExtractionTask)
    .withSdkConfig(sdkConfig)
    .withNotifications(notificationConfig)
    .build();

    //Create session
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
import com.yoti.api.client.docs.DocScanException;
import com.yoti.api.client.docs.session.create.CreateSessionResult;
import com.yoti.api.client.docs.session.create.NotificationConfig;
import com.yoti.api.client.docs.session.create.SdkConfig;
import com.yoti.api.client.docs.session.create.SessionSpec;
import com.yoti.api.client.docs.session.create.check.RequestedDocumentAuthenticityCheck;
import com.yoti.api.client.docs.session.create.check.RequestedFaceMatchCheck;
import com.yoti.api.client.docs.session.create.check.RequestedLivenessCheck;
import com.yoti.api.client.docs.session.create.check.RequestedIdDocumentComparisonCheck;
import com.yoti.api.client.docs.session.create.task.RequestedIdDocTextExtractionTask;
import com.yoti.api.client.docs.session.create.filters.OrthogonalRestrictionsFilter;
import com.yoti.api.client.docs.session.create.objectives.ProofOfAddressObjective;
import com.yoti.api.client.docs.session.create.filters.RequiredSupplementaryDocument;
import com.yoti.api.client.docs.session.create.filters.RequiredIdDocument;


...
DocScanClient docScanClient = DocScanClient.builder()
        .withClientSdkId("YOTI_CLIENT_SDK_ID")
        .withKeyPairSource(ClassPathKeySource.fromClasspath("/path/to/pem"))
        .build();

        //Configuration for the client SDK (Frontend)
SdkConfig sdkConfig = SdkConfig.builder()
        .withAllowsCameraAndUpload()
        .withPrimaryColour("#2d9fff")
        .withSecondaryColour("#FFFFFF")
        .withFontColour("#FFFFFF")
        .withLocale("en-GB")
        .withPresetIssuingCountry("GBR")
        .withSuccessUrl("https://localhost:8443/success")
        .withErrorUrl("https://localhost:8443/error")
        .withBlockBiometricConsent(false)
        .build();

        //Buiding the Session with defined specification
SessionSpec sessionSpec = SessionSpec.builder()
        .withClientSessionTokenTtl(600)
        .withResourcesTtl(90000)
        .withUserTrackingId("some-user-tracking-id")
        .withSdkConfig(sdkConfig)
        // First required document - with filter
        .withRequiredDocument(
                RequiredIdDocument.builder()
                        .withFilter(
                                OrthogonalRestrictionsFilter.builder()
                                        // Allow from specific countries
                                        .withWhitelistedCountries(['GBR', 'JPN'])
                                        // Allow specific documents
                                        .withWhitelistedDocumentTypes(['PASSPORT'])
                                        .build();
                        )
                        .build()
        )
        //Second required document - no filter
        .withRequiredDocument(
                RequiredIdDocument.builder()
                    .build()
         )
        // Requesting a supporting document to aqquire proof of address
        .withRequiredDocument(
                RequiredSupplementaryDocument.builder()
                        .withObjective(
                                ProofOfAddressObjective.builder(
                                        .build()
                                )
                        .build()
                        )  
        )
        //Document Authenticity Check
        .withRequestedCheck(
                RequestedDocumentAuthenticityCheck.builder()
                        .build()
        )
        //Face Match Check with manual check set to fallback
        .withRequestedCheck(
                RequestedFaceMatchCheck.builder()
                        .withManualCheckFallback()
                        .build()
        )
        //Liveness check with 3 retries
        .withRequestedCheck(
                RequestedLivenessCheck.builder()
                        .forZoomLiveness()
                        .withMaxRetries(3)
                        .build()
        )
        //Compare the details on both documents are the same - only if 2 ID documents are required
        .withRequestedCheck(
                .RequestedIdDocumentComparisonCheck.builder()
                        .build() 
        )
        //ID Document Text Extraction Task with manual check set to fallback
        .withRequestedTask(
                RequestedIdDocTextExtractionTask.builder()
                        .withManualCheckFallback()
                        .build()
        )
        //Notifications config 
        .withNotifications(
                NotificationConfig.builder()
                        .withEndpoint("https://yourdomain.example/idverify/updates")
                        .withAuthToken("some_auth_token")
                        .forSessionCompletion()
                        .build()
        )
        .build();

        //Create session
CreateSessionResult sessionResult = docScanClient.createSession(sessionSpec);
{% /tab %}
{% tab language="php" %}
<?php

require_once './vendor/autoload.php';

use Yoti\DocScan\DocScanClient;
use Yoti\DocScan\Session\Create\Check\RequestedDocumentAuthenticityCheckBuilder;
use Yoti\DocScan\Session\Create\Check\RequestedFaceMatchCheckBuilder;
use Yoti\DocScan\Session\Create\Check\RequestedLivenessCheckBuilder;
use Yoti\DocScan\Session\Create\Check\RequestedIdDocumentComparisonCheckBuilder;
use Yoti\DocScan\Session\Create\Task\RequestedTextExtractionTaskBuilder;
use Yoti\DocScan\Session\Create\Filters\RequiredIdDocumentBuilder;
use Yoti\DocScan\Session\Create\Filters\RequiredSupplementaryDocumentBuilder;
use Yoti\DocScan\Session\Create\Filters\Orthogonal\OrthogonalRestrictionsFilterBuilder;
use Yoti\DocScan\Session\Create\Objective\ProofOfAddressObjectiveBuilder;
use Yoti\DocScan\Session\Create\SdkConfigBuilder;
use Yoti\DocScan\Session\Create\SessionSpecificationBuilder;
use Yoti\DocScan\Session\Create\NotificationConfigBuilder;

$YOTI_CLIENT_SDK_ID = 'YOTI_CLIENT_SDK_ID';
$YOTI_PEM = '/path/to/pem';

$client = new DocScanClient($YOTI_CLIENT_SDK_ID, $YOTI_PEM);

$sessionSpec = (new SessionSpecificationBuilder())
    ->withClientSessionTokenTtl(600)
    ->withResourcesTtl(604800)
    ->withUserTrackingId('some-user-tracking-id')
    
    // First required document - with filter
    ->withRequiredDocument(
        (new RequiredIdDocumentBuilder())
            ->withFilter(
                (new OrthogonalRestrictionsFilterBuilder())
                    // Allow from specific countries
                    ->withWhitelistedCountries(['GBR', 'JPN'])
                    // Allow specific documents
                    ->withWhitelistedDocumentTypes(['PASSPORT'])
                    ->build()
            )
            ->build()
    )

    //Second required document - no filter
    ->withRequiredDocument(
        (new RequiredIdDocumentBuilder())
            ->build()
    )
    
    // Requesting a supporting document to aqquire proof of address
    ->withRequiredDocument(
        (new RequiredSupplementaryDocumentbuilder())
                ->withObjective(
                        (new ProofOfAddressObjectivebuilder())
                            ->build()
                )
                ->build()
    )  

    //Document Authenticity Check
    ->withRequestedCheck(
        (new RequestedDocumentAuthenticityCheckBuilder())
            ->build()
    )
    //Liveness check with 3 retries
    ->withRequestedCheck(
        (new RequestedLivenessCheckBuilder())
            ->forZoomLiveness()
            ->build()
    )
    //Face Match Check with manual check set to fallback
    ->withRequestedCheck(
        (new RequestedFaceMatchCheckBuilder())
            ->withManualCheckFallback()
            ->build()
    )
    //Compare the details on both documents are the same - only if 2 ID documents are required
    ->withRequestedCheck(
        (new RequestedIdDocumentComparisonCheckBuilder())
            ->build()
    )
    //ID Document Text Extraction Task with manual check set to fallback
    ->withRequestedTask(
        (new RequestedTextExtractionTaskBuilder())
            ->withManualCheckAlways()
            ->build()
    )
    //Configuration for the client SDK (Frontend)
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
            ->withBlockBiometricConsent(false)
            ->build()
    )
    //Notifications config 
    ->withNotifications(
        (new NotificationConfigBuilder())
            ->withEndpoint('https://yourdomain.example/idverify/updates')
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
package main

import (
	"io/ioutil"

	"github.com/getyoti/yoti-go-sdk/v3/docscan"
	"github.com/getyoti/yoti-go-sdk/v3/docscan/session/create"
	"github.com/getyoti/yoti-go-sdk/v3/docscan/session/create/check"
	"github.com/getyoti/yoti-go-sdk/v3/docscan/session/create/filter"
	"github.com/getyoti/yoti-go-sdk/v3/docscan/session/create/objective"
	"github.com/getyoti/yoti-go-sdk/v3/docscan/session/create/task"
)

var (
	sdkId               string
	key                 []byte
	client              *docscan.Client
	createSessionResult *create.SessionResult
)

func main() {
	sdkId := "YOTI_CLIENT_SDK_ID"
	key, _ := ioutil.ReadFile("/path/to/pem")

	client, err := docscan.NewClient(sdkId, key)

	sessionSpec, err := buildSessionSpec()

	createSessionResult, err = client.CreateSession(sessionSpec)

	sessionId := createSessionResult.SessionID
	clientSessionToken := createSessionResult.ClientSessionToken
}

func buildSessionSpec() (sessionSpec *create.SessionSpecification, err error) {
	var faceMatchCheck *check.RequestedFaceMatchCheck
	faceMatchCheck, err = check.NewRequestedFaceMatchCheckBuilder().
		WithManualCheckAlways().
		Build()
	if err != nil {
		return nil, err
	}

	var documentAuthenticityCheck *check.RequestedDocumentAuthenticityCheck
	documentAuthenticityCheck, err = check.NewRequestedDocumentAuthenticityCheckBuilder().
		Build()
	if err != nil {
		return nil, err
	}

	var livenessCheck *check.RequestedLivenessCheck
	livenessCheck, err = check.NewRequestedLivenessCheckBuilder().
		ForZoomLiveness().
		WithMaxRetries(5).
		Build()
	if err != nil {
		return nil, err
	}

	var textExtractionTask *task.RequestedTextExtractionTask
	textExtractionTask, err = task.NewRequestedTextExtractionTaskBuilder().
		WithManualCheckAlways().
		Build()
	if err != nil {
		return nil, err
	}

	var sdkConfig *create.SDKConfig
	sdkConfig, err = create.NewSdkConfigBuilder().
		WithAllowsCameraAndUpload().
		WithPrimaryColour("#2d9fff").
		WithSecondaryColour("#FFFFFF").
		WithFontColour("#FFFFFF").
		WithLocale("en-GB").
		WithPresetIssuingCountry("GBR").
		WithSuccessUrl("https://localhost:8080/success").
		WithErrorUrl("https://localhost:8080/error").
		Build()

	if err != nil {
		return nil, err
	}

	sessionSpec, err = create.NewSessionSpecificationBuilder().
		WithClientSessionTokenTTL(600).
		WithResourcesTTL(90000).
		WithUserTrackingID("some-tracking-id").
		WithRequestedCheck(faceMatchCheck).
		WithRequestedCheck(documentAuthenticityCheck).
		WithRequestedCheck(livenessCheck).
		WithRequestedTask(textExtractionTask).
		WithSDKConfig(sdkConfig).
		Build()

	if err != nil {
		return nil, err
	}
	return sessionSpec, nil
}
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
{% tab language="java" title="Java v2" %}
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
{% /code %}