---
type: page
title: Face Comparison
listed: false
slug: face-comparison-api
description: 
index_title: Face Comparison RequestBuilder
hidden: 
keywords: 
tags: 
---

The Identity verification service also provides a face comparison check that can be used to authenticate a user by using their live selfie. This check does a AI comparison between the user selfie and the reference face image and returns a confidence score.

## Serialised payload

To use the Face comparison service, you have to create a serialised request with at least two checks - Liveness and Face Comparison. You can also set the maximum retries for liveness and manual check option for face comparison checks.

{% code %}
{% tab language="csharp" %}
string serializedRequest = JsonConvert.SerializeObject(new 
{
	client_session_token_ttl = 600,
  resources_ttl = 604800,
  user_tracking_id = "12345",
  requested_checks = new List<object> {
    new {
      type = "LIVENESS",
      config = new {
        liveness_type = "ZOOM",
        max_retries = 3
        }
    },
    new {
      type = "FACE_COMPARISON",
      config = new {
        manual_check = "NEVER"
        }
    }
  },
  requested_tasks = new List<object> {},
  required_documents = new List<object> {},
  sdk_config = new {
    allowed_capture_methods = "CAMERA_AND_UPLOAD",
    locale = "en-GB",
    preset_issuing_country = "GBR",
    success_url = $ "{_baseUrl}/success",
    error_url = $ "{_baseUrl}/error",
    privacy_policy_url = $ "{_baseUrl}/privacy",
    allow_handoff = false
    },
});
{% /tab %}
{% tab language="java" %}
String payloadString = "{ \"client_session_token_ttl\": 600, \"resources_ttl\": 604800, \"user_tracking_id\": \"12345\", \"requested_checks\": [ { \"type\": \"LIVENESS\", \"config\": { \"liveness_type\": \"ZOOM\", \"max_retries\": 3 } }, { \"type\": \"FACE_COMPARISON\", \"config\": { \"manual_check\": \"NEVER\" } } ], \"requested_tasks\": [], \"required_documents\": [], \"sdk_config\": { \"allowed_capture_methods\": \"CAMERA_AND_UPLOAD\", \"locale\": \"en-GB\", \"preset_issuing_country\": \"GBR\", \"success_url\": \"https://localhost:8443/success\", \"error_url\": \"https://localhost:8443/error\", \"privacy_policy_url\": \"https://localhost:8443/privacy\", \"allow_handoff\": false } }";
{% /tab %}
{% tab language="php" %}
$payload = (object)[
  'client_session_token_ttl' => '600',
  'resources_ttl' => '604800',
  'user_tracking_id' => '12345',
  'requested_checks' => [
    (object)[
      'type' => 'LIVENESS',
      'config' => (object)[
        'liveness_type' => 'STATIC',
        'max_retries' => '3',
      ],
    ],
    (object)[
      'type' => 'FACE_COMPARISON',
      'config' => (object)[
        'manual_check' => 'NEVER',
      ],
    ]
  ],
  'requested_tasks' => [],
  'required_documents' => [],
  'sdk_config' => (object)[
    'allowed_capture_methods' => 'CAMERA_AND_UPLOAD',
    'locale' => 'en-GB',
    'preset_issuing_country' => 'GBR',
    'success_url' => env('APP_URL') . '/success',
    'error_url' => env('APP_URL') . '/error',
    'privacy_policy_url' => env('APP_URL') . '/privacy',
    'allow_handoff' => 'false'
  ]
];
{% /tab %}
{% /code %}

## Create a session

You can use the RequestBuilder method from the corresponding SDK to create a session. You need to send the payload as part of the POST request. After the session is successfully created, you will get back a session result.

{% code %}
{% tab language="csharp" %}
using System;
using System.Net.Http;
using Newtonsoft.Json;
using Yoti.Auth.Web;
using Yoti.Auth.DocScan.Session.Create;

HttpClient _httpClient = new HttpClient();

byte[] body = Encoding.UTF8.GetBytes(serializedRequest);

Request createSessionRequest = new RequestBuilder()
	.WithKeyPair(keyPair)
  .WithHttpMethod(HttpMethod.Post)
  .WithBaseUri("https://api.yoti.com/idverify/v1")
  .WithEndpoint("/sessions")
  .WithQueryParam("sdkId", "<YOTI_CLIENT_SDK_ID>")
  .WithContent(body)
  .Build();

HttpResponseMessage response = await createSessionRequest.Execute(_httpClient).ConfigureAwait(false);

CreateSessionResult createSessionResult = JsonConvert.DeserializeObject<CreateSessionResult>(     response.Content.ReadAsStringAsync().Result);
{% /tab %}
{% tab language="java" %}
import com.yoti.api.client.spi.remote.call.YotiConstants;
import com.yoti.api.client.spi.remote.call.SignedRequest;
import com.yoti.api.client.spi.remote.call.SignedRequestBuilderFactory;
import com.yoti.api.client.docs.session.create.CreateSessionResult;

import static com.yoti.api.client.spi.remote.call.HttpMethod.HTTP_POST;
import static com.yoti.api.client.spi.remote.call.YotiConstants.CONTENT_TYPE;
import static com.yoti.api.client.spi.remote.call.YotiConstants.CONTENT_TYPE_JSON;

byte[] payload = payloadString.getBytes("UTF-8");

SignedRequest signedRequest = signedRequestBuilderFactory.create()
    .withKeyPair(keyPair)
    .withBaseUrl("https://api.yoti.com/idverify/v1")
    .withEndpoint("/sessions")
    .withQueryParameter("sdkId", sdkId)
    .withHttpMethod(HTTP_POST)
    .withPayload(payload)
    .withHeader(CONTENT_TYPE, CONTENT_TYPE_JSON)
    .build();

CreateSessionResult sessionResult = signedRequest.execute(CreateSessionResult.class);
{% /tab %}
{% tab language="php" %}
use Yoti\Constants;
use Yoti\Http\Payload;
use Yoti\Http\RequestBuilder;

use Yoti\Util\Env;
use Yoti\Util\Config;
use Yoti\Util\Json;
use Yoti\Util\PemFile;

$options[Config::API_URL] = $options[Config::API_URL] ?? Env::get(Constants::ENV_DOC_SCAN_API_URL);
$config = new Config($options);
$pemFile = PemFile::resolveFromString('/path-to-pem-file');

$response = (new RequestBuilder($config))
  ->withPemFile($pemFile)
  ->withBaseUrl('https://api.yoti.com/idverify/v1')
  ->withEndpoint('/sessions')
  ->withQueryParam('sdkId', $sdkId)
  ->withPayload(Payload::fromJsonData($payload))
  ->withHeader('Content-Type', 'application/json')
  ->withPost()
  ->build()
  ->execute();

$sessionResult = Json::decode((string)$response->getBody());
{% /tab %}
{% /code %}

## Initialise the Yoti client

The included DocScanClient includes several helper methods to interact with the Yoti's API. You can initialise the client using your unique SDK ID and PEM file.

{% code %}
{% tab language="csharp" %}
using System.IO;
using Org.BouncyCastle.Crypto;
using Yoti.Auth.DocScan;

internal static DocScanClient GetDocScanClient(Uri apiUrl = null) {
  if (apiUrl == null) { 
    apiUrl = GetApiUrl();
	}
  
  StreamReader privateKeyStream = System.IO.File.OpenText(Environment.GetEnvironmentVariable("YOTI_KEY_FILE_PATH"));
  var key = CryptoEngine.LoadRsaKey(privateKeyStream);
  string clientSdkId = Environment.GetEnvironmentVariable("YOTI_CLIENT_SDK_ID");

  return new DocScanClient(clientSdkId, key, new HttpClient(), apiUrl);
}

DocScanClient _client = GetDocScanClient("https://api.yoti.com/idverify/v1");
{% /tab %}
{% tab language="java" %}
import com.yoti.api.client.ClassPathKeySource;
import com.yoti.api.client.docs.DocScanClient;
import com.yoti.api.client.docs.DocScanException;

DocScanClient docScanClient = DocScanClient.builder()
    .withClientSdkId("YOTI_CLIENT_SDK_ID")
    .withKeyPairSource(ClassPathKeySource.fromClasspath("/path/to/pem"))
    .build();
{% /tab %}
{% tab language="php" %}
use Yoti\DocScan\DocScanClient;

$YOTI_CLIENT_SDK_ID = 'YOTI_CLIENT_SDK_ID';
$YOTI_PEM = '/path/to/pem';

$docScanClient = new DocScanClient($YOTI_CLIENT_SDK_ID, $YOTI_PEM);
{% /tab %}
{% /code %}

## Create a Face Capture resource

Session ID can be extracted from the session result retrieved earlier. This is used to fetch the session configuration. You will need a Requirement Id from the Face Capture requirements. This can then be used to create a face capture resource. If successfully, you will receive a Resource Id.

{% code %}
{% tab language="csharp" %}
using Yoti.Auth.DocScan.Session.Retrieve.Configuration;
using Yoti.Auth.DocScan.Session.Retrieve.Configuration.Capture.FaceCapture;
using Yoti.Auth.DocScan.Session.Create.FaceCapture;
using Yoti.Auth.DocScan.Session.Retrieve.CreateFaceCaptureResourceResponse;

string sessionId = createSessionResult.SessionId;

SessionConfigurationResponse sessionConfig = _client.GetSessionConfiguration(sessionId);
RequiredResourceResponse resourceResponse = sessionConfig.Capture.GetFaceCaptureResourceRequirements()[0];
string requirementId = resourceResponse.Id;

CreateFaceCaptureResourcePayload resourcePayload = new CreateFaceCaptureResourcePayloadBuilder()
  .WithRequirementId(requirementId)
  .Build(); 

CreateFaceCaptureResourceResponse resourceResponse = _client.CreateFaceCaptureResource(sessionId, createFaceCapturePayload);
string resourceId = resourceResponse.Id;
{% /tab %}
{% tab language="java" %}
import com.yoti.api.client.docs.session.retrieve.configuration.SessionConfigurationResponse;
import com.yoti.api.client.docs.session.create.facecapture.CreateFaceCaptureResourcePayload;
import com.yoti.api.client.docs.session.retrieve.CreateFaceCaptureResourceResponse;

String sessionId = sessionResult.getSessionId();

SessionConfigurationResponse sessionConfig = docScanClient.getSessionConfiguration(sessionId);
String requirementId = sessionConfig.getCapture().getFaceCaptureResourceRequirements().get(0).getId();

CreateFaceCaptureResourcePayload createFaceCaptureResourcePayload = CreateFaceCaptureResourcePayload.builder()
    .withRequirementId(requirementId)
    .build();

CreateFaceCaptureResourceResponse faceCaptureResource = docScanClient.createFaceCaptureResource(sessionId, createFaceCaptureResourcePayload);
String resourceId = faceCaptureResource.getId();
{% /tab %}
{% tab language="php" %}
use Yoti\DocScan\Session\Retrieve\Configuration;
use Yoti\DocScan\Session\Retrieve\Configuration\Capture;
use Yoti\DocScan\Session\Retrieve\Configuration\Capture\CaptureResponse;

use Yoti\DocScan\Session\Create\FaceCapture;
use Yoti\DocScan\Session\Retrieve\CreateFaceCaptureResourceResponse;

$sessionId = $sessionResult->getSessionId();

$sessionConfig = $docScanClient->getSessionConfiguration($sessionId);
$resourceRequirements = $sessionConfig->getCapture()->getFaceCaptureResourceRequirements()[0];
$requirementId = $resourceRequirements->getId();

$faceCapturePayload = (new CreateFaceCaptureResourcePayloadBuilder())
  ->withRequirementId($requirementId)
  ->build();

$faceCaptureResource = $docScanClient->createFaceCaptureResource($sessionId, $faceCapturePayload);
$resourceId = $faceCaptureResource->getId();
{% /tab %}
{% /code %}

## Uploading a reference image

To do an accurate face comparison, a reference selfie image of the user is required. You have to convert the image into a byte array which can then be uploaded using the Doc Scan Client. You also have to pass in the Resource Id.

{% code %}
{% tab language="csharp" %}
using SixLabors.ImageSharp;

public byte[] ImageToByteArray(Image image) {
  using (MemoryStream memoryStream = new MemoryStream()) {
    image.SaveAsJpeg(memoryStream);
    return memoryStream.ToArray();
  }
}

Image selfieImage = Image.Load("selfie.jpeg");
byte[] imageArray = ImageToByteArray(selfieImage);

UploadFaceCaptureImagePayload uploadFaceCapturePayload = new UploadFaceCaptureImagePayloadBuilder()
  .ForJpeg()
  .WithImageContents(imageArray)
  .Build();

_client.UploadFaceCaptureImage(sessionId, resourceId, uploadFaceCapturePayload);
{% /tab %}
{% tab language="java" %}
import java.awt.image.BufferedImage;
import javax.imageio.ImageIO;
import java.io.ByteArrayOutputStream;
import com.yoti.api.client.docs.session.create.facecapture.UploadFaceCaptureImagePayload;

BufferedImage bImage = ImageIO.read(new File("selfie.jpeg"));
ByteArrayOutputStream bos = new ByteArrayOutputStream();
ImageIO.write(bImage, "jpg", bos);
byte[] data = bos.toByteArray();

UploadFaceCaptureImagePayload result = UploadFaceCaptureImagePayload.builder()
    .withImageContents(data)
    .forJpegImage()
    .build();

docScanClient.uploadFaceCaptureImage(sessionId, resourceId, uploadFaceCaptureImagePayload);
{% /tab %}
{% tab language="php" %}
use Yoti\Media\Image\Jpeg;
use Yoti\DocScan\Session\Create\FaceCapture\UploadFaceCaptureImagePayloadBuilder;

$imageData = file_get_contents('selfie.jpeg');
$imageArray = unpack("C*", $imageData);

$uploadFaceCapturePayload = (new UploadFaceCaptureImagePayloadBuilder())
  ->forJpegImage()
  ->withImageContents($imageArray)
  ->build();

$docScanClient->uploadFaceCaptureImage($sessionId, $resourceId, $uploadFaceCapturePayload);
{% /tab %}
{% /code %}