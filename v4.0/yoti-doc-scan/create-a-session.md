---
type: page
title: Create a Session
listed: false
slug: create-a-session
description: 
index_title: Create a Session
hidden: 
keywords: 
tags: 
---

Once you have added the Yoti SDK dependency to your project, you can use it to build and send your session. Every time an end user elects to supply a document(s) on the relying party app/website/custom product, a session is created.

{% table %}
| Name | Acts on | Type | Manual / Auto | Description | 
| ---- | ---- | ---- | ---- | ---- | 
| Document authenticity | 1x Document Resource | Asynchronous | Manual | To determine the validity of the ID document. Must wait for the TextDataCheck, if there is one. | 
| Liveness | 1x Liveness Resource | Synchronous | Auto | A check to assess whether the document scan is being performed by a real person and not someone wearing a mask or an automated system. Runs as soon as the FaceMap is uploaded. Can be repeated until it succeeds, but only one successful _Check_ is allowed in each _Session._ | 
| Face match | 1x Doc Resource & 1x Liveness Resource | Asynchronous | Auto &  or Manual | A request to assess whether the user's face matches the face on the ID document. The user's facial image is obtained from the liveness check, which must be performed first. Must wait for the TextDataCheck, if there is one. | 
| Text extraction | 1 x Document Resource | Asynchronous | Auto &  or Manual | Used to recover a failed TextExtractionTask | 
| Supporting documents | 1x Document Resource | Asynchronous | Manual | A check to request an additional document as a proof of address check. | 
| Client \n\npreferences | N/A | N/A | N/A | Camera and preset country options and where the user should be directed after the user journey (success/error redirect URL). | 
| System preferences | N/A | N/A | N/A | Doc Scan session length (seconds) and user tracking. | 
| Notification | N/A | N/A | N/A | An update notification when the session state changes, based on the selected subscription topics. | 
{% /table %}

---

## Example

Below is an example complete request snippet in different languages. The documentation continues to outline the full request in step by step detail.

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
// You can simply add a `require github.com/getyoti/yoti-go-sdk/v3` to go.mod.
// To download and install the Yoti SDK and its dependencies, run the following command from your terminal:

go get "github.com/getyoti/yoti-go-sdk/v3"
{% /tab %}
{% tab language="ruby" %}
gem install yoti

# The gem provides a configuration generator for Ruby on Rails:

rails generate yoti:install
{% /tab %}
{% /code %}

### This is a basic example showing 1 document with text extraction, liveness and face match.

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
{% /code %}