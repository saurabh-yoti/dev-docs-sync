---
type: page
title: Embedded IDV
listed: true
slug: Embedded-IDV
description: 
index_title: Quick start
hidden: 
keywords: 
tags: 
---

To successfully integrate Embedded IDV through Yoti's SDK, there are two prerequisites:

- SDK ID
- Application key pair (.PEM file)

These details can be retrieved from the [application](/dbs-rtw/idv) that was created in the Yoti Hub.

## Install the SDK

Yoti SDKs are available for several languages through popular dependency management systems. 

To install the SDK: 

{% code %}
{% tab language="javascript" %}
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
composer require yoti/yoti-php-sdk
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

## Using Yoti SDKs

The description on how to use the above endpoint from the SDK can be found here:

Please read the above for a full description and understanding, below we have provided examples on how those requests will expose the new functionality.

First, specify the required imports and create a DocScanClient using the SDK ID and the PEM file.

{% code %}
{% tab language="javascript" %}
const path = require('path');
const fs = require('fs');

const {
    IDVClient,
    SessionSpecificationBuilder,
    SdkConfigBuilder,
} = require('yoti');

const YOTI_CLIENT_SDK_ID = 'YOTI_CLIENT_SDK_ID';
const YOTI_PEM = fs.readFileSync(path.join(__dirname, '/path/to/pem'));
const idvClient = new IDVClient(YOTI_CLIENT_SDK_ID, YOTI_PEM);
{% /tab %}
{% tab language="java" %}
import com.yoti.api.client.ClassPathKeySource;
import com.yoti.api.client.docs.DocScanClient;
import com.yoti.api.client.docs.session.create.SdkConfig;
import com.yoti.api.client.docs.session.create.SessionSpec;
import com.yoti.api.client.docs.session.create.CreateSessionResult;

...
DocScanClient docScanClient = DocScanClient.builder()
        .withClientSdkId("YOTI_CLIENT_SDK_ID")
        .withKeyPairSource(ClassPathKeySource.fromClasspath("/path/to/pem"))
        .build();
{% /tab %}
{% tab language="php" %}
use Yoti\DocScan\DocScanClient;
use Yoti\DocScan\Session\Create\SdkConfigBuilder;
use Yoti\DocScan\Session\Create\SessionSpecificationBuilder;

$YOTI_CLIENT_SDK_ID = 'YOTI_CLIENT_SDK_ID';
$YOTI_PEM = '/path/to/pem';

$docScanClient = new DocScanClient($YOTI_CLIENT_SDK_ID, $YOTI_PEM);
{% /tab %}
{% tab language="csharp" %}
using System.IO;
using System.Net.Http;
using Yoti.Auth;
using Yoti.Auth.DocScan;
using Yoti.Auth.DocScan.Session.Create;

...
const string YOTI_CLIENT_SDK_ID = "YOTI_CLIENT_SDK_ID";
const string PEM_PATH = "/path/to/pem";

StreamReader privateKeyStream = System.IO.File.OpenText(PEM_PATH);
var key = CryptoEngine.LoadRsaKey(privateKeyStream);

DocScanClient docScanClient = new DocScanClient(YOTI_CLIENT_SDK_ID, key, new HttpClient());
{% /tab %}
{% tab language="go" %}
sdkID := "YOTI_CLIENT_SDK_ID";
key, _ := ioutil.ReadFile("YOTI_KEY_FILE_PATH")

client, err := docscan.NewClient(sdkId, key)
if err != nil {
  	return nil, err
}
{% /tab %}
{% /code %}

Then, define the subject to be returned in the verification report. Also, set the identity profile requirements to the desired scheme:

{% code %}
{% tab language="javascript" %}
const subject = {
  subject_id: 'subject_id_string',
};

const identityProfileRequirements = {
  trust_framework: 'UK_TFIDA',
  scheme: {
    type: 'DBS',
    objective: 'STANDARD',
  },
};
{% /tab %}
{% tab language="java" %}
JSONObject subject = new JSONObject();
subject.put("subject_id", "subject_id_string");

JSONObject scheme = new JSONObject();
scheme.put("type", "DBS");
scheme.put("objective", "STANDARD");

JSONObject identityProfileRequirements = new JSONObject();
identityProfileRequirements.put("trust_framework", "UK_TFIDA");
identityProfileRequirements.put("scheme", scheme);
{% /tab %}
{% tab language="php" %}
$subject = (object)[
	'subject_id' => 'subject_id_string',
];

$identityProfileRequirements = (object)[
  'trust_framework' => 'UK_TFIDA',
  'scheme' => [
    'type' => 'DBS',
    'objective' => 'STANDARD'
  ]
];
{% /tab %}
{% tab language="csharp" %}
string subjectString = @"{
  subject_id: 'subject_id_string',
}";

JObject subject = JObject.Parse(subjectString);

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

subject := []byte(`{
	"subject_id": "subject-id-string"
}`)
{% /tab %}
{% /code %}

### Subject Explained

{% table widths="203,160,0" %}
| Field | Value | Description | Mandatory | 
| ---- | ---- | ---- | ---- | 
| subject | Object | Allows to provide information on the subject. | Optional | 
| subject_id | String | Allows to track the same user across multiple sessions. Should not contain any personal identifiable information. | Optional | 
{% /table %}

### Identity Profile Requirements Explained

{% table widths="203,160,0" %}
| Field | Value | Description | Mandatory | 
| ---- | ---- | ---- | ---- | 
| trust_framework | String | Defines under which trust framework this identity profile should be verified. Enum: UK_TFIDA | Required | 
| scheme | Object | Defines which scheme this identity profile should satisfy. The scheme must be supported by the specified trust framework otherwise the request is considered invalid. | Required | 
| type | String | Defines which scheme this identity profile should satisfy. Enum: DBS, RTW, RTR, DBS_RTW | Required | 
| objective | String | Defines the objective to be achieved for the particular scheme. It must be provided for those schemes where it is mandatory. Example, this is mandatory for DBS and the possible values are: ”BASIC”, “STANDARD”, “ENHANCED”. | Required | 
{% /table %}

Now, set up the SDK configuration as follows:

{% code %}
{% tab language="javascript" %}
const sdkConfig = new SdkConfigBuilder()
    .withAllowHandoff(true)
		.withSuccessUrl(`${APP_BASE_URL}/success`)
		.withErrorUrl(`${APP_BASE_URL}/error`)
    .build();
{% /tab %}
{% tab language="java" %}
SdkConfig sdkConfig = SdkConfig.builder()
    .withAllowHandoff(true)
    .withSuccessUrl("https://localhost:8443/success")
    .withErrorUrl("https://localhost:8443/error")
    .build();
{% /tab %}
{% tab language="php" %}
$sdkConfig = (new SdkConfigBuilder())
    ->withAllowHandoff(true)
    ->withSuccessUrl('https://localhost:8443/success')
    ->withErrorUrl('https://localhost:8443/error')
    ->build();
{% /tab %}
{% tab language="csharp" %}
SdkConfig sdkConfig = new SDKConfigBuilder()
    .WithAllowHandoff(true)
    .WithSuccessUrl("https://localhost:8443/success")
    .WithErrorUrl("https://localhost:8443/error")
    .Build();
{% /tab %}
{% tab language="go" %}
var sdkConfig *create.SDKConfig
sdkConfig, err = create.NewSdkConfigBuilder().
	withAllowHandoff(true).
	WithSuccessUrl("https://localhost:8443/success").
	WithErrorUrl("https://localhost:8443/error").
	WithPrivacyPolicyUrl("https://localhost:8443/privacy-policy").
	Build()

if err != nil {
  	return nil, err
}
{% /tab %}
{% /code %}

After this, create a session specification with the scheme requirements and the SDK config:

{% code %}
{% tab language="javascript" %}
const sessionSpec = new SessionSpecificationBuilder()
    .withSubject(subject)
    .withIdentityProfileRequirements(identityProfileRequirements)
    .withSdkConfig(sdkConfig)
    .build();
{% /tab %}
{% tab language="java" %}
SessionSpec sessionSpec = SessionSpec.builder()
    .withSubject(subject)
    .withIdentityProfileRequirements(identityProfileRequirements)
    .withSdkConfig(sdkConfig)
    .build();
{% /tab %}
{% tab language="php" %}
$sessionSpec = (new SessionSpecificationBuilder())
    ->withSubject($subject)
    ->withIdentityProfileRequirements($identityProfileRequirements)
    ->withSdkConfig($sdkConfig)
    ->build();
{% /tab %}
{% tab language="csharp" %}
SessionSpecification sessionSpec = new SessionSpecificationBuilder()
    .WithSubject(subject)
    .WithIdentityProfileRequirements(identityProfileRequirements)
    .WithSdkConfig(sdkConfig)
    .Build();
{% /tab %}
{% tab language="go" %}
sessionSpec, err = create.NewSessionSpecificationBuilder().
	WithSDKConfig(sdkConfig).
	WithIdentityProfileRequirements(identityProfile).
	WithSubject(subject).
	Build()
{% /tab %}
{% /code %}

Finally, use the DocScanClient to create a session by providing the session specification. Retrieve the Session ID and Client Session Token and utilise them to generate the iframe URL.

{% code %}
{% tab language="javascript" %}
const session = await idvClient.createSession(sessionSpec);

const sessionId = session.getSessionId();
const clientSessionToken = session.getClientSessionToken();

const iframeURL = `${config.YOTI_DOC_SCAN_IFRAME_URL}?		 sessionID=${sessionId}&sessionToken=${clientSessionToken}`;
{% /tab %}
{% tab language="java" %}
CreateSessionResult createSessionResult = docScanClient.createSession(sessionSpec);

string sessionId = createSessionResult.getSessionId();
string clientSessionToken = createSessionResult.getClientSessionToken();

private static final String IFRAME_URL_FORMAT = "%s/web/index.html?sessionID=%s&sessionToken=%s";
String apiUrl = System.getProperty(YotiConstants.PROPERTY_YOTI_DOCS_URL, YotiConstants.DEFAULT_YOTI_DOCS_URL);

String iframeURL = String.format(IFRAME_URL_FORMAT, apiUrl, sessionId, clientSessionToken);
{% /tab %}
{% tab language="php" %}
$session = $docScanClient->createSession($sessionSpec);

$sessionId = $session->getSessionId();
$clientSessionToken = $session->getClientSessionToken();

$doc.scan.iframe.url => (env('YOTI_DOC_SCAN_API_URL') ?: Constants::DOC_SCAN_API_URL) . '/web/index.html';

$iframeUrl => $doc.scan.iframe.url. '?' . http_build_query([
  'sessionID' => $sessionId,
  'sessionToken' => $clientSessionToken,
])
{% /tab %}
{% tab language="csharp" %}
CreateSessionResult createSessionResult = docScanClient.CreateSession(sessionSpec);

string sessionId = createSessionResult.SessionId;
string clientSessionToken = createSessionResult.ClientSessionToken;

string apiUrl = Environment.GetEnvironmentVariable("YOTI_DOC_SCAN_API_URL");
string path = $"web/index.html?sessionID={sessionId}&sessionToken={clientSessionToken}";

Uri uri = new Uri(apiUrl, path);
string iframeUrl = uri.ToString();
{% /tab %}
{% tab language="go" %}
createSessionResult, err = client.CreateSession(sessionSpec)
if err != nil {
  	return nil, err
}

sessionId = createSessionResult.SessionID
clientSessionToken = createSessionResult.ClientSessionToken

func getIframeURL(sessionID, sessionToken string) string {
	baseURL := "YOTI_DOC_SCAN_API_URL"
	return fmt.Sprintf("%s/web/index.html?sessionID=%s&sessionToken=%s", baseURL, sessionID, sessionToken)
}

iFrameURL := getIframeURL(createSessionResult.SessionID, createSessionResult.ClientSessionToken)
{% /tab %}
{% /code %}

---

## Client side view

Once you have generated the iframe URL, you can send it to the frontend for it to be rendered on the page. Please see example below:

{% code %}
{% tab language="html" %}
<!DOCTYPE html>
<html lang="en">
  
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Embedded IDV Integration</title>
</head>
  
<body>
  <div>
    <iframe style="border:none;" width="100%" height="750" allow="camera" src="<%= iframeUrl %>" allowfullscreen></iframe>
  </div>
</body>
  
</html>
{% /tab %}
{% /code %}

---

## Retrieve Results

After a session has been created, you can use the Yoti SDK to retrieve the session result (containing all the end-user's uploaded documents and associated metadata).

### Result of the session

Session retrieval requires a session ID. This is generated while creating a session as demonstrated above.

{% code %}
{% tab language="javascript" %}
// Returns the session result
const sessionResult = await idvClient.getSession(sessionId);

// Returns the session state
const state = sessionResult.getState();

// Returns session resources
const resources = session.getResources();
{% /tab %}
{% tab language="java" %}
// Returns the session result
GetSessionResult sessionResult = docScanClient.getSession(sessionId);

// Returns the session state
String state = sessionResult.getState();

// Returns session resources
ResourceContainer resources = sessionResult.getResources();
{% /tab %}
{% tab language="php" %}
// Returns the session result
$sessionResult = $docScanClient->getSession($sessionId);

// Returns the session state
$state = $sessionResult->getState();

// Returns session resources
$resources = $sessionResult->getResources();
{% /tab %}
{% tab language="csharp" %}
// Returns the session result
GetSessionResult sessionResult = docScanClient.GetSession(sessionId);

// Returns the session state
string state = sessionResult.State;

// Returns session resources
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

// Returns session resources
resources = sessionResult.Resources
{% /tab %}
{% /code %}

### Retrieve Media

In order to retrieve document images and document fields from the resources container we have to look for the relevant media ID inside of the id document pages.

{% code %}
{% tab language="javascript" %}
// Returns a collection of ID Documents
const idDocuments = resources.getIdDocuments();

const media = await idvClient.getMediaContent(sessionId, mediaId);

const buffer = media.getContent();
const base64Content = media.getBase64Content();
const mimeType = media.getMimeType();
{% /tab %}
{% tab language="java" %}
// Returns a collection of ID Documents
List<? extends IdDocumentResourceResponse> idDocuments = resources.getIdDocuments();

Media media = docScanClient.getMediaContent(sessionId, mediaId);
{% /tab %}
{% tab language="php" %}
// Returns a collection of ID Documents
$idDocuments = $resources->getIdDocuments();

$media = $docScanClient->getMediaContent($sessionId, $mediaId);
$base64Content = $media->getBase64Content();
$contentType = $media->getMimeType();
{% /tab %}
{% tab language="csharp" %}
// Returns a collection of ID Documents
List<IdDocumentResourceResponse> idDocuments = resources.IdDocuments;

MediaValue media = docScanClient.GetMediaContent(sessionId, mediaId);
{% /tab %}
{% tab language="go" %}
// Returns a collection of ID Documents
idDocuments = resources.IDDocuments

media, err := client.GetMediaContent(sessionId, mediaID)

mimeType = media.MIME()
data = media.Data()
{% /tab %}
{% /code %}

### Retrieve Identity Profile

Once the session has reached the state of 'Completed', identify profile can be successfully retrieved.

In case of a successful transaction, once the identity profile is received, the identity profile report JSON will be accessible. This contains the media ID which can then be used to get the full JSON response of the report.

{% code %}
{% tab language="javascript" %}
const identityProfile = sessionResult.getIdentityProfile();
const identityProfileReport = identityProfile.getIdentityProfileReport();

const mediaID = identityProfileReport.getMedia().getId();
const identityProfileReportMedia = await idvClient.getMediaContent(sessionId, mediaId);

const identityProfileReportMediaBuffer = identityProfileReportMedia.getContent();
{% /tab %}
{% tab language="java" %}
IdentityProfile identityProfile = sessionResult.getIdentityProfile();
IdentityProfileReport identityProfileReport = identityProfile.getIdentityProfileReport();

String mediaID = identityProfileReport.getMedia().getId();
Media identityProfileReportMedia = await docScanClient.getMediaContent(sessionId, mediaId);
{% /tab %}
{% tab language="php" %}
$identityProfile = $sessionResult->getIdentityProfile();
$identityProfileReport = $identityProfile->getIdentityProfileReport();

$mediaID = identityProfileReport->getMedia()->getId();

$identityProfileReportMedia = $docScanClient->getMediaContent($sessionId, $mediaId);
$base64Content = $media->getBase64Content();
$contentType = $media->getMimeType();
{% /tab %}
{% tab language="csharp" %}
string mediaId = sessionResult.IdentityProfile.Report["media"]["id"].ToString();
MediaValue mediaValue = docScanClient.GetMediaContent(sessionId, mediaId);

byte[] identityProfileReport = mediaValue.GetContent();
{% /tab %}
{% tab language="go" %}
identityProfile = sessionResult.IdentityProfileResponse
identityProfileReport = identityProfile.IdentityProfileResponse.Report

media, err := identityProfile.Report["media"].(map[string]interface{})
mediaID, err := media["id"].(string)

identityProfileReportMedia, err := client.GetMediaContent(sessionId, mediaID)
{% /tab %}
{% /code %}

---