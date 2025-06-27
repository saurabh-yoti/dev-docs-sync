---
type: page
title: Face Comparison
listed: true
slug: face-comparison
description: 
index_title: Face Comparison
hidden: 
keywords: 
tags: 
---

{% callout type="info" title="Good to know" %}
Face Comparison can be requested along with other checks (i.e. Document authenticity, Face match etc.) or as a standalone check.
{% /callout %}

The Identity Verification (IDV) service also provides a face comparison check that can be used to authenticate a user by using their selfie. This check does an AI comparison between a live user selfie and the reference facial image to return a confidence score. Combined with a liveness check, this can be used for selfie authentication.

## Configure selfie auth

Before triggering the selfie auth check, you have to create an IDV session configured with Face comparison and Liveness check. Additionally, a reference face image has to be uploaded against which the live selfie will be compared.

### Session specification

To use this service, you have to create session specification with at least two checks - Liveness and Face Comparison. You can also set the maximum retries for liveness and manual check option for face comparison checks. Currently, only an automated face comparison is available.

{% code %}
{% tab language="javascript" title="Node.js" %}
const {
    SessionSpecificationBuilder,
    RequestedLivenessCheckBuilder,
    RequestedFaceComparisonCheckBuilder,
    SdkConfigBuilder
} = require('yoti');

// Liveness check with 3 retries
const livenessCheck = new RequestedLivenessCheckBuilder()
    .forStaticLiveness()
    .withMaxRetries(3)
    .build();

// Face Comparison check with manual check set to never
const faceComparisonCheck = new RequestedFaceComparisonCheckBuilder()
    .withManualCheckNever()
    .build();

// Configuration for the client SDK (Frontend)
const sdkConfig = new SdkConfigBuilder()
    .withSuccessUrl('/success')
    .withErrorUrl('/error')
		.withAllowHandoff(true)
    .build();

// Buiding the Session with defined specification from above
const sessionSpec = new SessionSpecificationBuilder()
    .withClientSessionTokenTtl(600)
    .withResourcesTtl(90000) 
    .withUserTrackingId('some-user-tracking-id')
    .withRequestedCheck(livenessCheck)
    .withRequestedCheck(faceComparisonCheck)
    .withSdkConfig(sdkConfig)
    .build();
{% /tab %}
{% tab language="java" %}
import com.yoti.api.client.docs.session.create.check.RequestedLivenessCheck;
import com.yoti.api.client.docs.session.create.check.RequestedFaceComparisonCheck;
import com.yoti.api.client.docs.session.create.SdkConfig;
import com.yoti.api.client.docs.session.create.SessionSpec;

...
SessionSpec sessionSpec = SessionSpec.builder()
    .withClientSessionTokenTtl(600)
    .withResourcesTtl(90000)
    .withUserTrackingId("some-user-tracking-id")
    .withRequestedCheck(
        RequestedLivenessCheck.builder()
            .forStaticLiveness()
            .withMaxRetries(3)
            .build()
  	)
    .withRequestedCheck(
        RequestedFaceComparisonCheck.builder()
        		.withManualCheckNever()
            .build()
  	)
    .withSdkConfig(
        SdkConfig.builder()
            .withSuccessUrl("https://localhost:8443/success")
            .withErrorUrl("https://localhost:8443/error")
            .withAllowHandoff(true)
            .build();
		)
    .build();
...
{% /tab %}
{% tab language="php" %}
use Yoti\DocScan\Session\Create\Check\RequestedLivenessCheckBuilder;
use Yoti\DocScan\Session\Create\Check\RequestedFaceComparisonCheckBuilder;
use Yoti\DocScan\Session\Create\SdkConfigBuilder;
use Yoti\DocScan\Session\Create\SessionSpecificationBuilder;

$sessionSpec = (new SessionSpecificationBuilder())
    ->withClientSessionTokenTtl(600)
    ->withResourcesTtl(90000)
    ->withUserTrackingId('some-user-tracking-id')
    ->withRequestedCheck(
        (new RequestedLivenessCheckBuilder())
            ->forLivenessType('Static')
            ->withMaxRetries(3)
            ->build()
    )
    ->withRequestedCheck(
        (new RequestedFaceComparisonCheckBuilder())
            ->withManualCheckNever()
            ->build()
    )
    ->withSdkConfig(
        (new SdkConfigBuilder())
            ->withSuccessUrl(config('app.url') . '/success')
            ->withErrorUrl(config('app.url') . '/error')
            ->withAllowHandoff(true)
            ->build()
    )
    ->build();
{% /tab %}
{% tab language="python" %}
# Coming Soon
{% /tab %}
{% tab language="csharp" %}
using Yoti.Auth;
using Yoti.Auth.DocScan;
using Yoti.Auth.DocScan.Session.Create;
using Yoti.Auth.DocScan.Session.Create.Check;

...
var sessionSpec = new SessionSpecificationBuilder()
    .WithClientSessionTokenTtl(600)
    .WithResourcesTtl(90000)
    .WithUserTrackingId("some-user-tracking-id")
    .WithRequestedCheck(
        new RequestedLivenessCheckBuilder()
        .ForStaticLiveness()
        .Build()
    )
    .WithRequestedCheck(
        new RequestedFaceComparisonCheckBuilder()
        .WithManualCheckNever()
        .Build()
    )
    .WithSdkConfig(
        new SdkConfigBuilder()
        .WithSuccessUrl(Path.Combine("/success"))
        .WithErrorUrl(Path.Combine("/error"))
        .WithAllowHandoff(true)
        .Build()
    )
    .Build();
...
{% /tab %}
{% tab language="go" %}
package main

import (
    "os"
    "github.com/getyoti/yoti-go-sdk/v3/docscan"
    "github.com/getyoti/yoti-go-sdk/v3/docscan/session/create"
    "github.com/getyoti/yoti-go-sdk/v3/docscan/session/create/check"
)

func buildSessionSpec() (sessionSpec *create.SessionSpecification, err error) {

    var livenessCheck *check.RequestedLivenessCheck
    livenessCheck, err = check.NewRequestedLivenessCheckBuilder().
        ForStaticLiveness().
        WithMaxRetries(3).
        Build()
    if err != nil {
        panic(err)
    }

    var faceComparisonCheck *check.RequestedFaceComparisonCheck
    faceComparisonCheck, err = check.NewRequestedFaceComparisonCheckBuilder().
        WithManualCheckNever().
        Build()
    if err != nil {
        panic(err)
    }

    var sdkConfig *create.SDKConfig
    sdkConfig, err = create.NewSdkConfigBuilder().
        WithSuccessUrl("https://localhost:8080/success").
        WithErrorUrl("https://localhost:8080/error").
        WithAllowHandOff(true).
        Build()
    if err != nil {
          panic(err)
    }

    var sessionSpec *create.SessionSpecification
    sessionSpec, err = create.NewSessionSpecificationBuilder().
        WithClientSessionTokenTTL(600).
        WithResourcesTTL(90000).
        WithUserTrackingID("some-tracking-id").
        WithRequestedCheck(faceComparisonCheck).
        WithRequestedCheck(livenessCheck).
        WithSDKConfig(sdkConfig).
        Build()
    if err != nil {
        panic(err)
    }
    return sessionSpec, nil
}
{% /tab %}
{% /code %}

### Initialise the Yoti client

The included DocScan/IDV Client includes several helper methods to interact with the Yoti's API. You can initialise the client using your unique SDK ID and PEM file.

{% code %}
{% tab language="javascript" title="Node.js" %}
const path = require('path');
const fs = require('fs');

const { IDVClient } = require('yoti');

const YOTI_CLIENT_SDK_ID = 'YOTI_CLIENT_SDK_ID';
const YOTI_PEM = fs.readFileSync(path.join(__dirname, '/path/to/pem'));

const idvClient = new IDVClient(YOTI_CLIENT_SDK_ID, YOTI_PEM);
{% /tab %}
{% tab language="java" %}
import com.yoti.api.client.ClassPathKeySource;
import com.yoti.api.client.docs.DocScanClient;
import com.yoti.api.client.docs.DocScanException;

...
DocScanClient docScanClient = DocScanClient.builder()
    .withClientSdkId("YOTI_CLIENT_SDK_ID")
    .withKeyPairSource(ClassPathKeySource.fromClasspath("/path/to/pem"))
    .build();
...
{% /tab %}
{% tab language="php" %}
use Yoti\DocScan\DocScanClient;

$YOTI_CLIENT_SDK_ID = 'YOTI_CLIENT_SDK_ID';
$YOTI_PEM = '/path/to/pem';

$client = new DocScanClient($YOTI_CLIENT_SDK_ID, $YOTI_PEM);
{% /tab %}
{% tab language="python" %}
# Coming Soon
{% /tab %}
{% tab language="csharp" %}
using System.IO;
using System.Net.Http;
using Yoti.Auth;
using Yoti.Auth.DocScan;

...
const string YOTI_CLIENT_SDK_ID = "YOTI_CLIENT_SDK_ID";
const string PEM_PATH = "/path/to/pem";

StreamReader privateKeyStream = System.IO.File.OpenText(PEM_PATH);
var key = CryptoEngine.LoadRsaKey(privateKeyStream);

var docScanClient = new DocScanClient(YOTI_CLIENT_SDK_ID, key, new HttpClient());
...
{% /tab %}
{% tab language="go" %}
package main

import (
    "os"

    "github.com/getyoti/yoti-go-sdk/v3/docscan"
    "github.com/getyoti/yoti-go-sdk/v3/docscan/session/create"
    "github.com/getyoti/yoti-go-sdk/v3/docscan/session/create/check"
)

var (
    sdkId               string
    key                 []byte
)

func main() {
    var err error

    sdkId = "YOTI_CLIENT_SDK_ID"
    key, err = os.ReadFile("/path/to/pem")
    if err != nil {
        panic(err)
    }

    var client *docscan.Client
    client, err = docscan.NewClient(sdkId, key)
    if err != nil {
        panic(err)
    }
}
{% /tab %}
{% /code %}

### Create a session

You can use the createSession method from the above client to create a Yoti session. Session specification needs to be passed as an argument. After the session is successfully created, you will get a Session ID that can be used to retrieve the Session configuration.

{% code %}
{% tab language="javascript" title="Node.js" %}
let sessionId, sessionToken;

idvClient
    .createSession(sessionSpec)
    .then((session) => {
        sessionId = session.getSessionId();
        sessionToken = session.getClientSessionToken();
    })
    .catch((err) => {
        console.log(err)
    });

const sessionConfig = await idvClient.getSessionConfiguration(sessionId);
{% /tab %}
{% tab language="java" %}
import com.yoti.api.client.docs.session.create.CreateSessionResult;
import com.yoti.api.client.docs.session.retrieve.configuration.SessionConfigurationResponse;

...
CreateSessionResult session = docScanClient.createSession(sessionSpec);

String sessionId = session.getSessionId();
String sessionToken = session.getClientSessionToken();

SessionConfigurationResponse sessionConfig = docScanClient.getSessionConfiguration(sessionId);
...
{% /tab %}
{% tab language="php" %}
$session = $client->createSession($sessionSpec);

$sessionId = $session->getSessionId();
$sessionToken = $session->getClientSessionToken();

$sessionConfig = $client->getSessionConfiguration($sessionId);
{% /tab %}
{% tab language="python" %}
# Coming Soon
{% /tab %}
{% tab language="csharp" %}
using Yoti.Auth.DocScan.Session.Retrieve.Configuration

...
CreateSessionResult session = docScanClient.CreateSession(sessionSpec);

string sessionId = session.SessionId;
string sessionToken = session.ClientSessionToken

SessionConfigurationResponse sessionConfig = docScanClient.GetSessionConfiguration(sessionId);
...
{% /tab %}
{% tab language="go" %}
var createSessionResult *create.SessionResult
    createSessionResult, err = client.CreateSession(sessionSpec)
    if err != nil {
        panic(err)
    }

    sessionId := createSessionResult.SessionID
    clientSessionToken := createSessionResult.ClientSessionToken
    
    sessionConfig, err := client.GetSessionConfiguration(sessionId)
    if err != nil {
        panic(err)
    }
{% /tab %}
{% /code %}

### Create a Face Capture resource

Before uploading the reference face image, you have to create a Face capture resource. To do this, a Requirement ID from the Face Capture requirements needs to retrieved. This can then be used to create a face capture resource. If successful, you will receive a Resource Id.

{% code %}
{% tab language="javascript" title="Node.js" %}
const {
  CreateFaceCaptureResourcePayloadBuilder,
  UploadFaceCaptureImagePayloadBuilder,
} = require('yoti');

const resourceRequirements = sessionConfiguration.getCapture().getFaceCaptureResourceRequirements()[0];
const requirementId = resourceRequirements.getId();

const faceCapturePayload = new CreateFaceCaptureResourcePayloadBuilder()
    .withRequirementId(requirementId)
    .build();

const faceCaptureResource = await idvClient.createFaceCaptureResource(sessionId, faceCapturePayload);
const resourceId = faceCaptureResource.getId();
{% /tab %}
{% tab language="java" %}
import com.yoti.api.client.docs.session.retrieve.configuration.SessionConfigurationResponse;
import com.yoti.api.client.docs.session.retrieve.configuration.capture;
import com.yoti.api.client.docs.session.retrieve.configuration.capture.facecapture;

import com.yoti.api.client.docs.session.create.facecapture.CreateFaceCaptureResourcePayload;
import com.yoti.api.client.docs.session.retrieve.CreateFaceCaptureResourceResponse;

...
RequiredFaceCaptureResourceResponse resourceRequirements = sessionConfig.getCapture().getFaceCaptureResourceRequirements().get(0);
String requirementId = resourceRequirements.getId();

CreateFaceCaptureResourcePayload faceCapturePayload = CreateFaceCaptureResourcePayload.builder()
    .withRequirementId(requirementId)
    .build();

CreateFaceCaptureResourceResponse faceCaptureResource = docScanClient.createFaceCaptureResource(sessionId, faceCapturePayload);
String resourceId = faceCaptureResource.getId();
...
{% /tab %}
{% tab language="php" %}
use Yoti\DocScan\Session\Retrieve\Configuration;
use Yoti\DocScan\Session\Retrieve\Configuration\Capture;
use Yoti\DocScan\Session\Retrieve\Configuration\Capture\CaptureResponse;

use Yoti\DocScan\Session\Create\FaceCapture;
use Yoti\DocScan\Session\Create\FaceCapture\CreateFaceCaptureResourcePayloadBuilder;
use Yoti\DocScan\Session\Retrieve\CreateFaceCaptureResourceResponse;

$resourceRequirements = $sessionConfig->getCapture()->getFaceCaptureResourceRequirements()[0];
$requirementId = $resourceRequirements->getId();

$faceCapturePayload = (new CreateFaceCaptureResourcePayloadBuilder())
  ->withRequirementId($requirementId)
  ->build();

$faceCaptureResource = $client->createFaceCaptureResource($sessionId, $faceCapturePayload);
$resourceId = $faceCaptureResource->getId();
{% /tab %}
{% tab language="python" %}
# Coming Soon
{% /tab %}
{% tab language="csharp" %}
using Yoti.Auth.DocScan.Session.Create.FaceCapture
using Yoti.Auth.DocScan.Session.Create.FaceCapture.CreateFaceCaptureResourcePayloadBuilder
using Yoti.Auth.DocScan.Session.Retrieve.Configuration.Capture

...
RequiredFaceCaptureResourceResponse resourceRequirements = sessionConfiguration.Capture.GetFaceCaptureResourceRequirements()[0];
string requirementId = resourceRequirements.Id;

CreateFaceCaptureResourcePayload faceCapturePayload = new CreateFaceCaptureResourcePayloadBuilder()
    .WithRequirementId(requirementId)
    .Build();

CreateFaceCaptureResourceResponse faceCaptureResource = docScanClient.CreateFaceCaptureResource(sessionId, faceCapturePayload);
string resourceId = faceCaptureResource.Id;
...
{% /tab %}
{% tab language="go" %}
import (
    "os"

    "github.com/getyoti/yoti-go-sdk/v3/docscan"
    "github.com/getyoti/yoti-go-sdk/v3/docscan/session/create"
    "github.com/getyoti/yoti-go-sdk/v3/docscan/session/create/facecapture"
)

func main() {
    var err error

    resourceRequirements := sessionConfig.GetCapture().GetFaceCaptureResourceRequirements()[0]
    requirementId := resourceRequirements.GetID()

    faceCapturePayload := facecapture.NewCreateFaceCaptureResourcePayload(requirementId)
 
    faceCaptureResource, err := client.CreateFaceCaptureResource(sessionId, faceCapturePayload)
    if err != nil {
        panic(err)
    }

    resourceId := faceCaptureResource.GetID()
    _ = resourceId // Use resourceId as needed
}
{% /tab %}
{% /code %}

### Upload a reference image

To do accurate face comparison, a reference facial image of the user is required. You have to get the contents of this image which can then be uploaded using the Doc Scan Client. You also have to pass in the Resource Id retrieved earlier

{% code %}
{% tab language="javascript" title="Node.js" %}
const fs = require('fs');

const imageBuffer = fs.readFileSync('path-to-selfie-jpeg');

const faceCaptureImagePayload = new UploadFaceCaptureImagePayloadBuilder()
    .forJpegImage()
    .withImageContents(imageBuffer)
    .build();

await idvClient.uploadFaceCaptureImage(sessionId, resourceId, faceCaptureImagePayload);
{% /tab %}
{% tab language="java" %}
import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.ByteArrayOutputStream;
import com.yoti.api.client.docs.session.create.facecapture.UploadFaceCaptureImagePayload;

...
BufferedImage imageBuffer = ImageIO.read(new File("path-to-selfie-jpeg"));
ByteArrayOutputStream bos = new ByteArrayOutputStream();
ImageIO.write(bImage, "jpg", bos);
byte[] data = bos.toByteArray();

UploadFaceCaptureImagePayload faceCaptureImagePayload = UploadFaceCaptureImagePayload.builder()
    .forJpegImage()
  	.withImageContents(data)
    .build();

docScanClient.uploadFaceCaptureImage(sessionId, resourceId, faceCaptureImagePayload);
...
{% /tab %}
{% tab language="php" %}
use Yoti\Media\Image\Jpeg;
use Yoti\DocScan\Session\Create\FaceCapture\UploadFaceCaptureImagePayloadBuilder;

$imageData = file_get_contents('path-to-selfie-jpeg');

$faceCaptureImagePayload = (new UploadFaceCaptureImagePayloadBuilder())
  ->forJpegImage()
  ->withImageContents($imageData)
  ->build();

$client->uploadFaceCaptureImage($sessionId, $resourceId, $faceCaptureImagePayload);
{% /tab %}
{% tab language="python" %}
# Coming Soon
{% /tab %}
{% tab language="csharp" %}
using System.IO;
using Yoti.Auth.DocScan.Session.Create.FaceCapture
using Yoti.Auth.DocScan.Session.Create.FaceCapture.UploadFaceCaptureImagePayloadBuilder

...
string imagePath = "path-to-selfie-jpeg";
byte[] imageData = File.ReadAllBytes(imagePath);

UploadFaceCaptureImagePayload faceCaptureImagePayload = new UploadFaceCaptureImagePayloadBuilder()
    .ForJpegImage()
    .WithImageContents(imageData)
    .Build();

docScanClient.UploadFaceCaptureImage(sessionId, resourceId, faceCaptureImagePayload);
...
{% /tab %}
{% tab language="go" %}
import (
		"encoding/base64"
    "os"

    "github.com/getyoti/yoti-go-sdk/v3/docscan/session/create/facecapture"
)

func main() {
   imgBytes, err := os.ReadFile("face.png")
    if err != nil {
        panic(err)
    }
    base64Str := base64.StdEncoding.EncodeToString(imgBytes)
    }

	addResource := client.AddFaceCaptureResourceToSession(sessionId, base64Str)
{% /tab %}
{% /code %}

---

## Client-side view

The next step is to load the Yoti client-side SDK. To do this, you need the below parameters generated with the session creation request above:

- Session ID
- Session Token

We then utilise these to construct a Web URL which loads the Yoti Client SDK. The URL is in the following format:

{% code %}
{% tab language="yaml" title="HTTP" %}
https://api.yoti.com/idverify/v1/web/index.html?sessionID=<sessionID>&sessionToken=<sessionToken>
{% /tab %}
{% /code %}

Once the above URL launches in a web browser, it will take the user through the Selfie and liveness capture flow. For more detailed steps, please refer to the [auto$](/identity-verification/render-the-user-view) page.

---

## Retrieve results

Once a session has been completed, the associated checks' results and resources can be retrieved using the session ID. Each check would contain a recommendation and a breakdown. The resources however are not directly included in the results, but contain a media ID. This can be used to fetch the actual media resource.

The liveness part of the process may contain multiple checks, as a liveness check is generated for each allowed retry. For a face comparison to be considered a 'PASS' overall, the recommended action is to confirm that at least one Liveness check is 'Approve' and the Face Comparison check is 'Approve'.

### Retrieve checks

{% code %}
{% tab language="javascript" title="Node.js" %}
idvClient.getSession(sessionId).then(sessionResult => {
    const state = sessionResult.getState();
  
  	const livenessChecks = sessionResult.getLivenessChecks();
  
  	livenessChecks.map(check => {
        const id = check.getId();
        const state = check.getState();
        const resourcesUsed = check.getResourcesUsed();

        const report = check.getReport();
        const recommendation = report.getRecommendation().getValue();
        const breakdown = report.getBreakdown();
      
      	breakdown.forEach(function(breakdown) {
          const subCheck = breakdown.getSubCheck();
          const subCheckResult = breakdown.getResult();
        });
    })
  
    const faceComparisonChecks = sessionResult.getFaceComparisonChecks();
  
  	faceComparisonChecks.map(check => {
        const id = check.getId();
        const state = check.getState();
        const resourcesUsed = check.getResourcesUsed();
      
        const report = check.getReport();
        const recommendation = report.getRecommendation().getValue();
        const breakdown = report.getBreakdown();
      
      	breakdown.forEach(function(breakdown) {
          const subCheck = breakdown.getSubCheck();
          const subCheckResult = breakdown.getResult();
        });
    })
}).catch(error => {
   	console.log(error);
    // handle error
})
{% /tab %}
{% tab language="java" %}
GetSessionResult sessionResult = docScanClient.getSession(sessionId);
String state = sessionResult.getState();

List<? extends CheckResponse> livenessChecks = sessionResult.getLivenessChecks();

for (CheckResponse check: livenessChecks) {
    String id = check.getId();
    String state = check.getState();
    List<String> resourcesUsed = check.getResourcesUsed();

    ReportResponse report = check.getReport();
    String recommendation = report.getRecommendation().getValue();
    List<? extends BreakdownResponse> breakdown = report.getBreakdown();
  
  	for (BreakdownResponse breakdown: breakdown) {
        String subCheck = breakdown.getSubCheck();
        String subCheckResult = breakdown.getResult();
    }
}

List<? extends CheckResponse> faceComparisonChecks = sessionResult.getFaceComparisonChecks();

for (CheckResponse check: faceComparisonChecks) {
    String id = check.getId();
    String state = check.getState();
    List<String> resourcesUsed = check.getResourcesUsed();

    ReportResponse report = check.getReport();
    String recommendationValue = report.getRecommendation().getValue();
    List<? extends BreakdownResponse> breakdown = report.getBreakdown();
  
  	for (BreakdownResponse breakdown: breakdown) {
        String subCheck = breakdown.getSubCheck();
        String subCheckResult = breakdown.getResult();
    }
}
{% /tab %}
{% tab language="php" %}
$sessionResult = $docScanClient->getSession($sessionId);
$state = $sessionResult->getState();

$livenessChecks = $sessionResult->getLivenessChecks();

foreach($livenessChecks as $check) {
    $id = $check->getId();
    $state = $check->getState();
    $resourcesUsed = $check->getResourcesUsed();

    $report = $check->getReport();
    $recommendation = $report->getRecommendation()->getValue();
    $breakdown = $report->getBreakdown();
  
  	foreach($breakdown as $breakdown) {
        $subCheck = $breakdown->getSubCheck();
        $subCheckResult = $breakdown->getResult();
    }
}

$faceComparisonChecks = $sessionResult->getFaceComparisonChecks();

foreach($faceComparisonChecks as $check) {
    $id = $check->getId();
    $state = $check->getState();
    $resourcesUsed = $check->getResourcesUsed();

    $report = $check->getReport();
    $recommendation = $report->getRecommendation()->getValue();
    $breakdown = $report->getBreakdown();
  
  	foreach($breakdown as $breakdown) {
        $subCheck = $breakdown->getSubCheck();
        $subCheckResult = $breakdown->getResult();
    }
}
{% /tab %}
{% tab language="python" %}
# Coming Soon
{% /tab %}
{% tab language="csharp" %}
GetSessionResult sessionResult = docScanClient.GetSession(sessionId);
string state = sessionResult.State;

List<CheckResponse> livenessChecks = sessionResult.GetLivenessChecks();

foreach (CheckResponse check in livenessChecks)
{
    string id = check.Id;
    string state = check.State;
    List<String> resourcesUsed = check.ResourcesUsed;

    ReportResponse report = check.Report;
    string recommendation = report.Recommendation.Value;
    List<BreakdownResponse> breakdown = report.Breakdown;
  
    foreach (BreakdownResponse breakdown in breakdown)
    {
        string subCheck = breakdown.SubCheck;
        string subCheckResult = breakdown.Result;
    }
}
{% /tab %}
{% tab language="go" %}
var sessionResults *retrieve.GetSessionResult
sessionResults, err = client.GetSession(sessionId)
if err != nil {
    panic(err)
    }

state := sessionResults.State

livenessChecks := sessionResults.LivenessChecks()
for _, check := range livenessChecks {
    id := check.GetID()
    state := check.GetState()
    resourcesUsed := check.GetResourcesUsed()

    report := check.GetReport()
    recommendation := report.GetRecommendation().GetValue()
    breakdown := report.GetBreakdown()

    for _, breakdown := range breakdown {
        subCheck := breakdown.GetSubCheck()
        subCheckResult := breakdown.GetResult()
    }
}

faceComparisonChecks := sessionResults.FaceComparisonChecks()
for _, check := range faceComparisonChecks {
    id := check.GetID()
    state := check.GetState()
    resourcesUsed := check.GetResourcesUsed()

    report := check.GetReport()
    recommendation := report.GetRecommendation().GetValue()
    breakdown := report.GetBreakdown()

    for _, breakdown := range breakdown {
        subCheck := breakdown.GetSubCheck()
        subCheckResult := breakdown.GetResult()
    }
}
{% /tab %}
{% /code %}

### Retrieve resources

{% code %}
{% tab language="javascript" title="Node.js" %}
idvClient.getSession(sessionId).then(sessionResult => {
    const resources = sessionResult.getResources();
  
  	const faceCaptureResources = resources.getFaceCaptureResources();
  
  	const staticLivenessResources = resources.getStaticLivenessResources();
  
  	staticLivenessResources.map(resource => {
        const id = resource.getId();m
        const type = resource.getLivenessType();
        const mediaId = check.getImage().getId();
    })
}).catch(error => {
   	console.log(error);
    // handle error
})
{% /tab %}
{% tab language="java" %}
GetSessionResult sessionResult = docScanClient.getSession(sessionId);
ResourceContainer resources = sessionResult.getResources();

List<? extends FaceCaptureResourceResponse> faceCaptureResources = resources.getFaceCapture();

List<? extends StaticLivenessResourceResponse> staticLivenessResources = resources.getStaticLivenessResources();

for (StaticLivenessResourceResponse resource: staticLivenessResources) {
    String id = resource.getId();
    String type = resource.getLivenessType();
    String mediaId = resource.getImage().getMedia().getId();
}
{% /tab %}
{% tab language="php" %}
$sessionResult = $docScanClient->getSession($sessionId);
$resources = $sessionResult->getResources();

$faceCaptureResources = $resources->getFaceCapture();

$staticLivenessResources = $resources->getStaticLivenessResources();

foreach ($staticLivenessResources as $resource) {
    $id = $resource->getId();
    $type = $resource->getLivenessType();
    $mediaId = $resource->getImage()->getId();
}
{% /tab %}
{% tab language="python" %}
# Coming Soon
{% /tab %}
{% tab language="csharp" %}
GetSessionResult sessionResult = docScanClient.GetSession(sessionId);
ResourceContainer resources = sessionResult.Resources;

List<FaceCaptureResourceResponse> faceCaptureResources = resources.FaceCapture;

List<StaticLivenessResourceResponse> staticLivenessResources = resources.StaticLivenessResources;

foreach (StaticLivenessResourceResponse resource in staticLivenessResources)
{
    string id = resource.Id;
    string type = resource.LivenessType;
    string mediaId = resource.image.Media.Id;
}
{% /tab %}
{% tab language="go" %}
resources := sessionResults.GetResources()
faceCaptureResources := resources.GetFaceCaptureResources()
staticLivenessResources := resources.GetStaticLivenessResources()

for _, resource := range staticLivenessResources {
    id := resource.GetID()
    livenessType := resource.GetLivenessType()
    mediaId := resource.GetImage().GetID()
}
{% /tab %}
{% /code %}

### Retrieve media

{% code %}
{% tab language="javascript" title="Node.js" %}
idvClient.getMediaContent(sessionId, mediaId).then(media => {
    const buffer = media.getContent();
  	const mimeType = media.getMimeType();
    const base64Content = media.getBase64Content();
    // handle base64content or buffer
}).catch(error => {
    console.log(error)
    // handle error
})
{% /tab %}
{% tab language="java" %}
Media media = docScanClient.getMediaContent(sessionId, mediaId);
{% /tab %}
{% tab language="php" %}
$media = $docScanClient->getMediaContent($sessionId, $mediaId);
$mimeType = $media->getMimeType();
$base64Content = $media->getBase64Content();
{% /tab %}
{% tab language="python" %}
# Coming Soon
{% /tab %}
{% tab language="csharp" %}
MediaValue media = docScanClient.GetMediaContent(sessionId, pageMediaId);
string mimeType = media->GetMIMEType();
string base64Content = $media->GetBase64URI();
{% /tab %}
{% tab language="go" %}
media, err := client.GetMediaContent(sessionId, mediaID)
if err != nil {
    panic(err)
    }

mimeType := media.MIME()
content := media.Data()
base64URL := media.Base64URL()
{% /tab %}
{% /code %}