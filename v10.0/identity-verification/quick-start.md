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

We suggest you read through the step by step integration guide to understand the integration in detail. Please see below for example code snippets and examples projects.

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
			You will need to access your Yoti Hub account with an e-mail & password or using the Yoti mobile app and to have registered your business with Yoti. Click below for more info.
   </div>
   <div class="alert-links"> 
         <a target="_self" href="https://developers.yoti.com/yoti/identity-verification/getting-started">View Onboarding with Yoti</a>
   </div>
</div>
{% /html %}

## Example code

Below is an example complete request snippet in different languages.

### Install the SDK

{% code %}
{% tab language="javascript" title="Node.js" %}
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
implementation group: 'com.yoti', name: 'yoti-sdk-api', version: '3.8.0'
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
{% /code %}

### Basic session

This is a basic example showing:

- One document authenticity check
- Text extraction
- Liveness
- Face match.

{% code %}
{% tab language="javascript" title="Node.js" %}
const path = require('path');
const fs = require('fs');

const {
    IDVClient,
    SessionSpecificationBuilder,
    RequestedDocumentAuthenticityCheckBuilder,
    RequestedLivenessCheckBuilder,
    RequestedTextExtractionTaskBuilder,
    RequestedFaceMatchCheckBuilder,
    SdkConfigBuilder

} = require('yoti');

const YOTI_CLIENT_SDK_ID = 'YOTI_CLIENT_SDK_ID';
const YOTI_PEM = fs.readFileSync(path.join(__dirname, '/path/to/pem'));
const idvClient = new IDVClient(YOTI_CLIENT_SDK_ID, YOTI_PEM);

    //Document Authenticity Check
const documentAuthenticityCheck = new RequestedDocumentAuthenticityCheckBuilder().build();

    //Liveness check with 3 retries
const livenessCheck = new RequestedLivenessCheckBuilder()
    .forStaticLiveness()
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
idvClient
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
        .withPresetIssuingCountry("GBR")
        .withSuccessUrl("https://localhost:8443/success")
        .withErrorUrl("https://localhost:8443/error")
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
                        .forStaticLiveness()
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
CreateSessionResult sessionResult = docScanClient.createSession(sessionSpec);// Click to edit code
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
            ->forStaticLiveness()
            ->withMaxRetries(3)
            ->build()
    )
    ->withRequestedCheck(
        (new RequestedFaceMatchCheckBuilder())
            ->withManualCheckFallback()
            ->build()
    )
    ->withRequestedTask(
        (new RequestedTextExtractionTaskBuilder())
            ->withManualCheckFallback()
            ->build()
    )
    ->withSdkConfig(
        (new SdkConfigBuilder())
            ->withPrimaryColour('#2d9fff')
            ->withPresetIssuingCountry('GBR')
            ->withSuccessUrl('/your/success/url')
            ->withErrorUrl('/your/error/url')
            ->withAllowHandoff(true)
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
    .with_primary_colour("#2d9fff")
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
        .with_liveness_type("STATIC")
        .with_max_retries(3)
        .build()
    )
    .with_requested_check(
        RequestedFaceMatchCheckBuilder().with_manual_check_fallback().build()
    )
    .with_requested_task(
        RequestedTextExtractionTaskBuilder().with_manual_check_fallback().build()
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
        .ForStaticLiveness()
        .WithMaxRetries(3)
        .Build()
    )
    .WithRequestedCheck(
        new RequestedFaceMatchCheckBuilder()
        .WithManualCheckFallback()
        .Build()
    )
    .WithRequestedTask(
        new RequestedTextExtractionTaskBuilder()
        .WithManualCheckFallback()
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
        .WithPrimaryColour("#2d9fff")
        .WithPresetIssuingCountry("GBR")
        .WithSuccessUrl(Path.Combine("/success"))
        .WithErrorUrl(Path.Combine("/error"))
        .WithAllowHandoff(true)
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
		WithManualCheckFallback().
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
		ForStaticLiveness().
		WithMaxRetries(3).
		Build()
	if err != nil {
		return nil, err
	}

	var textExtractionTask *task.RequestedTextExtractionTask
	textExtractionTask, err = task.NewRequestedTextExtractionTaskBuilder().
		WithManualCheckFallback().
		Build()
	if err != nil {
		return nil, err
	}

	var sdkConfig *create.SDKConfig
	sdkConfig, err = create.NewSdkConfigBuilder().
		WithPrimaryColour("#2d9fff").
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
{% tab language="json" %}
{
    "client_session_token_ttl": 900,
    "resources_ttl": 90000,
    "user_tracking_id": "some-user-tracking-id",
    "block_biometric_consent": false,
    "requested_checks": [
        {
            "type": "ID_DOCUMENT_AUTHENTICITY",
            "config": {
                "manual_check": "ALWAYS"
            }
        },
        {
            "type": "LIVENESS",
            "config": {
                "liveness_type": "STATIC",
                "max_retries": 3
            }
        },
        {
            "type": "ID_DOCUMENT_FACE_MATCH",
            "config": {
                "manual_check": "FALLBACK"
            }
        }
    ],
    "requested_tasks": [
        {
            "type": "ID_DOCUMENT_TEXT_DATA_EXTRACTION",
            "config": {
                "manual_check": "FALLBACK"
            }
        }
    ],
    "sdk_config": {
        "primary_colour": "#2d9fff",
        "preset_issuing_country": "GBR",
        "success_url": "https://localhost:8443/success",
        "error_url": "https://localhost:8443/error",
        "allow_handoff": true
    }
}
{% /tab %}
{% /code %}

### Advanced session

This is an advanced example showing:

- One document authenticity check
- Text extraction
- Liveness
- Face match
- Supporting document
- Proof of address
- Document filters.

{% code %}
{% tab language="javascript" title="Node.js" %}
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
const idvClient = new IDVClient(YOTI_CLIENT_SDK_ID, YOTI_PEM);

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

// Second required document - no filter
const anotherRequiredDocument = new RequiredIdDocumentBuilder()
    .build();

// Requesting a supporting document to aqquire proof of address
const supportingDocumentObjective = new ProofOfAddressObjectiveBuilder().build();

const supportingDocument = new RequiredSupplementaryDocumentBuilder()
    .withObjective(supportingDocumentObjective)
    .build();

// Document Authenticity Check
const documentAuthenticityCheck = new RequestedDocumentAuthenticityCheckBuilder().build();

// Compare the details on both documents are the same - only if 2 ID documents are required
const documentComparisonCheck = new RequestedIdDocumentComparisonCheckBuilder().build();

// Liveness check with 3 retries
const livenessCheck = new RequestedLivenessCheckBuilder()
    .forStaticLiveness()
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
    .withPrivacyPolicyUrl('/privacy-policy')
    .withAllowHandoff(true)
    .withIdDocumentTextExtractionGenericRetries(3)
    .withIdDocumentTextExtractionReclassificationRetries(3)
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
idvClient
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
        .withPresetIssuingCountry("GBR")
        .withSuccessUrl("https://localhost:8443/success")
        .withErrorUrl("https://localhost:8443/error")
        .withPrivacyPolicyUrl("https://localhost:8443/privacy-policy")
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
                        .forStaticLiveness()
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
// Coming soon
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
{% tab language="json" %}
{
    "client_session_token_ttl": 900,
    "resources_ttl": 90000,
    "user_tracking_id": "some-user-tracking-id",
    "block_biometric_consent": false,
    "notifications": {
        "endpoint": "https://yourdomain.example/idverify/updates",
        "topics": [
          "SESSION_COMPLETION"
        ],
        "auth_token": "some_auth_token",
        "auth_type": "BASIC"
      },
    "requested_checks": [
        {
            "type": "ID_DOCUMENT_AUTHENTICITY",
            "config": {
                "manual_check": "FALLBACK"
            }
        },
        {
            "type": "LIVENESS",
            "config": {
                "liveness_type": "STATIC",
                "max_retries": 3
            }
        },
        {
            "type": "ID_DOCUMENT_FACE_MATCH",
            "config": {
                "manual_check": "FALLBACK"
            }
        }
    ],
    "requested_tasks": [
        {
            "type": "SUPPLEMENTARY_DOCUMENT_TEXT_DATA_EXTRACTION",
            "config": {
                "manual_check": "NEVER"
            }
        },
        {
            "type": "ID_DOCUMENT_TEXT_DATA_EXTRACTION",
            "config": {
                "manual_check": "FALLBACK"
            }
        }
    ],
    "sdk_config": {
        "allowed_capture_methods": "CAMERA_AND_UPLOAD",
        "primary_colour": "#2d9fff",
        "locale": "en-GB",
        "preset_issuing_country": "GBR",
        "success_url": "https://localhost:8443/success",
        "error_url": "https://localhost:8443/error",
        "privacy_policy_url": "https://localhost:8443/privacy-policy",
        "allow_handoff": true
    },
    "required_documents": [
        {
            "type": "ID_DOCUMENT",
            "filter": {
                "type": "ORTHOGONAL_RESTRICTIONS",
                "country_restriction": {
                    "inclusion": "WHITELIST",
                    "country_codes": [
                        "GBR",
                        "USA"
                    ]
                },
                "type_restriction": {
                    "inclusion": "WHITELIST",
                    "document_types": [
                        "PASSPORT"
                    ]
                }
            }
        },
        {
            "type": "ID_DOCUMENT"
        },
        {
            "type": "SUPPLEMENTARY_DOCUMENT",
            "objective": {
                "type": "PROOF_OF_ADDRESS"
            }
        }
    ]
}
{% /tab %}
{% /code %}

---

## Web examples

If we don't support your language please [get in touch](https://developers.yoti.com/yoti/get-in-touch) with us.

{% table widths="" %}
| Production | Sandbox | 
| ---- | ---- | 
| [Javascript](https://github.com/getyoti/yoti-node-sdk/tree/master/examples/idv) | [Javascript](https://github.com/getyoti/yoti-node-sdk-sandbox/tree/master/examples/doc_scan) | 
| [Java](https://github.com/getyoti/yoti-java-sdk/tree/master/examples/doc-scan) | [Java](https://github.com/getyoti/yoti-java-sdk) | 
| [PHP](https://github.com/getyoti/yoti-php-sdk/tree/master/examples/doc-scan) | [PHP](https://github.com/getyoti/yoti-php-sdk-sandbox/tree/master/examples/doc-scan) | 
| [Python](https://github.com/getyoti/yoti-python-sdk/tree/master/examples/doc_scan) | [Python](https://github.com/getyoti/yoti-python-sdk-sandbox/tree/master/examples) | 
| [.NET](https://github.com/getyoti/yoti-dotnet-sdk/tree/master/src/Examples/DocScan/DocScanExample) | .[NET](https://github.com/getyoti/yoti-dotnet-sdk-sandbox/tree/master/Examples/Yoti.Auth.Sandbox.Examples) | 
| [Go](https://github.com/getyoti/doc-scan-examples/tree/master/go) | [Go](https://github.com/getyoti/yoti-go-sdk/tree/master/_examples/docscansandbox) | 
{% /table %}