---
type: page
title: Migration Guide
listed: true
slug: migration-guide
description: This guide provides instructions on how to migrate from Active to Passive liveness in the Identity Verification (IDV) SDK. Follow the guide to implement the necessary configurations.
index_title: Migration Guide
hidden: 
keywords: 
tags: 
---

This acts as a reference guide for migrating from Active to Passive liveness in the Identity Verification (IDV) SDK.

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
{% tab language="python" %}
# Install the Yoti Python SDK via Pip
pip install yoti
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

## Session specification

Once you have added the Yoti SDK dependency to your project, you can use it to specify your IDV session with a liveness check as shown in the following code snippet(s).

### Active liveness

{% code %}
{% tab language="javascript" %}
const {
    RequestedLivenessCheckBuilder,
    SdkConfigBuilder,
    SessionSpecificationBuilder,
} = require('yoti');

// Active liveness check with 3 retries
const livenessCheck = new RequestedLivenessCheckBuilder()
    .forZoomLiveness()
    .withMaxRetries(3)
    .build();

// Configuration for the client SDK (Frontend)
const sdkConfig = new SdkConfigBuilder()
    .withAllowsCameraAndUpload()
    .withPresetIssuingCountry('GBR')
    .withSuccessUrl('https://localhost:8443/success')
    .withErrorUrl('https://localhost:8443/error')
    .build();

// Build the Session specification
const sessionSpec = new SessionSpecificationBuilder()
    .withClientSessionTokenTtl(900)
    .withResourcesTtl(90000) 
    .withUserTrackingId('some-user-tracking-id')
    .withRequestedCheck(livenessCheck)
    .withSdkConfig(sdkConfig)
    .build();
{% /tab %}
{% tab language="java" %}
import com.yoti.api.client.docs.session.create.check.RequestedLivenessCheck;
import com.yoti.api.client.docs.session.create.SdkConfig;
import com.yoti.api.client.docs.session.create.SessionSpec;

...
// Active liveness check with 3 retries
RequestedLivenessCheck livenessCheck = RequestedLivenessCheck.builder()
    .forZoomLiveness()
    .withMaxRetries(3)
    .build()
  
// Configuration for the client SDK (Frontend)
SdkConfig sdkConfig = SdkConfig.builder()
  	.withAllowsCameraAndUpload()
    .withPresetIssuingCountry("GBR")
    .withSuccessUrl("https://localhost:8443/success")
    .withErrorUrl("https://localhost:8443/error")
    .build();

// Build the Session specification
SessionSpec sessionSpec = SessionSpec.builder()
    .withClientSessionTokenTtl(900)
    .withResourcesTtl(90000)
    .withUserTrackingId("some-user-tracking-id")
    .withSdkConfig(sdkConfig)
  	.withRequestedCheck(livenessCheck)
  	.build();
{% /tab %}
{% tab language="php" %}
<?php
  
require_once './vendor/autoload.php';

use Yoti\DocScan\Session\Create\Check\RequestedLivenessCheckBuilder;
use Yoti\DocScan\Session\Create\SdkConfigBuilder;
use Yoti\DocScan\Session\Create\SessionSpecificationBuilder;

// Active liveness check with 3 retries
$livenessCheck = (new RequestedLivenessCheckBuilder())
    ->forZoomLiveness()
    ->withMaxRetries(3)
    ->build()
  
// Configuration for the client SDK (Frontend)
$sdkConfig = (new SdkConfigBuilder())
    ->withAllowsCameraAndUpload()
    ->withPresetIssuingCountry('GBR')
    ->withSuccessUrl('https://localhost:8443/success')
    ->withErrorUrl('https://localhost:8443/error')
    ->build()
  
// Build the Session specification
$sessionSpec = (new SessionSpecificationBuilder())
    ->withClientSessionTokenTtl(900)
    ->withResourcesTtl(90000)
    ->withUserTrackingId('some-user-tracking-id')
    ->withRequestedCheck($livenessCheck)
  	->withSdkConfig($sdkConfig)
  	->build();
{% /tab %}
{% tab language="python" %}
from yoti_python_sdk.doc_scan import (
    RequestedLivenessCheckBuilder,
    SdkConfigBuilder,
    SessionSpecBuilder
)

# Active liveness check with 3 retries
liveness_check = RequestedLivenessCheckBuilder()
    .for_zoom_liveness()
    .with_max_retries(3)
    .build()  
      
# Configuration for the client SDK (Frontend)
sdk_config = (
    SdkConfigBuilder()
    .with_allows_camera_and_upload()
    .with_preset_issuing_country("GBR")
    .with_success_url("https://localhost:8443/success")
    .with_error_url("https://localhost:8443/error")
    .build()
)

# Build the Session specification
session_spec = (
    SessionSpecBuilder()
    .with_client_session_token_ttl(900)
    .with_resources_ttl(90000)
    .with_user_tracking_id("some-user-tracking-id")
    .with_requested_check(liveness_check)
    .with_sdk_config(sdk_config)
    .build()
)
{% /tab %}
{% tab language="csharp" %}
using Yoti.Auth.DocScan.Session.Create;
using Yoti.Auth.DocScan.Session.Create.Check;

// Active liveness check with 3 retries
var livenessCheck = new RequestedLivenessCheckBuilder()
    .ForZoomLiveness()
    .WithMaxRetries(3)
    .Build();

// Configuration for the client SDK (Frontend)
var sdkConfig = new SdkConfigBuilder()
    .WithAllowsCameraAndUpload()
    .WithPresetIssuingCountry("GBR")
    .WithSuccessUrl("https://localhost:8443/success")
    .WithErrorUrl("https://localhost:8443/error")
    .Build();
  
// Build the Session specification
var sessionSpec = new SessionSpecificationBuilder()
    .WithClientSessionTokenTtl(900)
    .WithResourcesTtl(90000)
    .WithUserTrackingId("some-user-tracking-id")
    .WithRequestedCheck(livenessCheck)
    .WithSdkConfig(sdkConfig)
    .Build();
{% /tab %}
{% tab language="go" %}
import (
	"github.com/getyoti/yoti-go-sdk/v3/docscan/session/create"
	"github.com/getyoti/yoti-go-sdk/v3/docscan/session/create/check"
)

// Active liveness check with 3 retries
var livenessCheck *check.RequestedLivenessCheck
livenessCheck, err = check.NewRequestedLivenessCheckBuilder()
    .ForZoomLiveness()
    .WithMaxRetries(3)
    .Build()

if err != nil {
  	return nil, err
}

// Configuration for the client SDK (Frontend)
var sdkConfig *create.SDKConfig
sdkConfig, err = create.NewSdkConfigBuilder().
    WithAllowsCameraAndUpload().
    WithPresetIssuingCountry("GBR").
    WithSuccessUrl("https://localhost:8443/success").
    WithErrorUrl("https://localhost:8443/error")
    Build()

if err != nil {
  	return nil, err
}

// Build the Session specification
var sessionSpec *create.SessionSpecification
sessionSpec, err = create.NewSessionSpecificationBuilder().
    WithClientSessionTokenTTL(900).
    WithResourcesTTL(90000).
    WithUserTrackingID("some-tracking-id").
    WithRequestedCheck(livenessCheck).
    WithSDKConfig(sdkConfig).
    Build()

if err != nil {
  	return nil, err
}
{% /tab %}
{% tab language="json" %}
{
    "client_session_token_ttl": 900,
    "resources_ttl": 90000,
    "user_tracking_id": "some-user-tracking-id",
    "requested_checks": [
        {
            "type": "LIVENESS",
            "config": {
                "liveness_type": "ZOOM",
                "max_retries": 3
            }
        },
    ],
    "requested_tasks": [],
    "sdk_config": {
        "allowed_capture_methods": "CAMERA_AND_UPLOAD",
        "locale": "en-GB",
        "preset_issuing_country": "GBR",
        "success_url": "https://localhost:8443/success",
        "error_url": "https://localhost:8443/error"
    }
}
{% /tab %}
{% /code %}

### Passive liveness

{% code %}
{% tab language="javascript" %}
const {
    RequestedLivenessCheckBuilder,
    SdkConfigBuilder,
    SessionSpecificationBuilder,
} = require('yoti');

// Passive (Static) liveness check with 3 retries
const livenessCheck = new RequestedLivenessCheckBuilder()
    .forStaticLiveness()
    .withMaxRetries(3)
    .build();

// Configuration for the client SDK (Frontend)
const sdkConfig = new SdkConfigBuilder()
    .withAllowsCameraAndUpload()
    .withPresetIssuingCountry('GBR')
    .withSuccessUrl('/success')
    .withErrorUrl('/error')
    .build();

// Build the Session specification
const sessionSpec = new SessionSpecificationBuilder()
    .withClientSessionTokenTtl(900)
    .withResourcesTtl(90000) 
    .withUserTrackingId('some-user-tracking-id')
    .withRequestedCheck(livenessCheck)
    .withSdkConfig(sdkConfig)
    .build();
{% /tab %}
{% tab language="java" %}
import com.yoti.api.client.docs.session.create.check.RequestedLivenessCheck;
import com.yoti.api.client.docs.session.create.SdkConfig;
import com.yoti.api.client.docs.session.create.SessionSpec;

...
// Passive (Static) liveness check with 3 retries
RequestedLivenessCheck livenessCheck = RequestedLivenessCheck.builder()
    .forStaticLiveness()
    .withMaxRetries(3)
    .build()
  
// Configuration for the client SDK (Frontend)
SdkConfig sdkConfig = SdkConfig.builder()
  	.withAllowsCameraAndUpload()
    .withPresetIssuingCountry("GBR")
    .withSuccessUrl("https://localhost:8443/success")
    .withErrorUrl("https://localhost:8443/error")
    .build();

// Build the Session specification
SessionSpec sessionSpec = SessionSpec.builder()
    .withClientSessionTokenTtl(900)
    .withResourcesTtl(90000)
    .withUserTrackingId("some-user-tracking-id")
    .withSdkConfig(sdkConfig)
  	.withRequestedCheck(livenessCheck)
  	.build();edit code
{% /tab %}
{% tab language="php" %}
<?php
  
require_once './vendor/autoload.php';

use Yoti\DocScan\Session\Create\Check\RequestedLivenessCheckBuilder;
use Yoti\DocScan\Session\Create\SdkConfigBuilder;
use Yoti\DocScan\Session\Create\SessionSpecificationBuilder;

// Passive (Static) liveness check with 3 retries
$livenessCheck = (new RequestedLivenessCheckBuilder())
    ->forStaticLiveness()
    ->withMaxRetries(3)
    ->build()
  
// Configuration for the client SDK (Frontend)
$sdkConfig = (new SdkConfigBuilder())
    ->withAllowsCameraAndUpload()
    ->withPresetIssuingCountry('GBR')
    ->withSuccessUrl('https://localhost:8443/success')
    ->withErrorUrl('https://localhost:8443/error')
    ->build()
  
// Build the Session specification
$sessionSpec = (new SessionSpecificationBuilder())
    ->withClientSessionTokenTtl(900)
    ->withResourcesTtl(90000)
    ->withUserTrackingId('some-user-tracking-id')
    ->withRequestedCheck($livenessCheck)
  	->withSdkConfig($sdkConfig)
  	->build();
{% /tab %}
{% tab language="python" %}
from yoti_python_sdk.doc_scan import (
    RequestedLivenessCheckBuilder,
    SdkConfigBuilder,
    SessionSpecBuilder
)

# Passive (Static) liveness check with 3 retries
liveness_check = RequestedLivenessCheckBuilder()
    .with_liveness_type("STATIC")
    .with_max_retries(3)
    .build()  
      
# Configuration for the client SDK (Frontend)
sdk_config = (
    SdkConfigBuilder()
    .with_allows_camera_and_upload()
    .with_preset_issuing_country("GBR")
    .with_success_url("https://localhost:8443/success")
    .with_error_url("https://localhost:8443/error")
    .build()
)

# Build the Session specification
session_spec = (
    SessionSpecBuilder()
    .with_client_session_token_ttl(900)
    .with_resources_ttl(90000)
    .with_user_tracking_id("some-user-tracking-id")
    .with_requested_check(liveness_check)
    .with_sdk_config(sdk_config)
    .build()
)
{% /tab %}
{% tab language="csharp" %}
using Yoti.Auth.DocScan.Session.Create;
using Yoti.Auth.DocScan.Session.Create.Check;

// Passive (Static) liveness check with 3 retries
var livenessCheck = new RequestedLivenessCheckBuilder()
    .ForStaticLiveness()
    .WithMaxRetries(3)
    .Build();

// Configuration for the client SDK (Frontend)
var sdkConfig = new SdkConfigBuilder()
    .WithAllowsCameraAndUpload()
    .WithPresetIssuingCountry("GBR")
    .WithSuccessUrl("https://localhost:8443/success")
    .WithErrorUrl("https://localhost:8443/error")
    .Build();
  
// Build the Session specification
var sessionSpec = new SessionSpecificationBuilder()
    .WithClientSessionTokenTtl(900)
    .WithResourcesTtl(90000)
    .WithUserTrackingId("some-user-tracking-id")
    .WithRequestedCheck(livenessCheck)
    .WithSdkConfig(sdkConfig)
    .Build();
{% /tab %}
{% tab language="go" %}
import (
	"github.com/getyoti/yoti-go-sdk/v3/docscan/session/create"
	"github.com/getyoti/yoti-go-sdk/v3/docscan/session/create/check"
)

// Passive (Static) liveness check with 3 retries
var livenessCheck *check.RequestedLivenessCheck
livenessCheck, err = check.NewRequestedLivenessCheckBuilder()
    .ForStaticLiveness()
    .WithMaxRetries(3)
    .Build()

if err != nil {
  	return nil, err
}

// Configuration for the client SDK (Frontend)
var sdkConfig *create.SDKConfig
sdkConfig, err = create.NewSdkConfigBuilder().
    WithAllowsCameraAndUpload().
    WithPresetIssuingCountry("GBR").
    WithSuccessUrl("https://localhost:8443/success").
    WithErrorUrl("https://localhost:8443/error")
    Build()

if err != nil {
  	return nil, err
}

// Build the Session specification
var sessionSpec *create.SessionSpecification
sessionSpec, err = create.NewSessionSpecificationBuilder().
    WithClientSessionTokenTTL(900).
    WithResourcesTTL(90000).
    WithUserTrackingID("some-tracking-id").
    WithRequestedCheck(livenessCheck).
    WithSDKConfig(sdkConfig).
    Build()

if err != nil {
  	return nil, err
}
{% /tab %}
{% tab language="json" %}
{
    "client_session_token_ttl": 900,
    "resources_ttl": 90000,
    "user_tracking_id": "some-user-tracking-id",
    "requested_checks": [
        {
            "type": "LIVENESS",
            "config": {
                "liveness_type": "STATIC",
                "max_retries": 3
            }
        },
    ],
    "requested_tasks": [],
    "sdk_config": {
        "allowed_capture_methods": "CAMERA_AND_UPLOAD",
        "locale": "en-GB",
        "preset_issuing_country": "GBR",
        "success_url": "https://localhost:8443/success",
        "error_url": "https://localhost:8443/error"
    }
}
{% /tab %}
{% /code %}

## Session creation

Once you have built the session specification, you can send the request to creation a session.

{% code %}
{% tab language="javascript" %}
const path = require('path');
const fs = require("fs");

const {
  	IDVClient
} = require('yoti');

const CLIENT_SDK_ID = 'YOTI_CLIENT_SDK_ID'
const PEM_PATH = 'YOTI_KEY_FILE_PATH'
const PEM_KEY = fs.readFileSync(path.join(__dirname, PEM_PATH));

const idvClient = new IDVClient(CLIENT_SDK_ID, PEM_KEY);

idvClient
    .createSession(sessionSpec)
    .then((session) => {
  			const sessionId = session.getSessionId();
  			const clientSessionToken = session.getClientSessionToken();
    })
    .catch((error) => {
        console.log(error)
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
    .withKeyPairSource(ClassPathKeySource.fromClasspath("YOTI_KEY_FILE_PATH"))
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
$YOTI_PEM = 'YOTI_KEY_FILE_PATH';

$docScanClient = new DocScanClient($YOTI_CLIENT_SDK_ID, $YOTI_PEM);

$session = $docScanClient->createSession($sessionSpec);

$sessionId = $session->getSessionId();
$clientSessionToken = $session->getClientSessionToken();
{% /tab %}
{% tab language="python" %}
from yoti_python_sdk.doc_scan import (
    DocScanClient
)

YOTI_CLIENT_SDK_ID = 'YOTI_CLIENT_SDK_ID'
YOTI_PEM = 'YOTI_KEY_FILE_PATH'

doc_scan_client = DocScanClient(YOTI_CLIENT_SDK_ID, YOTI_PEM)

session = doc_scan_client.create_session(session_spec)

session_id = session.session_id
client_session_token = session.client_session_token
{% /tab %}
{% tab language="csharp" %}
using System.IO;
using System.Net.Http;
using Yoti.Auth;
using Yoti.Auth.DocScan;

...
const string YOTI_CLIENT_SDK_ID = "YOTI_CLIENT_SDK_ID";
const string PEM_PATH = "YOTI_KEY_FILE_PATH";

StreamReader privateKeyStream = System.IO.File.OpenText(PEM_PATH);
var key = CryptoEngine.LoadRsaKey(privateKeyStream);

var docScanClient = new DocScanClient(YOTI_CLIENT_SDK_ID, key, new HttpClient());

CreateSessionResult createSessionResult = docScanClient.CreateSession(sessionSpec);

string sessionId = createSessionResult.SessionId;
string clientSessionToken = createSessionResult.ClientSessionToken;
...
{% /tab %}
{% tab language="go" %}
import (
	"io/ioutil"
	"github.com/getyoti/yoti-go-sdk/v3/docscan"
	"github.com/getyoti/yoti-go-sdk/v3/docscan/session/create"
	_ "github.com/joho/godotenv/autoload"
)

var (
	sdkID               string
	key                 []byte
	client              *docscan.Client
	createSessionResult *create.SessionResult
)

sdkID := "YOTI_CLIENT_SDK_ID";
key, _ := ioutil.ReadFile("YOTI_KEY_FILE_PATH")

client, err := docscan.NewClient(sdkId, key)
if err != nil {
  	return nil, err
}

createSessionResult, err = client.CreateSession(sessionSpec)
if err != nil {
  	return nil, err
}

sessionId = createSessionResult.SessionID
clientSessionToken = createSessionResult.ClientSessionToken
{% /tab %}
{% /code %}

## Retrieve session results

After a session has been created, you can use the Yoti SDK to retrieve the session result (containing results of the liveness check and associated resources).

{% code %}
{% tab language="javascript" %}
// Returns the session result
idvClient.getSession(sessionId).then(session => {
    // Returns the session state
    const state = session.getState();
  
  	// Returns all checks for the session
    const checks = session.getChecks();
  
    // Returns the session resources
    const resources = session.getResources();
}).catch(error => {
  	console.log(error)
})
{% /tab %}
{% tab language="java" %}
// Returns the session result
GetSessionResult sessionResult = docScanClient.getSession(sessionId);

// Returns the session state
String state = sessionResult.getState();

// Returns all checks for the session
List<? extends CheckResponse> checks = sessionResult.getChecks();

// Returns the session resources
ResourceContainer resources = sessionResult.getResources();
{% /tab %}
{% tab language="php" %}
<?php
// Returns the session result
$sessionResult = $docScanClient->getSession($sessionId);

// Returns the session state
$state = $sessionResult->getState();

// Returns all checks for the session
$checks = $sessionResult->getChecks();

// Returns the session resources
$resources = $sessionResult->getResources();
{% /tab %}
{% tab language="python" %}
# Returns the session result
session_result = doc_scan_client.get_session(session_id)

# Returns the session state
state = session_result.state

# Returns all checks for the session
checks = session_result.checks

# Returns the session resources
resources = session_result.resources
{% /tab %}
{% tab language="csharp" %}
// Returns the session result
GetSessionResult sessionResult = docScanClient.GetSession(sessionId);

// Returns the session state
string state = sessionResult.State;

// Returns all checks for the session
List<CheckResponse> checks = sessionResult.Checks;

// Returns the session resources
ResourceContainer resources = sessionResult.Resources;
{% /tab %}
{% tab language="go" %}
// Returns a session result
sessionResult, err := client.GetSession(sessionId)
if err != nil {
  	return nil, err
}

// Returns the session state
state = sessionResult.State

// Returns all checks for the session
checks = sessionResult.Checks

// Returns the session resources
resources = sessionResult.Resources
{% /tab %}
{% /code %}

### Liveness checks

The liveness checks include any attempts the user made to provide their liveness. It's possible that some of these attempts were rejected.

{% code %}
{% tab language="javascript" %}
// Returns the liveness checks
const livenessChecks = session.getLivenessChecks();

livenessChecks.map(check => {
    // Returns the id of the check
    const id = check.getId();

    // Returns the state of the check
    const state = check.getState();

    // Returns an array of resources used in the check
    const resourcesUsed = check.getResourcesUsed();

    // Returns the report for the check
    const report = check.getReport();

    // Returns the recommendation value, either APPROVE, NOT_AVAILABLE or REJECT
    const recommendation = report.getRecommendation().getValue();

    // Returns the report breakdown including sub-checks
    const breakdown = report.getBreakdown();

    breakdown.forEach(function (breakdown) {
        // Returns the sub-check
        const subCheck = breakdown.getSubCheck();

        // Returns the sub-check result
        const subCheckResult = breakdown.getResult();
    });
})
{% /tab %}
{% tab language="java" %}
// Returns the liveness checks
List<LivenessCheckResponse> livenessChecks = sessionResult.getLivenessChecks();

for (CheckResponse check: livenessChecks) {
    // Returns the id of the check
    String id = check.getId();
    
    // Returns the state of the check
    String state = check.getState();
    
    // Returns a list of resources used in the check
    List<String> resourcesUsed = check.getResourcesUsed();

    // Returns the report for the check
    ReportResponse report = check.getReport();

    // Returns the recommendation value, either APPROVE, NOT_AVAILABLE or REJECT
    String recommendationValue = report.getRecommendation().getValue();

    // Returns the report breakdown including sub-checks
    List<? extends BreakdownResponse> breakdown = report.getBreakdown();
  
  	for (BreakdownResponse breakdown: breakdown) {
        // Returns the sub-check
        String subCheck - breakdown.getSubCheck();

        // Returns the sub-check result
        String subCheckResult - breakdown.getResult();
    }
}
{% /tab %}
{% tab language="php" %}
// Returns the liveness checks
$livenessChecks = $sessionResult->getLivenessChecks();

foreach($livenessChecks as $check) {
    // Returns the id of the check
    $id = $check->getId();

    // Returns the state of the check
    $state = $check->getState();

    // Returns an array of resources used in the check
    $resourcesUsed = $check->getResourcesUsed();

    // Returns the report for the check
    $report = $check->getReport();

    // Returns the recommendation value, either APPROVE, NOT_AVAILABLE or REJECT
    $recommendationValue = $report->getRecommendation()->getValue();

    // Returns the report breakdown including sub-checks
    $breakdown = $report->getBreakdown();
  
  	foreach($breakdown as $breakdown) {
        // Returns the sub-check
        $subCheck = $breakdown->getSubCheck();

        // Returns the sub-check result
        $subCheckResult = $breakdown->getResult();
    }
}
{% /tab %}
{% tab language="python" %}
# Returns the liveness checks
liveness_checks = session_result.liveness_checks

for check in liveness_checks:
    # Returns the id of the check
    check_id = check.id

    # Returns the state of the check
    check_state = check.state

    # Returns an array of resources used in this check
    resources_used = check.resources_used

    # Returns tje report for the check
    report = check.report

    # Returns the recommendation value, either APPROVE, NOT_AVAILABLE or REJECT
    recommendation_value = report.recommendation.value

    # Returns the report breakdown including sub-checks
    breakdown = report.breakdown
    
    for breakdown in breakdown:
        # Returns the sub-check
        subCheck = breakdown.sub_check

        # Returns the sub-check result
        subCheckResult = breakdown.result
{% /tab %}
{% tab language="csharp" %}
// Returns the liveness checks
List<LivenessCheckResponse> livenessChecks = sessionResult.GetLivenessChecks();

foreach (CheckResponse check in livenessChecks)
{
    // Returns the id of the check
    string id = check.Id;

    // Returns the state of the check
    string state = check.State;

    // Returns an array of resources used in this check
    List<String> resourcesUsed = check.ResourcesUsed;

    // Returns the report for the check
    ReportResponse report = check.Report;

    // Returns the recommendation value, either APPROVE, NOT_AVAILABLE or REJECT
    string recommendationValue = report.Recommendation.Value;

    // Returns the report breakdown including sub-checks
    List<BreakdownResponse> breakdown = report.Breakdown;
  
    foreach (BreakdownResponse breakdown in breakdown)
    {
        // Returns the sub-check
        string subCheck = breakdown.SubCheck;

        // Returns the sub-check result
        string subCheckResult = breakdown.Result;
    }
}
{% /tab %}
{% tab language="go" %}
// Returns the liveness checks
livenessChecks = sessionResult.LivenessChecks

for _, check := range livenessChecks {
    // Returns the id of the chec
    id := check.ID

    // Returns the state of the check
    state := check.State

    // Returns an array of resources used in the check
    resourcesUsed := check.ResourcesUsed

    // Returns the report for the check
    report := check.Report

    // Returns the recommendation value, either APPROVE, NOT_AVAILABLE or REJECT
    recommendationValue := report.Recommendation.Value

    // Returns the report breakdown including sub-checks
    breakdown := report.Breakdown

    for _, subCheck := range breakdown {
        // Returns the sub-check
        subCheckValue := subCheck.SubCheck

        // Returns the sub-check result
        subCheckResult := subCheck.Result
    }
}
{% /tab %}
{% /code %}

### Liveness resources

The liveness resources include any media resources that were captured when the user provided their liveness.

{% code %}
{% tab language="javascript" %}
// Returns the liveness resources
const livenessResources = resources.getLivenessCapture();

livenessResources.forEach((liveness) => {
    // Get the liveness id
    const livenessId = liveness.getId();

    // Get the liveness type
    const livenessType = liveness.getLivenessType();
});
{% /tab %}
{% tab language="java" %}
// Returns the liveness resources
List<? extends LivenessResourceResponse> livenessResources = resources.getLivenessCapture();

for (LivenessResourceResponse liveness : livenessResources) {
    // Get the liveness id
    String livenessId = liveness.getId();
  
  	// Get the liveness type
    String livenessType = liveness.getType();
}
{% /tab %}
{% tab language="php" %}
// Returns the liveness resources
$livenessResources = $resources->getLivenessCapture();

foreach ($livenessResources as $liveness) {
    // Get the liveness id
    $livenessId = $liveness->getId();

    // Get the liveness type
    $livenessType = $liveness->getType();
});
{% /tab %}
{% tab language="python" %}
# Returns the liveness resources
liveness_resources = resources.liveness_capture

for liveness in liveness_resources:
    # Get the liveness id
    liveness_id = liveness.id

    # Get the liveness type
    liveness_type = liveness.type
{% /tab %}
{% tab language="csharp" %}
// Returns the liveness resources
List<LivenessResourceResponse> livenessResources = resources.LivenessCapture;

foreach (LivenessResourceResponse liveness in livenessResources)
{
    // Get the liveness id
    string livenessId = liveness.Id;

    // Get the liveness type
    string livenessType = liveness.Type;
}
{% /tab %}
{% tab language="go" %}
// Returns the liveness resources
livenessResources = resources.LivenessCapture

for _, liveness := range livenessResources {
    // Get the liveness id
    livenessId := liveness.ID

    // Get the liveness type
    livenessType := liveness.LivenessType
}
{% /tab %}
{% /code %}

#### Active liveness

{% code %}
{% tab language="javascript" %}
// Returns Active (Zoom) liveness resources
const zoomLivenessResources = resources.getZoomLivenessResources();

zoomLivenessResources.forEach((liveness) => {
  	// Get the liveness id
  	const livenessId = liveness.getId();
  
    // Get the liveness facemap
    const facemap = liveness.getFaceMap();

    // Get the liveness frames
    const frames = liveness.getFrames();
  
    frames.forEach((frame) => {
        // Get the frame media
        const frameMedia = frame.getMedia();

        // Get the frame media id
        const frameMediaId = frameMedia.getId();
    });
});
{% /tab %}
{% tab language="java" %}
// Returns Active (Zoom) liveness resources
List<? extends ZoomLivenessResourceResponse> zoomLivenessResources = resources.getZoomLivenessResources();

for (ZoomLivenessResourceResponse liveness : zoomLivenessResources) {
  	// Get the liveness id
    String livenessId = liveness.getId();
  
    // Get the liveness facemap
    FaceMapResponse facemap = liveness.getFaceMap();
    
    // Get the liveness frames
    List<? extends FrameResponse> frames = liveness.getFrames();
  
    for (FrameResponse frame : frames) {
        // Get the frame media
      	MediaResponse frameMedia = frame.getMedia();

        // Get the frame media id
        String frameMediaId = frameMedia.getId();
  	}
}
{% /tab %}
{% tab language="php" %}
// Returns Active (Zoom) liveness resources
$zoomLivenessResources = $resources->getZoomLivenessResources();

foreach ($zoomLivenessResources as $liveness) {
    // Get the liveness id
    $livenessId = $liveness->getId();
  
  	// Get the liveness facemap
    $facemap = liveness.getFaceMap();

    // Get the liveness frames
    $frames = liveness.getFrames();
  
    foreach ($frames as $frame) {
        // Get the frame media
        $frameMedia = $frame->getMedia();

        // Get the frame media id
        $frameMediaId = $frameMedia->getId();
  	});
});
{% /tab %}
{% tab language="python" %}
# Returns Active (Zoom) liveness resources
zoom_liveness_resources = resources.zoom_liveness_resources

for liveness in zoom_liveness_resources:
    # Get the liveness id
    liveness_id = liveness.id

    # Get the liveness facemap
    facemap = liveness.facemap
    
    # Get the liveness frames
    frames = liveness.frames
    
    for frame in frames:
        # Get the frame media
        frame_media = frame.media

        # Get the frame media id
        frame_media_id = frame_media.id
{% /tab %}
{% tab language="csharp" %}
// Returns Active (Zoom) liveness resources
List<ZoomLivenessResourceResponse> zoomLivenessResources = resources.ZoomLivenessResources;

foreach (ZoomLivenessResourceResponse liveness in zoomLivenessResources)
{
    // Get the liveness id
    string livenessId = liveness.Id;

  	// Get the liveness facemap
    FaceMapResponse facemap = liveness.FaceMap;
    
    // Get the liveness frames
    List<FrameResponse> frames = liveness.Frames;
  
    foreach (ZoomLivenessResourceResponse liveness in zoomLivenessResources)
    {
       // Get the frame media
      	MediaResponse frameMedia = frame.Media;

        // Get the frame media id
        String frameMediaId = frameMedia.Id;
    }
}
{% /tab %}
{% tab language="go" %}
// Returns Active (Zoom) liveness resources
zoomLivenessResources = resources.zoomLivenessResources

for _, liveness := range zoomLivenessResources {
    // Get the liveness id
    livenessId := liveness.ID

    // Get the liveness facemap
    facemap := liveness.FaceMap

    // Get the liveness frames
    frames := liveness.Frames

    for _, frame := range frames {
        // Get the frame media
        frameMedia := frame.Media

        // Get the frame media id
        frameMediaId := frameMedia.ID
    }
}
{% /tab %}
{% /code %}

#### Passive liveness

{% code %}
{% tab language="javascript" %}
// Returns Passive (Static) liveness resources
const staticLivenessResources = resources.getStaticLivenessResources();

staticLivenessResources.forEach((liveness) => {
  	// Get the liveness id
    const livenessId = liveness.getId();
  
  	// Get the liveness image media
    const livenessMedia = liveness.getImage();

    // Get the liveness media id
    const livenessMediaId = livenessMedia.getId();
});
{% /tab %}
{% tab language="java" %}
// Returns Passive (Static) liveness resources
List<? extends StaticLivenessResourceResponse> staticLivenessResources = resources.getLivenessCapture();

for (StaticLivenessResourceResponse liveness : staticLivenessResources) {
  	// Get the liveness id
    String livenessId = liveness.getId();
  
  	// Get the liveness image media
    MediaResponse livenessMedia = liveness.getImage().getMedia();

    // Get the liveness media id
    const livenessMediaId = livenessMedia.getId(); 
}
{% /tab %}
{% tab language="php" %}
// Returns Passive (Static) liveness resources
$staticLivenessResources = $resources->getStaticLivenessResources();

foreach ($staticLivenessResources as $liveness) {
    // Get the liveness id
    $livenessId = $liveness->getId();
  
  	// Get the liveness image media
    $livenessMedia = $liveness.getImage();

    // Get the liveness media id
    $livenessMediaId = $livenessMedia.getId();
});
{% /tab %}
{% tab language="python" %}
# For each oject in liveness resources
for liveness in liveness_resources:
    # Get the liveness id
    liveness_id = liveness.id

    # Get the liveness type
    liveness_type = liveness.type
    
    # Check if the liveness type is "STATIC"
    if liveness_type == "STATIC":
        # Get the liveness image media
        liveness_media = getattr(getattr(liveness, "image", None), "media", {})

        # Get the media id
        liveness_media_id = liveness_media.get("id", None)
{% /tab %}
{% tab language="csharp" %}
// Returns Passive (Static) liveness resources
List<StaticLivenessResourceResponse> staticLivenessResources = resources.StaticLivenessResourceResponse;

foreach (StaticLivenessResourceResponse liveness in staticLivenessResources)
    {
      // Get the liveness id
      String livenessId = liveness.Id;

      // Get the liveness image media
      MediaResponse livenessMedia = liveness.image.Media;

      // Get the liveness media id
      String livenessMediaId = livenessMedia.Id; 
    }
{% /tab %}
{% tab language="go" %}
// Returns Passive (Static) liveness resources
staticLivenessResources = resources.staticLivenessResources

for _, liveness := range staticLivenessResources {
    // Get the liveness id
    livenessId := liveness.ID

    // Get the liveness image media
    livenessMedia := livenessImage.Image.Media

    // Get the liveness media id
    livenessMediaId := livenessMedia.ID
}
{% /tab %}
{% /code %}