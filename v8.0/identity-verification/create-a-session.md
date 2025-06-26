---
type: page
title: Create a session
listed: true
slug: create-a-session
description: 
index_title: Create a session
hidden: 
keywords: 
tags: 
---

Once you have added the Yoti SDK dependency to your project, you can use it to build and send your session as shown in the code snippet below:

{% code %}
{% tab language="javascript" %}
const path = require('path');
const fs = require("fs");

const {
    IDVClient,
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

const idvClient = new IDVClient(
    CLIENT_SDK_ID,
    PEM_KEY
 );

 idvClient
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
import com.yoti.api.client.docs.DocScanException;
import com.yoti.api.client.docs.session.create.CreateSessionResult;

...
DocScanClient docScanClient = DocScanClient.builder()
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
sdkID := "YOTI_CLIENT_SDK_ID";
key, _ := ioutil.ReadFile("YOTI_KEY_FILE_PATH")

client, err := docscan.NewClient(sdkId, key)

createSessionResult, err = client.CreateSession(sessionSpec)
{% /tab %}
{% tab language="json" %}
{
    "client_session_token_ttl": 900,
    "session_id": "5ef0ec7a-ba19-45c6-a208-2dd257ef2dd4",
    "client_session_token": "f097b1d9-84c9-48fd-bb4c-54f9ba6099c8"
}
{% /tab %}
{% /code %}

Your session is configured to with the following:

- Preferences
- Each check and task
- Notifications

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
Jump to our full example in our Quick Start section.    </div>
    <div class="alert-links"> 
       <a href="https://developers.yoti.com/identity-verification/quick-start
                ">Quick Start</a>
    </div>
</div>
{% /html %}

We go into more details over the next few pages on granular detail for creating a session.

{% html %}
<div class="alert-know">
    <div class="alert-title" id="know">
        Recommendation
    </div>
    <div class="alert-text">
Yoti strongly recommends you use notifications for each session status.    </div>
    <div class="alert-links"> 
       <a href="https://developers.yoti.com/identity-verification/notifications">Notifications</a>
    </div>
</div>
{% /html %}