---
type: page
title: Face Comparison Old
listed: false
slug: face-comparison-old
description: 
index_title: Face Comparison Old
hidden: 
keywords: 
tags: 
---

The Identity Verification (IDV) service also provides a face comparison check that can be used to authenticate a user by using their selfie. This check does a AI comparison between live user selfie and the reference face image to return a confidence score.

## Session specification

To use the Face comparison service, you have to create session specification with at least two checks - Liveness and Face Comparison. You can also set the maximum retries for liveness and manual check option for face comparison checks.

{% code %}
{% tab language="javascript" %}
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
		.withAllowsCameraAndUpload()
		.withLocale("en-GB")
    .withPresetIssuingCountry('GBR')
    .withSuccessUrl('/success')
    .withErrorUrl('/error')
    .withPrivacyPolicyUrl('/privacy-policy')
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
            .withAllowsCameraAndUpload()
            .withLocale("en-GB")
            .withPresetIssuingCountry("GBR")
            .withSuccessUrl("https://localhost:8443/success")
            .withErrorUrl("https://localhost:8443/error")
            .withPrivacyPolicyUrl("https://localhost:8443/privacy-policy")
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
            ->withAllowsCameraAndUpload()
            ->withLocale('en-GB')
            ->withPresetIssuingCountry('GBR')
            ->withSuccessUrl(config('app.url') . '/success')
            ->withErrorUrl(config('app.url') . '/error')
            ->withPrivacyPolicyUrl(config('app.url') . '/privacy-policy')
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
        .WithAllowsCameraAndUpload()
        .WithLocale("en-GB")
        .WithPresetIssuingCountry("GBR")
        .WithSuccessUrl(Path.Combine("/success"))
        .WithErrorUrl(Path.Combine("/error"))
        .PrivacyPolicyUrl(Path.Combine("/privacy-policy"))
        .WithAllowHandoff(true)
        .Build()
    )
    .Build();
...
{% /tab %}
{% tab language="go" %}
// Coming soon
{% /tab %}
{% /code %}

## Initialise the Yoti client

The included DocScan/IDV Client includes several helper methods to interact with the Yoti's API. You can initialise the client using your unique SDK ID and PEM file.

{% code %}
{% tab language="javascript" %}
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
// Coming soon
{% /tab %}
{% /code %}

## Create a session

You can use the createSession method from the above client to create a Yoti session. Session specification needs to be passed as an argument. After the session is successfully created, you will get a Session ID that can be used to retrieve the Session configuration.

{% code %}
{% tab language="javascript" %}
let sessionId, clientSessionToken;

idvClient
    .createSession(sessionSpec)
    .then((session) => {
        sessionId = session.getSessionId();
        clientSessionToken = session.getClientSessionToken();
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
// Coming soon
{% /tab %}
{% /code %}

## Create a Face Capture resource

Before uploading the reference face image, you have to create a Face capture resource. To do this, a Requirement ID from the Face Capture requirements needs to retrieved. This can then be used to create a face capture resource. If successful, you will receive a Resource Id.

{% code %}
{% tab language="javascript" %}
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
// Coming soon
{% /tab %}
{% /code %}

## Upload a reference image

To do an accurate face comparison, a reference selfie image of the user is required. You have to get the contents of this image which can then be uploaded using the Doc Scan Client. You also have to pass in the Resource Id retrieved earlier.

{% code %}
{% tab language="javascript" %}
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
// Coming soon
{% /tab %}
{% /code %}