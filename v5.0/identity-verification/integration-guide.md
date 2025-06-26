---
type: page
title: Create a session
listed: true
slug: integration-guide
description: 
index_title: Create a session
hidden: 
keywords: 
tags: 
---

There are three steps to follow to integrate the Identity verification SDK:

1. Install the SDK
2. Create the session
3. Launch the user view
4. Retrieve the results

This section will explain how to install the SDK. 

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      You will need the Yoti App on your phone and to have registered your business with Yoti. Click here for more info.
   </div>
   <div class="alert-links"> 
         <a target="_self" href="https://developers.yoti.com/yoti/getting-started">View Onboarding with Yoti</a>
      <a target="_self" href="https://developers.yoti.com/yoti/production-keys">View Generate API Keys</a> 
   </div>
</div>
{% /html %}

---

## Installing the SDK

Please use our Yoti SDKs to automatically build the relevant session for you. First you will need the following information about your application from [Yoti Hub](https://hub.yoti.com/login):

- Yoti SDK ID
- Your application key pair.

The Yoti SDKs are available via popular dependency management systems. Further details can be found on the pages of the [auto$](/identity-verification/quick-start).

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

## Create a session

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
{% tab language="java" title="Java v2" %}
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
{% /code %}

Your session is configured to with the following:

- Preferences
- Checks and Tasks
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