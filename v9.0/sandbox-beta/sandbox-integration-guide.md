---
type: page
title: Sandbox Integration Guide
listed: true
slug: sandbox-integration-guide
description: 
index_title: Sandbox Integration Guide
hidden: 
keywords: 
tags: 
---

Welcome to the free Identity verification Sandbox! The sandbox is an isolated test environment, intended to easily create test cases using dummy data where it's not feasible to test your integration with live data.

The sandbox environment will allow you to:

- Set outcomes and mock text results
- Mock approvals and rejections
- Mock liveness and image upload

The main difference between our Yoti production services and sandbox is the sandbox bypasses real world checks and tasks. Instead, you must specify the outcome beforehand, as opposed to it being returned from Yoti’s production systems.

This is achieved by using an additional response-config endpoint. A response-config must be set before proceeding with the user view for sandbox setups.

{% html %}
<div class="alert-BYS">

   <div class="alert-title" id="BYS">

      Before you start

   </div>

   <div class="alert-text" >
     We recommend familiarising yourself with the production integration to ensure you create reliable tests that accurately simulate the production environment.
You will also need some sandbox api keys.

   </div>

   <div class="alert-links"> 

      <a target="_self" href="https://developers.yoti.com/identity-verification/integration-guide">Integration Guide</a> 
      <a target="_self" href="https://developers.yoti.com/yoti/sandbox-keys">Generate Sandbox Keys</a> 
   </div>

</div>
{% /html %}

An overview of the steps is shown below:

Step 1: [Generating sandbox keys](/identity-verification/sandbox-keys)

Step 2: [Installing the sandbox SDK](https://developers.yoti.com/identity-verification/sandbox#install-the-sandbox-sdk)

Step 3: [Generating a sandbox session](https://developers.yoti.com/identity-verification/sandbox#generating-a-sandbox-session)

Step 4: [Configuring the response](https://developers.yoti.com/identity-verification/sandbox#configure-the-responses)([breakdown ](https://developers.yoti.com/identity-verification/sandbox#sandbox-breakdown)version available too)

Step 5: [Launching the user view](https://developers.yoti.com/identity-verification/sandbox#launching-the-user-view)

---

## [Supported Languages](https://developers.yoti.com/yoti/sandbox-app#supported-languages)

Just like the normal Yoti Client, the Yoti Sandbox Client SDK is available in seven languages:

- [Javascript (Node.js)](https://github.com/getyoti/yoti-node-sdk-sandbox/tree/master/examples/doc_scan)
- [Ruby](https://github.com/getyoti/yoti-ruby-sdk-sandbox/tree/master/examples)
- [PHP](https://github.com/getyoti/yoti-php-sdk-sandbox/tree/master/examples/doc-scan)
- [Python](https://github.com/getyoti/yoti-python-sdk-sandbox/tree/master/examples)
- [.NET](https://github.com/getyoti/yoti-dotnet-sdk-sandbox/tree/master/Examples/Yoti.Auth.Sandbox.Examples)

---

## Install the Sandbox SDK

Once you have generated your keys, you can continue with installing the Sandbox SDK into your backend.

Just like our production integration, the Yoti Sandbox Client SDK is available in seven languages and installing is easy through popular package managers.

{% code %}
{% tab language="javascript" %}
// Doc Scan Client (skip if already installed)
npm install -S -E yoti

// Sandbox
npm install -S -E -D @getyoti/sdk-sandbox
{% /tab %}
{% tab language="java" %}
// If you are using Maven, add the following dependency
<dependency>
    <groupId>com.yoti</groupId>
    <artifactId>yoti-sdk-api</artifactId>
    <version>3.8.0</version>
</dependency>

// If you are using Gradle, add the following dependency:
implementation group: 'com.yoti', name: 'yoti-sdk-api', version: '3.8.0'

// Sandbox
<dependency>
    <groupId>com.yoti</groupId>
    <artifactId>yoti-sdk-sandbox</artifactId>
    <version>3.8.0</version>
</dependency>

// If you are using Gradle, add the following dependency:
implementation group: 'com.yoti', name: 'yoti-sdk-sandbox', version: '3.8.0'
{% /tab %}
{% tab language="php" %}
// Get the Doc Scan PHP SDK library via a Composer package
composer require yoti/yoti-php-sdk

// Get the Doc Scan PHP SDK Sandbox library via a Composer package
composer require yoti/yoti-php-sdk-sandbox
{% /tab %}
{% tab language="python" %}
# Doc Scan Client (skip if already installed)
pip install yoti

# Sandbox
pip install yoti-sandbox
{% /tab %}
{% tab language="csharp" %}
// To install the Yoti NuGet package you will need to install NuGet.
// To import the latest Yoti SDK into your project, enter the following
// command from NuGet Package Manager Console in Visual Studio:

// Doc Scan Client (skip if already installed)
Install-Package Yoti

// Sandbox
Install-Package Yoti.Sandbox

// For other installation methods, see https://www.nuget.org/packages/Yoti
{% /tab %}
{% tab language="go" %}
// As of version 2.4.0, modules are used. This means it's not necessary to get a copy or fetch all dependencies 
// as instructed below, as the Go toolchain will fetch them as necessary. 
// You can simply add a `require github.com/getyoti/yoti-go-sdk/v2` to go.mod.
// To download and install the Yoti SDK and its dependencies, run the following command from your terminal:

go get "github.com/getyoti/yoti-go-sdk/v2”
{% /tab %}
{% tab language="ruby" %}
gem install yoti

# The gem provides a configuration generator for Ruby on Rails:

rails generate yoti:install

# To import the Yoti Sandbox SDK inside your project, add this line to your application's Gemfile:
gem 'yoti_sandbox'

# And then execute:
bundle install

# Or simply run the following command from your terminal:
gem install yoti_sandbox
{% /tab %}
{% /code %}

The sandbox client is packaged separately to the production Yoti client enabling it to be used as a development dependency.

## Initialising the sandbox client

You will need your Sandbox Client SDK ID and PEM file created from the [Yoti Hub](https://hub.yoti.com/) to initialise the sandbox client.

Please do not open the pem file as this might corrupt the key and you will need to create a new sandbox key.

{% code %}
{% tab language="javascript" %}
// Point the IDV Client at the sandbox by setting environment variable YOTI_IDV_API_URL to https://api.yoti.com/sandbox/idverify/v1

const { IDVClient } = require('yoti');
const fs = require('fs');

const SANDBOX_CLIENT_SDK_ID = 'SANDBOX_CLIENT_SDK_ID';
const PEM = fs.readFileSync('/path/to/your-pem-file.pem', 'utf8');

const idvClient = new IDVClient(SANDBOX_CLIENT_SDK_ID, PEM);
// Alternatively - const idvClient = new IDVClient(SANDBOX_CLIENT_SDK_ID, PEM, { apiUrl: 'sandbox-api-url' });
{% /tab %}
{% tab language="java" %}
// Point the Doc Scan client at the sandbox by setting environment variable
System.setProperty("yoti.docs.url", "https://api.yoti.com/sandbox/idverify/v1");

import com.yoti.api.client.ClassPathKeySource;
import com.yoti.api.client.docs.DocScanClient;
import com.yoti.api.client.docs.DocScanClientBuilder;

...
String YOTI_CLIENT_SDK_ID = "YOUR_SANDBOX_SDK_ID";
String PEM_PATH = "/path/to/pem";

String sessionId = "YOUR_SESSION_ID";

DocScanClient docScanClient = DocScanClient.builder()
        .withClientSdkId(YOTI_CLIENT_SDK_ID)
        .withKeyPairSource(ClassPathKeySource.fromClasspath(PEM_PATH))
        .build();
...
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\DocScan\DocScanClient;

$docScanClient = new DocScanClient('SANDBOX_CLIENT_SDK_ID', '/path/to/your-pem-file.pem', [
    'api.url' => 'https://api.yoti.com/sandbox/idverify/v1'
]);
{% /tab %}
{% tab language="python" %}
from yoti_python_sdk.doc_scan import (
    DocScanClient
)

sandbox_client_sdk_id = 'YOUR_SANDBOX_SDK_ID'
pem_file_path = '/path/to/pem'

doc_scan_client = DocScanClient(sandbox_client_sdk_id, pem_file_path, api_url="https://api.yoti.com/sandbox/idverify/v1")
{% /tab %}
{% tab language="csharp" %}
using System;
using System.IO;
using System.Net.Http;
using Yoti.Auth;
using Yoti.Auth.DocScan;
...
const string YOTI_CLIENT_SDK_ID = "YOTI_CLIENT_SDK_ID";
const string PEM_PATH = "/path/to/pem";

StreamReader privateKeyStream = System.IO.File.OpenText(PEM_PATH);
var key = CryptoEngine.LoadRsaKey(privateKeyStream);

var docScanClient = new DocScanClient(YOTI_CLIENT_SDK_ID, key, new HttpClient(), new Uri("https://api.yoti.com/sandbox/idverify/v1"));
...
{% /tab %}
{% tab language="go" %}
// COMING SOON
{% /tab %}
{% tab language="ruby" %}
# COMING SOON
{% /tab %}
{% tab language="java" title="Java v2" %}
// Point the Doc Scan client at the sandbox by setting environment variable
System.setProperty("yoti.docs.url", "https://api.yoti.com/sandbox/idverify/v1");

import com.yoti.api.client.ClassPathKeySource;
import com.yoti.api.client.docs.DocScanClient;
import com.yoti.api.client.docs.DocScanClientBuilder;

...
String YOTI_CLIENT_SDK_ID = "YOUR_SANDBOX_SDK_ID";
String PEM_PATH = "/path/to/pem";

String sessionId = "YOUR_SESSION_ID";

DocScanClient docScanClient = DocScanClientBuilder.newInstance()
        .withClientSdkId(YOTI_CLIENT_SDK_ID)
        .withKeyPairSource(ClassPathKeySource.fromClasspath(PEM_PATH))
        .build();
...
{% /tab %}
{% /code %}

**Configuring the sandbox client**

{% code %}
{% tab language="javascript" %}
const { SandboxIDVClientBuilder } = require('@getyoti/sdk-sandbox');

const sandboxClient = new SandboxIDVClientBuilder()
  .withClientSdkId(SANDBOX_CLIENT_SDK_ID)
  .withPemString(PEM)
  .build();
{% /tab %}
{% tab language="java" %}
import com.yoti.api.client.ClassPathKeySource;
import com.yoti.api.client.sandbox.docs.DocScanSandboxClient;

...
String SANDBOX_CLIENT_SDK_ID = "SANDBOX_CLIENT_SDK_ID";
String SANDBOX_KEY_PAIR_FILE_NAME = "/path/to/pem";

DocScanSandboxClient sandboxClient = DocScanSandboxClient.builder()
        .withSdkId(SANDBOX_CLIENT_SDK_ID)
        .withKeyPair(ClassPathKeySource.fromClasspath(SANDBOX_KEY_PAIR_FILE_NAME))
        .build();
...
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\Sandbox\DocScan\SandboxClient;

$sandboxClient = new SandboxClient('SANDBOX_CLIENT_SDK_ID', '/path/to/your-pem-file.pem');
{% /tab %}
{% tab language="python" %}
from yoti_python_sandbox.doc_scan.client import DocScanSandboxClient

sandbox_client_sdk_id = 'YOUR_SANDBOX_SDK_ID'
pem_file_path = '/path/to/pem'

doc_scan_sandbox_client = DocScanSandboxClient(sandbox_client_sdk_id, pem_file_path)
{% /tab %}
{% tab language="csharp" %}
using System.IO;
using Yoti.Auth;
using Yoti.Auth.Sandbox.DocScan.Request;

...
const string YOTI_CLIENT_SDK_ID = "YOUR_SANDBOX_SDK_ID";
const string PEM_PATH = "/path/to/pem";

StreamReader privateKeyStream = System.IO.File.OpenText(PEM_PATH);
var key = CryptoEngine.LoadRsaKey(privateKeyStream);

var sandboxClient = new SandboxClientBuilder()
    .WithClientSdkId(YOTI_CLIENT_SDK_ID)
    .WithKeyPair(key)
    .Build();
...
{% /tab %}
{% tab language="go" %}
// COMING SOON
{% /tab %}
{% tab language="ruby" %}
# COMING SOON
{% /tab %}
{% /code %}

---

## Generating a sandbox session

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      Check out how to create a session with Identity verification for a full understanding of how the product works. 
   </div>
   <div class="alert-links"> 
      <a href="https://developers.yoti.com/identity-verification/integration-guide">Integration guide</a>
   </div>
</div>
{% /html %}

A sandbox session will be created by

1) Replace the base URL with the Sandbox URL.

2) Replace the SDK ID

3) Replacing the pem file.

{% code %}
{% tab language="http" %}
Sandbox - https://api.yoti.com/sandbox/idverify/v1
Production - https://api.yoti.com/idverify/v1
{% /tab %}
{% /code %}

---

## Configure the responses

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      Understand the results of a session and the report. 
   </div>
   <div class="alert-links"> 
      <a href="https://developers.yoti.com/identity-verification/results">Retrieve results</a>
           <a href="https://developers.yoti.com/identity-verification/understanding-the-report">Understanding the report</a>
   </div>
</div>
{% /html %}

Sandbox requires you to set an expected outcome for your tasks and checks.

Below is a snippet of a full response config for all checks and tasks. These values are provided to mock the return output of fetching the completed session. For a further explanation there is a breakdown version below.

{% code %}
{% tab language="javascript" %}
const {
  SandboxIDVClientBuilder,
  SandboxBreakdownBuilder,
  SandboxRecommendationBuilder,
  SandboxDocumentAuthenticityCheckBuilder,
  SandboxCheckReportsBuilder,
  SandboxResponseConfigBuilder,
  SandboxDocumentTextDataCheckBuilder,
  SandboxTaskResultsBuilder,
  SandboxZoomLivenessCheckBuilder,
  SandboxDocumentFaceMatchCheckBuilder,
  SandboxDocumentTextDataExtractionTaskBuilder,
} = require('@getyoti/sdk-sandbox');

const sandboxClient = new SandboxIDVClientBuilder()
  .withClientSdkId('YOUR_SANDBOX_SDK_ID')
  .withPemString('YOUR_PEM_FILE')
  .build();

const sessionId = "YOUR_SANDBOX_SESSION_ID"

async function configureSessionResponse() {
  const documentAuthenticityCheckConfig = new SandboxDocumentAuthenticityCheckBuilder()
    .withRecommendation(
      new SandboxRecommendationBuilder().withValue('APPROVE').build(),
    )
    .withBreakdown(
      new SandboxBreakdownBuilder()
        .withSubCheck('document_in_date')
        .withResult('PASS')
        .build(),
    )
    .build();
  
  const textDataCheckConfig = new SandboxDocumentTextDataCheckBuilder()
    .withRecommendation(
      new SandboxRecommendationBuilder().withValue('APPROVE').build(),
    )
    .withBreakdown(
      new SandboxBreakdownBuilder()
        .withSubCheck('text_data_readable')
        .withResult('PASS')
        .build(),
    )
    .withDocumentFields({
      full_name: 'John Doe',
      nationality: 'GBR',
      date_of_birth: '1986-06-01',
      document_number: '123456789',
    })
    .build();

  const livenessCheckConfig = new SandboxZoomLivenessCheckBuilder()
    .withRecommendation(
      new SandboxRecommendationBuilder().withValue('APPROVE').build(),
    )
    .withBreakdown(
      new SandboxBreakdownBuilder()
        .withSubCheck('liveness_auth')
        .withResult('PASS')
        .build()
    )
    .build()

  const faceMatchCheckConfig = new SandboxDocumentFaceMatchCheckBuilder()
    .withRecommendation(
      new SandboxRecommendationBuilder().withValue('APPROVE').build(),
    )
    .withBreakdown(
      new SandboxBreakdownBuilder()
        .withSubCheck('ai_face_match')
        .withResult('PASS')
        .withDetail('confidence_score', '0.81')
        .build()
    )
    .build();

  const textExtractionConfig = new SandboxDocumentTextDataExtractionTaskBuilder()
    .withDocumentFields({
      full_name: 'John Doe',
      nationality: 'GBR',
      date_of_birth: '1986-06-01',
      document_number: '123456789',
    })
    .build();

  const checkReportsConfig = new SandboxCheckReportsBuilder()
    .withAsyncReportDelay(5)
    .withDocumentAuthenticityCheck(documentAuthenticityCheckConfig)
    .withDocumentTextDataCheck(textDataCheckConfig)
    .withLivenessCheck(livenessCheckConfig)
    .withDocumentFaceMatchCheck(faceMatchCheckConfig)
    .build();

  const taskResultsConfig = new SandboxTaskResultsBuilder()
    .withDocumentTextDataExtractionTask(textExtractionConfig)
    .build();

  const responseConfig = new SandboxResponseConfigBuilder()
    .withCheckReports(checkReportsConfig)
    .withTaskResults(taskResultsConfig)
    .build();

  await sandboxClient.configureSessionResponse(sessionId, responseConfig);
}

configureSessionResponse();
{% /tab %}
{% tab language="java" %}
import com.yoti.api.client.ClassPathKeySource;
import com.yoti.api.client.sandbox.docs.DocScanSandboxClient;
import com.yoti.api.client.sandbox.docs.request.ResponseConfig;
import com.yoti.api.client.sandbox.docs.request.SandboxCheckReports;
import com.yoti.api.client.sandbox.docs.request.SandboxTaskResults;
import com.yoti.api.client.sandbox.docs.request.check.SandboxDocumentAuthenticityCheck;
import com.yoti.api.client.sandbox.docs.request.check.SandboxDocumentFaceMatchCheck;
import com.yoti.api.client.sandbox.docs.request.check.SandboxDocumentTextDataCheck;
import com.yoti.api.client.sandbox.docs.request.check.SandboxLivenessCheck;
import com.yoti.api.client.sandbox.docs.request.check.report.SandboxBreakdown;
import com.yoti.api.client.sandbox.docs.request.check.report.SandboxRecommendation;
import com.yoti.api.client.sandbox.docs.request.task.SandboxDocumentTextDataExtractionTask;
import org.bouncycastle.jce.provider.BouncyCastleProvider;

...
Security.addProvider(new BouncyCastleProvider());  
  
String SANDBOX_CLIENT_SDK_ID = "YOUR_SANDBOX_SDK_ID";
String SANDBOX_KEY_PAIR_FILE_NAME = "/path/to/pem";

DocScanSandboxClient sandboxClient = DocScanSandboxClient.builder()
        .withSdkId(SANDBOX_CLIENT_SDK_ID)
        .withKeyPair(ClassPathKeySource.fromClasspath(SANDBOX_KEY_PAIR_FILE_NAME))
        .build();

String sessionId = "YOUR_SESSION_ID";

SandboxDocumentAuthenticityCheck documentAuthenticityCheckConfig = SandboxDocumentAuthenticityCheck.builder()
        .withRecommendation(SandboxRecommendation.builder()
                .withValue("APPROVE")
                .build())
        .withBreakdown(SandboxBreakdown.builder()
                .withSubCheck("document_in_date")
                .withResult("PASS")
                .build())
        .build();

SandboxDocumentTextDataCheck textDataCheckConfig = SandboxDocumentTextDataCheck.builder()
        .withRecommendation(SandboxRecommendation.builder().withValue("APPROVE").build())
        .withBreakdown(SandboxBreakdown.builder()
                .withSubCheck("text_data_readable")
                .withResult("PASS")
                .build())
        .withDocumentField("full_name", "John Doe")
        .withDocumentField("nationality", "GBR")
        .withDocumentField("date_of_birth", "1986-06-01")
        .withDocumentField("document_number", "123456789")
        .build();

SandboxLivenessCheck livenessCheckConfig = SandboxLivenessCheck.forZoomLiveness()
        .withRecommendation(SandboxRecommendation.builder().withValue("APPROVE").build())
        .withBreakdown(SandboxBreakdown.builder()
                .withSubCheck("liveness_auth")
                .withResult("PASS")
                .build())
        .build();

SandboxDocumentFaceMatchCheck faceMatchCheckConfig = SandboxDocumentFaceMatchCheck.builder()
        .withRecommendation(SandboxRecommendation.builder().withValue(("APPROVE")).build())
        .withBreakdown(SandboxBreakdown.builder()
                .withSubCheck("ai_face_match")
                .withResult("PASS")
                .withDetail("confidence_score", "0.81")
                .build())
        .build();

SandboxDocumentTextDataExtractionTask textExtractionConfig = SandboxDocumentTextDataExtractionTask.builder()
        .withDocumentField("full_name", "John Doe")
        .withDocumentField("nationality", "GBR")
        .withDocumentField("date_of_birth", "1986-06-01")
        .withDocumentField("document_number", "123456789")
        .build();

SandboxCheckReports checkReportsConfig = SandboxCheckReports.builder()
        .withAsyncReportDelay(5)
        .withDocumentAuthenticityCheck(documentAuthenticityCheckConfig)
        .withDocumentTextDataCheck(textDataCheckConfig)
        .withLivenessCheck(livenessCheckConfig)
        .withDocumentFaceMatchCheck(faceMatchCheckConfig)
        .build();

SandboxTaskResults taskResultsConfig = SandboxTaskResults.builder()
        .withDocumentTextDataExtractionTask(textExtractionConfig)
        .build();

ResponseConfig responseConfig = ResponseConfig.builder()
        .withCheckReports(checkReportsConfig)
        .withTaskResults(taskResultsConfig)
        .build();

sandboxClient.configureSessionResponse(sessionId, responseConfig);
...
{% /tab %}
{% tab language="php" %}
<?php

require_once './vendor/autoload.php';

use Yoti\Sandbox\DocScan\Request\Check\Report\SandboxBreakdownBuilder;
use Yoti\Sandbox\DocScan\Request\Check\Report\SandboxRecommendationBuilder;
use Yoti\Sandbox\DocScan\Request\Check\SandboxDocumentAuthenticityCheckBuilder;
use Yoti\Sandbox\DocScan\Request\Check\SandboxDocumentFaceMatchCheckBuilder;
use Yoti\Sandbox\DocScan\Request\Check\SandboxDocumentTextDataCheckBuilder;
use Yoti\Sandbox\DocScan\Request\Check\SandboxZoomLivenessCheckBuilder;
use Yoti\Sandbox\DocScan\Request\SandboxCheckReportsBuilder;
use Yoti\Sandbox\DocScan\Request\SandboxResponseConfigBuilder;
use Yoti\Sandbox\DocScan\Request\SandboxTaskResultsBuilder;
use Yoti\Sandbox\DocScan\Request\Task\SandboxDocumentTextDataExtractionTaskBuilder;
use Yoti\Sandbox\DocScan\SandboxClient;

$sandboxClient = new SandboxClient('YOUR_SANDBOX_SDK_ID', '/path/to/pem');

$sessionId = "YOUR_SESSION_ID";

$documentAuthenticityCheckConfig = (new SandboxDocumentAuthenticityCheckBuilder())
    ->withRecommendation(
        (new SandboxRecommendationBuilder())->withValue('APPROVE')->build()
    )
    ->withBreakdown(
        (new SandboxBreakdownBuilder())
            ->withSubCheck('document_in_date')
            ->withResult('PASS')
            ->build()
    )
    ->build();

$textDataCheckConfig = (new SandboxDocumentTextDataCheckBuilder())
    ->withRecommendation(
        (new SandboxRecommendationBuilder())->withValue('APPROVE')->build()
    )
    ->withBreakdown(
        (new SandboxBreakdownBuilder())
            ->withSubCheck('text_data_readable')
            ->withResult('PASS')
            ->build()
    )
    ->withDocumentFields([
        'full_name' => 'John Doe',
        'nationality' => 'GBR',
        'date_of_birth' => '1986-06-01',
        'document_number' => '123456789',
    ])
    ->build();

$livenessCheckConfig = (new SandboxZoomLivenessCheckBuilder())
    ->withRecommendation(
        (new SandboxRecommendationBuilder())->withValue('APPROVE')->build()
    )
    ->withBreakdown(
        (new SandboxBreakdownBuilder())
            ->withSubCheck('liveness_auth')
            ->withResult('PASS')
            ->build()
    )
    ->build();

$faceMatchCheckConfig = (new SandboxDocumentFaceMatchCheckBuilder())
    ->withRecommendation(
        (new SandboxRecommendationBuilder())->withValue('APPROVE')->build()
    )
    ->withBreakdown(
        (new SandboxBreakdownBuilder())
            ->withSubCheck('ai_face_match')
            ->withResult('PASS')
            ->withDetail('confidence_score', '0.81')
            ->build()
    )
    ->build();

$textExtractionConfig = (new SandboxDocumentTextDataExtractionTaskBuilder())
    ->withDocumentFields([
        'full_name' => 'John Doe',
        'nationality' => 'GBR',
        'date_of_birth' => '1986-06-01',
        'document_number' => '123456789',
    ])
    ->build();

$checkReportsConfig = (new SandboxCheckReportsBuilder())
    ->withAsyncReportDelay(5)
    ->withDocumentAuthenticityCheck($documentAuthenticityCheckConfig)
    ->withDocumentTextDataCheck($textDataCheckConfig)
    ->withLivenessCheck($livenessCheckConfig)
    ->withDocumentFaceMatchCheck($faceMatchCheckConfig)
    ->build();

$taskResultsConfig = (new SandboxTaskResultsBuilder())
    ->withDocumentTextDataExtractionTask($textExtractionConfig)
    ->build();

$responseConfig = (new SandboxResponseConfigBuilder())
    ->withCheckReports($checkReportsConfig)
    ->withTaskResults($taskResultsConfig)
    ->build();

$sandboxClient->configureSessionResponse($sessionId, $responseConfig);
{% /tab %}
{% tab language="python" %}
from yoti_python_sandbox.doc_scan import (
    ResponseConfigBuilder,
    SandboxDocumentFilterBuilder,
)
from yoti_python_sandbox.doc_scan.check import (
    SandboxDocumentAuthenticityCheckBuilder,
    SandboxBreakdownBuilder,
    SandboxRecommendationBuilder,
    SandboxDocumentFaceMatchCheckBuilder,
    SandboxDocumentTextDataCheckBuilder,
    SandboxZoomLivenessCheckBuilder,
    SandboxDetail,
)
from yoti_python_sandbox.doc_scan.check_reports import SandboxCheckReportsBuilder
from yoti_python_sandbox.doc_scan.client import DocScanSandboxClient
from yoti_python_sandbox.doc_scan.task import (
    SandboxDocumentTextDataExtractionTaskBuilder,
)
from yoti_python_sandbox.doc_scan.task_results import SandboxTaskResultsBuilder

sandbox_client_sdk_id = "YOUR_SANDBOX_SDK_ID"
pem_file_path = '/path/to/pem'

doc_scan_sandbox_client = DocScanSandboxClient(
    sandbox_client_sdk_id, pem_file_path)

session_id = "YOUR_SESSION_ID"

document_authenticity_check_config = (
    SandboxDocumentAuthenticityCheckBuilder()
    .with_recommendation(
        SandboxRecommendationBuilder()
        .with_value("APPROVE")
        .build()
    )
    .with_breakdown(
        SandboxBreakdownBuilder()
        .with_sub_check("document_in_date")
        .with_result("PASS")
        .build()
    )
    .build()
)

text_data_check_config = (
    SandboxDocumentTextDataCheckBuilder()
    .with_recommendation(
        SandboxRecommendationBuilder()
        .with_value("APPROVE")
        .build()
    )
    .with_breakdown(
        SandboxBreakdownBuilder()
        .with_sub_check("text_data_readable")
        .with_result("PASS")
        .build()
    )
    .with_document_field("full_name", "John Doe")
    .with_document_field("nationality", "GBR")
    .with_document_field("date_of_birth", "1986-06-01")
    .with_document_field("document_number", "123456789")
    .build()
)

liveness_check_config = (
    SandboxZoomLivenessCheckBuilder()
    .with_recommendation(
        SandboxRecommendationBuilder()
        .with_value("APPROVE")
        .build()
    )
    .with_breakdown(
        SandboxBreakdownBuilder()
        .with_sub_check("liveness_auth")
        .with_result("PASS")
        .build()
    )
    .build()
)

face_match_check_config = (
    SandboxDocumentFaceMatchCheckBuilder()
    .with_recommendation(
        SandboxRecommendationBuilder()
        .with_value("APPROVE")
        .build()
    )
    .with_breakdown(
        SandboxBreakdownBuilder()
        .with_sub_check("ai_face_match")
        .with_result("PASS")
        .with_detail(
            SandboxDetail("confidence_score", "0.81")
        )
        .build()
    )
    .build()
)

text_extraction_config = (
    SandboxDocumentTextDataExtractionTaskBuilder()
    .with_document_field("full_name", "John Doe")
    .with_document_field("nationality", "GBR")
    .with_document_field("date_of_birth", "1986-06-01")
    .with_document_field("document_number", "123456789")
    .build()
)

check_reports_config = (
    SandboxCheckReportsBuilder()
    .with_async_report_delay(5)
    .with_document_authenticity_check(document_authenticity_check_config)
    .with_document_text_data_check(text_data_check_config)
    .with_liveness_check(liveness_check_config)
    .with_document_face_match_check(face_match_check_config)
    .build()
)

task_results_config = (
    SandboxTaskResultsBuilder()
    .with_text_extraction_task(text_extraction_config)
    .build()
)

response_config = (
    ResponseConfigBuilder()
    .with_check_reports(check_reports_config)
    .with_task_results(task_results_config)
    .build()
)

doc_scan_sandbox_client.configure_session_response(session_id, response_config)
{% /tab %}
{% tab language="csharp" %}
using System.Collections.Generic;
using System.IO;
using Yoti.Auth;
using Yoti.Auth.Sandbox.DocScan.Request;
using Yoti.Auth.Sandbox.DocScan.Request.Check;
using Yoti.Auth.Sandbox.DocScan.Request.Check.Report;
using Yoti.Auth.Sandbox.DocScan.Request.Task;

const string YOTI_CLIENT_SDK_ID = "YOUR_SANDBOX_SDK_ID";
const string PEM_PATH = "/path/to/pem";

...
StreamReader privateKeyStream = System.IO.File.OpenText(PEM_PATH);
var key = CryptoEngine.LoadRsaKey(privateKeyStream);

var sandboxClient = new SandboxClientBuilder()
    .WithClientSdkId(YOTI_CLIENT_SDK_ID)
    .WithKeyPair(key)
    .Build();

const string sessionId = "YOUR_SESSION_ID";

var documentAuthenticityCheckConfig = new SandboxDocumentAuthenticityCheckBuilder()
    .WithRecommendation(
    new SandboxRecommendationBuilder()
    .WithValue("APPROVE")
    .Build()
    )
    .WithBreakdown(
    new SandboxBreakdownBuilder()
    .WithSubCheck("document_in_date")
    .WithResult("PASS")
    .Build()
    )
    .Build();

var textDataCheckConfig = new SandboxDocumentTextDataCheckBuilder()
    .WithRecommendation(
    new SandboxRecommendationBuilder()
    .WithValue("APPROVE")
    .Build()
    )
    .WithBreakdown(
    new SandboxBreakdownBuilder()
    .WithSubCheck("text_data_readable")
    .WithResult("PASS")
    .Build()
    )
    .WithDocumentFields(
    new Dictionary<string, object> {
        {
        "full_name",
        "John Doe"
        },
        {
        "nationality",
        "GBR"
        },
        {
        "date_of_birth",
        "1986-06-01"
        },
        {
        "document_number",
        "123456789"
        }
    })
    .Build();

var supplementaryTextDataCheckConfig = new SandboxSupplementaryDocTextDataCheckBuilder()
    .WithRecommendation(
    new SandboxRecommendationBuilder()
    .WithValue("APPROVE")
    .Build()
    )
    .WithDocumentFields(
      new Dictionary<string, object> {
          { "full_name", "John Doe"},
          {"date_of_issue", "2018-06-01"},
          {"organisation", "Yoti"},
          { "structured_postal_address", new Dictionary<string, object> {
                                             {"address_format" ,  1},
                                             {"building_number", "64"},
                                             {"street", "Derwent Road"},
                                             {"address_line1", "64 Derwent Road"},
                                             {"address_line2", "London"},
                                             {"address_line3", "United Kingdom"},
                                             {"address_line4", "SW20 9NH"},
                                             {"town_city", "United Kingdom"},
                                             {"state", "Greater London"},
                                             {"postal_code", "SW20 9NH"},
                                             {"country_iso", "GBR"},
                                             {"country", "United Kingdom"},
                                             {"formatted_address", "64 Derwent Road\nLondon\nSW20 9NH\nUnited Kingdom"}
                                            }}
    })
    .Build();

var livenessCheckConfig = new SandboxZoomLivenessCheckBuilder()
    .WithRecommendation(
    new SandboxRecommendationBuilder()
    .WithValue("APPROVE")
    .Build()
    )
    .WithBreakdown(
    new SandboxBreakdownBuilder()
    .WithSubCheck("liveness_auth")
    .WithResult("PASS")
    .Build()
    )
    .Build();

var faceMatchCheckConfig = new SandboxDocumentFaceMatchCheckBuilder()
    .WithRecommendation(
    new SandboxRecommendationBuilder()
    .WithValue("APPROVE")
    .Build()
    )
    .WithBreakdown(
    new SandboxBreakdownBuilder()
    .WithSubCheck("ai_face_match")
    .WithResult("PASS")
    .WithDetail(new SandboxDetail("confidence_score", "0.81"))
    .Build()
    )
    .Build();

var textExtractionConfig = new SandboxDocumentTextDataExtractionTaskBuilder()
    .WithDocumentFields(
    new Dictionary<string, object> {
        { "full_name","John Doe"},
        { "nationality","GBR"},
        { "date_of_birth","1986-06-01"},
        { "document_number","123456789"}
    })
    .Build();

var supplementaryTextExtractionConfig = new SandboxSupplementaryDocTextDataExtractionTaskBuilder()
    .WithDocumentFields(
     new Dictionary<string, object> {
         { "full_name", "John Doe"},
         {"date_of_issue", "2018-06-01"},
         {"organisation", "Yoti"},
         { "structured_postal_address", new Dictionary<string, object> {
                                                {"address_format" ,  1},
                                                {"building_number", "64"},
                                                {"street", "Derwent Road"},
                                                {"address_line1", "64 Derwent Road"},
                                                {"address_line2", "London"},
                                                {"address_line3", "United Kingdom"},
                                                {"address_line4", "SW20 9NH"},
                                                {"town_city", "United Kingdom"},
                                                {"state", "Greater London"},
                                                {"postal_code", "SW20 9NH"},
                                                {"country_iso", "GBR"},
                                                {"country", "United Kingdom"},
                                                {"formatted_address", "64 Derwent Road\nLondon\nSW20 9NH\nUnited Kingdom"}
                                            }}
     })
     .Build()

var checkReportsConfig = new SandboxCheckReportsBuilder()
    .WithAsyncReportDelay(5)
    .WithDocumentAuthenticityCheck(documentAuthenticityCheckConfig)
    .WithDocumentTextDataCheck(textDataCheckConfig)
    .WithSupplementaryDocTextDataCheck(supplementaryTextDataCheckConfig)
    .WithLivenessCheck(livenessCheckConfig)
    .WithDocumentFaceMatchCheck(faceMatchCheckConfig)
    .Build();

var taskResultsConfig = new SandboxTaskResultsBuilder()
    .WithDocumentTextDataExtractionTask(textExtractionConfig)
    .WithSupplementaryDocTextDataExtractionTask(supplementaryTextExtractionConfig)
    .Build();

var responseConfig = new ResponseConfigBuilder()
    .WithCheckReports(checkReportsConfig)
    .WithTaskResults(taskResultsConfig)
    .Build();

sandboxClient.ConfigureSessionResponse(sessionId, responseConfig);
...
{% /tab %}
{% tab language="go" %}
// COMING SOON
{% /tab %}
{% tab language="ruby" %}
// COMING SOON
{% /tab %}
{% /code %}

**Async report delay**

The Async report delay is a timer (in seconds) which simulates a delay between the Identity verification iFrame user journey and the result of the report, set by your expectation. By using this facility you can effectively handle pending states, or results that are not returned instantly (such as manual checks).

---

## Sandbox Breakdown

This section will go into detail on each task and check with the configuration split out.

### Task Results

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      Understand the task extraction and how to retrieve the user results . 
   </div>
   <div class="alert-links"> 
      <a href="https://developers.yoti.com/identity-verification/results">Retrieve results</a>
           <a href="https://developers.yoti.com/identity-verification/results#retrieve-id-document-information">Retrieve user information</a>
   </div>
</div>
{% /html %}

### Data extraction task (ID Document)

The task result contains the extracted text, defined by the **document_fields** property. This should be used to mock extracted text from documents.

{% code %}
{% tab language="javascript" title="" %}
const {
  SandboxDocumentTextDataExtractionTaskBuilder,
} = require('@getyoti/sdk-sandbox');

const textExtractionConfig = new SandboxDocumentTextDataExtractionTaskBuilder()
  .withDocumentFields({
    full_name: 'John Doe',
    nationality: 'GBR',
    date_of_birth: '1986-06-01',
    document_number: '123456789',
  })
  .build();
{% /tab %}
{% tab language="java" %}
import com.yoti.api.client.sandbox.docs.request.task.SandboxDocumentTextDataExtractionTask;

...
SandboxDocumentTextDataExtractionTask textExtractionConfig = SandboxDocumentTextDataExtractionTask.builder()
        .withDocumentField("full_name", "John Doe")
        .withDocumentField("nationality", "GBR")
        .withDocumentField("date_of_birth", "1986-06-01")
        .withDocumentField("document_number", "123456789")
        .build();
...
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\Sandbox\DocScan\Request\Task\SandboxDocumentTextDataExtractionTaskBuilder;

$textExtractionConfig = (new SandboxDocumentTextDataExtractionTaskBuilder())
    ->withDocumentFields([
        'full_name' => 'John Doe',
        'nationality' => 'GBR',
        'date_of_birth' => '1986-06-01',
        'document_number' => '123456789',
    ])
    ->build();
{% /tab %}
{% tab language="python" %}
from yoti_python_sandbox.doc_scan.task import (
    SandboxDocumentTextDataExtractionTaskBuilder,
)

text_extraction_config = (
    SandboxDocumentTextDataExtractionTaskBuilder()
    .with_document_field("full_name", "John Doe")
    .with_document_field("nationality", "GBR")
    .with_document_field("date_of_birth", "1986-06-01")
    .with_document_field("document_number", "123456789")
    .build()
)
{% /tab %}
{% tab language="csharp" %}
using System.Collections.Generic;
using System.IO;
using Yoti.Auth;
using Yoti.Auth.Sandbox.DocScan.Request;
using Yoti.Auth.Sandbox.DocScan.Request.Check;
using Yoti.Auth.Sandbox.DocScan.Request.Check.Report;
using Yoti.Auth.Sandbox.DocScan.Request.Task;

var textExtractionConfig = new SandboxDocumentTextDataExtractionTaskBuilder()
    .WithDocumentFields(
     new Dictionary<string, object> {
         { "full_name", "John Doe"},
         { "nationality", "GBR"},
         { "date_of_birth", "1986-06-01"},
         { "document_number", "123456789"}
     })
     .Build()
{% /tab %}
{% /code %}

### Data extraction task (Supplementary Document)

The supplementary task result contains the extracted text from the supplementary document, also defined by the **document_fields** property. This should be used to mock extracted text from  supplementary documents.

{% code %}
{% tab language="javascript" %}

{% /tab %}
{% tab language="java" %}
// Click to edit code
{% /tab %}
{% tab language="php" %}
// Click to edit code
{% /tab %}
{% tab language="python" %}
// Click to edit code
{% /tab %}
{% tab language="csharp" %}
using System.Collections.Generic;
using System.IO;
using Yoti.Auth;
using Yoti.Auth.Sandbox.DocScan.Request;
using Yoti.Auth.Sandbox.DocScan.Request.Check;
using Yoti.Auth.Sandbox.DocScan.Request.Check.Report;
using Yoti.Auth.Sandbox.DocScan.Request.Task;

var supplementaryTextExtractionConfig = new SandboxSupplementaryDocTextDataExtractionTaskBuilder()
    .WithDocumentFields(
        new Dictionary<string, object> {
            { "full_name", "John Doe"},
            {"date_of_issue", "2018-06-01"},
            {"organisation", "Yoti"},
            { "structured_postal_address", new Dictionary<string, object> {
                {"address_format" ,  1},
                {"building_number", "64"},
                {"street", "Derwent Road"},
                {"address_line1", "64 Derwent Road"},
                {"address_line2", "London"},
                {"address_line3", "United Kingdom"},
                {"address_line4", "SW20 9NH"},
                {"town_city", "United Kingdom"},
                {"state", "Greater London"},
                {"postal_code", "SW20 9NH"},
                {"country_iso", "GBR"},
                {"country", "United Kingdom"},
                {"formatted_address", "64 Derwent Road\nLondon\nSW20 9NH\nUnited Kingdom"}
            }}
        })
    .Build()
{% /tab %}
{% /code %}

### Check Results

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      Understand the results and the results of the checks . 
   </div>
   <div class="alert-links"> 
      <a href="https://developers.yoti.com/identity-verification/results">Retrieve results</a>
           <a href="https://developers.yoti.com/identity-verification/results#results-of-checks">Results of the checks</a>
   </div>
</div>
{% /html %}

Sandbox will allow you to set a response for each of the checks Identity verification offers. Below are examples of the check result.

### Document Authenticity

Yoti performs a numerous amount of sub checks on the document submitted, in order to simulate this report request you will need to understand the [document report](/identity-verification/document-report). Yoti will provide a recommendation for the authenticity of the document which you can mock using this service.

{% code %}
{% tab language="javascript" %}
const {
  SandboxBreakdownBuilder,
  SandboxRecommendationBuilder,
  SandboxDocumentAuthenticityCheckBuilder
} = require('@getyoti/sdk-sandbox');

const documentAuthenticityCheckConfig = new SandboxDocumentAuthenticityCheckBuilder()
  .withRecommendation(
    new SandboxRecommendationBuilder().withValue('APPROVE').build(),
  )
  .withBreakdowns([
    new SandboxBreakdownBuilder()
      .withSubCheck('data_in_correct_position')
      .withResult('PASS')
      .build(),
    new SandboxBreakdownBuilder()
      .withSubCheck('document_in_date')
      .withResult('PASS')
      .build(),
    new SandboxBreakdownBuilder()
      .withSubCheck('expected_data_present')
      .withResult('PASS')
      .build(),
    new SandboxBreakdownBuilder()
      .withSubCheck('fraud_list_check')
      .withResult('PASS')
      .build(),
    new SandboxBreakdownBuilder()
      .withSubCheck('hologram')
      .withResult('PASS')
      .build(),
    new SandboxBreakdownBuilder()
      .withSubCheck('hologram_movement')
      .withResult('FAIL')
      .build(),
    new SandboxBreakdownBuilder()
      .withSubCheck('no_sign_of_tampering')
      .withResult('PASS')
      .build(),
    new SandboxBreakdownBuilder()
      .withSubCheck('other_security_features')
      .withResult('PASS')
      .build(),
    new SandboxBreakdownBuilder()
      .withSubCheck('real_document')
      .withResult('PASS')
      .build(),
  ])
  .build();
{% /tab %}
{% tab language="java" %}
import com.yoti.api.client.sandbox.docs.request.check.report.SandboxBreakdown;
import com.yoti.api.client.sandbox.docs.request.check.report.SandboxRecommendation;
import com.yoti.api.client.sandbox.docs.request.check.SandboxDocumentAuthenticityCheck;

...
SandboxDocumentAuthenticityCheck documentAuthenticityCheckConfig = SandboxDocumentAuthenticityCheck.builder()
        .withRecommendation(SandboxRecommendation.builder()
                .withValue("APPROVE")
                .build())
        .withBreakdown(SandboxBreakdown.builder()
                .withSubCheck("data_in_correct_position")
                .withResult("PASS")
                .build())
        .withBreakdown(SandboxBreakdown.builder()
                .withSubCheck("document_in_date")
                .withResult("PASS")
                .build())
        .withBreakdown(SandboxBreakdown.builder()
                .withSubCheck("expected_data_present")
                .withResult("PASS")
                .build())
        .withBreakdown(SandboxBreakdown.builder()
                .withSubCheck("fraud_list_check")
                .withResult("PASS")
                .build())
        .withBreakdown(SandboxBreakdown.builder()
                .withSubCheck("hologram")
                .withResult("PASS")
                .build())
        .withBreakdown(SandboxBreakdown.builder()
                .withSubCheck("hologram_movement")
                .withResult("FAIL")
                .build())
        .withBreakdown(SandboxBreakdown.builder()
                .withSubCheck("no_sign_of_tampering")
                .withResult("PASS")
                .build())
        .withBreakdown(SandboxBreakdown.builder()
                .withSubCheck("other_security_features")
                .withResult("PASS")
                .build())
        .withBreakdown(SandboxBreakdown.builder()
                .withSubCheck("real_document")
                .withResult("PASS")
                .build())
        .build();
...
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\Sandbox\DocScan\Request\Check\Report\SandboxBreakdownBuilder;
use Yoti\Sandbox\DocScan\Request\Check\Report\SandboxRecommendationBuilder;
use Yoti\Sandbox\DocScan\Request\Check\SandboxDocumentAuthenticityCheckBuilder;

$documentAuthenticityCheckConfig = (new SandboxDocumentAuthenticityCheckBuilder())
    ->withRecommendation(
        (new SandboxRecommendationBuilder())->withValue('APPROVE')->build()
    )
    ->withBreakdowns([
        (new SandboxBreakdownBuilder())
            ->withSubCheck('data_in_correct_position')
            ->withResult('PASS')
            ->build(),
        (new SandboxBreakdownBuilder())
            ->withSubCheck('document_in_date')
            ->withResult('PASS')
            ->build(),
        (new SandboxBreakdownBuilder())
            ->withSubCheck('expected_data_present')
            ->withResult('PASS')
            ->build(),
        (new SandboxBreakdownBuilder())
            ->withSubCheck('fraud_list_check')
            ->withResult('PASS')
            ->build(),
        (new SandboxBreakdownBuilder())
            ->withSubCheck('hologram')
            ->withResult('PASS')
            ->build(),
        (new SandboxBreakdownBuilder())
            ->withSubCheck('hologram_movement')
            ->withResult('FAIL')
            ->build(),
        (new SandboxBreakdownBuilder())
            ->withSubCheck('no_sign_of_tampering')
            ->withResult('PASS')
            ->build(),
        (new SandboxBreakdownBuilder())
            ->withSubCheck('other_security_features')
            ->withResult('PASS')
            ->build(),
        (new SandboxBreakdownBuilder())
            ->withSubCheck('real_document')
            ->withResult('PASS')
            ->build(),
    ])
    ->build();
{% /tab %}
{% tab language="python" %}
from yoti_python_sandbox.doc_scan.check import (
    SandboxDocumentAuthenticityCheckBuilder,
    SandboxBreakdownBuilder,
    SandboxRecommendationBuilder
)

document_authenticity_check_config = (
    SandboxDocumentAuthenticityCheckBuilder()
    .with_recommendation(
        SandboxRecommendationBuilder()
        .with_value("APPROVE")
        .build()
    )
    .with_breakdowns([
        SandboxBreakdownBuilder()
        .with_sub_check("data_in_correct_position")
        .with_result("PASS")
        .build(),
        SandboxBreakdownBuilder()
        .with_sub_check("document_in_date")
        .with_result("PASS")
        .build(),
        SandboxBreakdownBuilder()
        .with_sub_check("expected_data_present")
        .with_result("PASS")
        .build(),
        SandboxBreakdownBuilder()
        .with_sub_check("fraud_list_check")
        .with_result("PASS")
        .build(),
        SandboxBreakdownBuilder()
        .with_sub_check("hologram")
        .with_result("PASS")
        .build(),
        SandboxBreakdownBuilder()
        .with_sub_check("hologram_movement")
        .with_result("FAIL")
        .build(),
        SandboxBreakdownBuilder()
        .with_sub_check("no_sign_of_tampering")
        .with_result("PASS")
        .build(),
        SandboxBreakdownBuilder()
        .with_sub_check("other_security_features")
        .with_result("PASS")
        .build(),
        SandboxBreakdownBuilder()
        .with_sub_check("real_document")
        .with_result("PASS")
        .build()
    ])
    .build()
)
{% /tab %}
{% tab language="csharp" %}
using System.Collections.Generic;
using System.IO;
using Yoti.Auth;
using Yoti.Auth.Sandbox.DocScan.Request;
using Yoti.Auth.Sandbox.DocScan.Request.Check;
using Yoti.Auth.Sandbox.DocScan.Request.Check.Report;
using Yoti.Auth.Sandbox.DocScan.Request.Task;

var documentAuthenticityCheckConfig = new SandboxDocumentAuthenticityCheckBuilder()
    .WithRecommendation(
    new SandboxRecommendationBuilder()
    .WithValue("APPROVE")
    .Build()
    )
    .WithBreakdown(
    new SandboxBreakdownBuilder()
    .WithSubCheck("data_in_correct_position")
    .WithResult("PASS")
    .Build()
    )
    .WithBreakdown(
    new SandboxBreakdownBuilder()
    .WithSubCheck("document_in_date")
    .WithResult("PASS")
    .Build()
    )
    .WithBreakdown(
    new SandboxBreakdownBuilder()
    .WithSubCheck("expected_data_present")
    .WithResult("PASS")
    .Build()
    )
    .WithBreakdown(
    new SandboxBreakdownBuilder()
    .WithSubCheck("fraud_list_check")
    .WithResult("PASS")
    .Build()
    )
    .WithBreakdown(
    new SandboxBreakdownBuilder()
    .WithSubCheck("hologram")
    .WithResult("PASS")
    .Build()
    )
    .WithBreakdown(
    new SandboxBreakdownBuilder()
    .WithSubCheck("hologram_movement")
    .WithResult("FAIL")
    .Build()
    )
    .WithBreakdown(
    new SandboxBreakdownBuilder()
    .WithSubCheck("no_sign_of_tampering")
    .WithResult("PASS")
    .Build()
    )
    .WithBreakdown(
    new SandboxBreakdownBuilder()
    .WithSubCheck("other_security_features")
    .WithResult("PASS")
    .Build()
    )
    .WithBreakdown(
    new SandboxBreakdownBuilder()
    .WithSubCheck("real_document")
    .WithResult("PASS")
    .Build()
    )
    .Build();
{% /tab %}
{% /code %}

### Data extraction check (ID Document)

Yoti will provide a recommendation for the text data extraction which will contain the sub-check `text_data_readable` which will either be a PASS or a FAIL.

{% code %}
{% tab language="javascript" %}
const {
  SandboxBreakdownBuilder,
  SandboxRecommendationBuilder,
  SandboxDocumentTextDataCheckBuilder
} = require('@getyoti/sdk-sandbox');

const textDataCheckConfig = new SandboxDocumentTextDataCheckBuilder()
  .withRecommendation(
    new SandboxRecommendationBuilder().withValue('APPROVE').build(),
  )
  .withBreakdown(
    new SandboxBreakdownBuilder()
      .withSubCheck('text_data_readable')
      .withResult('PASS')
      .build(),
  )
  .withDocumentFields({
    full_name: 'John Doe',
    nationality: 'GBR',
    date_of_birth: '1986-06-01',
    document_number: '123456789',
  })
  .build();
{% /tab %}
{% tab language="java" %}
import com.yoti.api.client.sandbox.docs.request.check.SandboxDocumentTextDataCheck;
import com.yoti.api.client.sandbox.docs.request.check.report.SandboxBreakdown;
import com.yoti.api.client.sandbox.docs.request.check.report.SandboxRecommendation;

...
SandboxDocumentTextDataCheck textDataCheckConfig = SandboxDocumentTextDataCheck.builder()
        .withRecommendation(SandboxRecommendation.builder().withValue("APPROVE").build())
        .withBreakdown(SandboxBreakdown.builder()
                .withSubCheck("text_data_readable")
                .withResult("PASS")
                .build())
        .withDocumentField("full_name", "John Doe")
        .withDocumentField("nationality", "GBR")
        .withDocumentField("date_of_birth", "1986-06-01")
        .withDocumentField("document_number", "123456789")
        .build();
...
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\Sandbox\DocScan\Request\Check\Report\SandboxBreakdownBuilder;
use Yoti\Sandbox\DocScan\Request\Check\Report\SandboxRecommendationBuilder;
use Yoti\Sandbox\DocScan\Request\Check\SandboxDocumentTextDataCheckBuilder;

$textDataCheckConfig = (new SandboxDocumentTextDataCheckBuilder())
    ->withRecommendation(
        (new SandboxRecommendationBuilder())->withValue('APPROVE')->build()
    )
    ->withBreakdown(
        (new SandboxBreakdownBuilder())
            ->withSubCheck('text_data_readable')
            ->withResult('PASS')
            ->build()
    )
    ->withDocumentFields([
        'full_name' => 'John Doe',
        'nationality' => 'GBR',
        'date_of_birth' => '1986-06-01',
        'document_number' => '123456789',
    ])
    ->build();
{% /tab %}
{% tab language="python" %}
from yoti_python_sandbox.doc_scan.check import (
    SandboxBreakdownBuilder,
    SandboxRecommendationBuilder,
    SandboxDocumentTextDataCheckBuilder
)

text_data_check_config = (
    SandboxDocumentTextDataCheckBuilder()
    .with_recommendation(
        SandboxRecommendationBuilder()
        .with_value("APPROVE")
        .build()
    )
    .with_breakdown(
        SandboxBreakdownBuilder()
        .with_sub_check("text_data_readable")
        .with_result("PASS")
        .build()
    )
    .with_document_field("full_name", "John Doe")
    .with_document_field("nationality", "GBR")
    .with_document_field("date_of_birth", "1986-06-01")
    .with_document_field("document_number", "123456789")
    .build()
)
{% /tab %}
{% tab language="csharp" %}
using System.Collections.Generic;
using System.IO;
using Yoti.Auth;
using Yoti.Auth.Sandbox.DocScan.Request;
using Yoti.Auth.Sandbox.DocScan.Request.Check;
using Yoti.Auth.Sandbox.DocScan.Request.Check.Report;
using Yoti.Auth.Sandbox.DocScan.Request.Task;

var textDataCheckConfig = new SandboxDocumentTextDataCheckBuilder()
    .WithRecommendation(
    new SandboxRecommendationBuilder()
    .WithValue("APPROVE")
    .Build()
    )
    .WithBreakdown(
    new SandboxBreakdownBuilder()
    .WithSubCheck("text_data_readable")
    .WithResult("PASS")
    .Build()
    )
    .WithDocumentFields(
    new Dictionary<string, object> {
        { "full_name","John Doe"},
        { "nationality","GBR"},
        { "date_of_birth","1986-06-01"},
        { "document_number", "123456789"}
    })
    .Build();
{% /tab %}
{% /code %}

### Data extraction check (Supplementary Document)

Similar to ID Document data entry, a Text data check may be generated if a Supplementary document goes for manual data entry. This block would mock the relevant response:

{% code %}
{% tab language="javascript" %}

{% /tab %}
{% tab language="java" %}
// Click to edit code
{% /tab %}
{% tab language="php" %}
// Click to edit code
{% /tab %}
{% tab language="python" %}
// Click to edit code
{% /tab %}
{% tab language="csharp" %}
var supplementaryTextDataCheckConfig = new SandboxSupplementaryDocTextDataCheckBuilder()
	.WithRecommendation(
		new SandboxRecommendationBuilder()
		.WithValue("APPROVE")
		.Build()
	)
	.WithDocumentFields(
		new Dictionary<string, object> {
			{ "full_name", "John Doe"},
			{"date_of_issue", "2018-06-01"},
			{"organisation", "Yoti"},
			{ "structured_postal_address", new Dictionary<string, object> {
				{"address_format" ,  1},
				{"building_number", "64"},
				{"street", "Derwent Road"},
				{"address_line1", "64 Derwent Road"},
				{"address_line2", "London"},
				{"address_line3", "United Kingdom"},
				{"address_line4", "SW20 9NH"},
				{"town_city", "United Kingdom"},
				{"state", "Greater London"},
				{"postal_code", "SW20 9NH"},
				{"country_iso", "GBR"},
				{"country", "United Kingdom"},
				{"formatted_address", "64 Derwent Road\nLondon\nSW20 9NH\nUnited Kingdom"}
			}}
		})
	.Build();
{% /tab %}
{% /code %}

### Liveness

Liveness checks can be retried if failed, depending on specified limited set when generating the session. Each try will generate a new breakdown in the response. The check will either be approved or rejected based on the result of the liveness check which is a pass/fail result. For more information head over to our [production service](/identity-verification/liveness-report).

{% code %}
{% tab language="javascript" %}
const {
  SandboxBreakdownBuilder,
  SandboxRecommendationBuilder,
  SandboxZoomLivenessCheckBuilder,
} = require('@getyoti/sdk-sandbox');

const livenessCheckConfig = new SandboxZoomLivenessCheckBuilder()
  .withRecommendation(
    new SandboxRecommendationBuilder().withValue('APPROVE').build(),
  )
  .withBreakdown(
    new SandboxBreakdownBuilder()
      .withSubCheck('liveness_auth')
      .withResult('PASS')
      .build()
  )
  .build()
{% /tab %}
{% tab language="java" %}
import com.yoti.api.client.sandbox.docs.request.check.SandboxLivenessCheck;
import com.yoti.api.client.sandbox.docs.request.check.report.SandboxBreakdown;
import com.yoti.api.client.sandbox.docs.request.check.report.SandboxRecommendation;

...
SandboxLivenessCheck livenessCheckConfig = SandboxLivenessCheck.forZoomLiveness()
        .withRecommendation(SandboxRecommendation.builder().withValue("APPROVE").build())
        .withBreakdown(SandboxBreakdown.builder()
                .withSubCheck("liveness_auth")
                .withResult("PASS")
                .build())
        .build();
...
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\Sandbox\DocScan\Request\Check\Report\SandboxBreakdownBuilder;
use Yoti\Sandbox\DocScan\Request\Check\Report\SandboxRecommendationBuilder;
use Yoti\Sandbox\DocScan\Request\Check\SandboxZoomLivenessCheckBuilder;

livenessCheckConfig = (new SandboxZoomLivenessCheckBuilder())
    ->withRecommendation(
        (new SandboxRecommendationBuilder())->withValue('APPROVE')->build()
    )
    ->withBreakdown(
        (new SandboxBreakdownBuilder())
            ->withSubCheck('liveness_auth')
            ->withResult('PASS')
            ->build()
    )
    ->build();
{% /tab %}
{% tab language="python" %}
from yoti_python_sandbox.doc_scan.check import (
    SandboxBreakdownBuilder,
    SandboxRecommendationBuilder,
    SandboxZoomLivenessCheckBuilder
)

liveness_check_config = (
    SandboxZoomLivenessCheckBuilder()
    .with_recommendation(
        SandboxRecommendationBuilder()
        .with_value("APPROVE")
        .build()
    )
    .with_breakdown(
        SandboxBreakdownBuilder()
        .with_sub_check("liveness_auth")
        .with_result("PASS")
        .build()
    )
    .build()
)
{% /tab %}
{% tab language="csharp" %}
using System.Collections.Generic;
using System.IO;
using Yoti.Auth;
using Yoti.Auth.Sandbox.DocScan.Request;
using Yoti.Auth.Sandbox.DocScan.Request.Check;
using Yoti.Auth.Sandbox.DocScan.Request.Check.Report;
using Yoti.Auth.Sandbox.DocScan.Request.Task;

var livenessCheckConfig = new SandboxZoomLivenessCheckBuilder()
    .WithRecommendation(
    new SandboxRecommendationBuilder()
    .WithValue("APPROVE")
    .Build()
    )
    .WithBreakdown(
    new SandboxBreakdownBuilder()
    .WithSubCheck("liveness_auth")
    .WithResult("PASS")
    .Build()
    )
    .Build();
{% /tab %}
{% /code %}

### Face Match

The face match check will give a recommendation based on these as either APPROVE or REJECT which can be mocked on sandbox.

A pass/fail result is returned if a manual check is also done, along with a confidence score (between 0 and 1) depending on how successful the match is, Yoti offers a PASS score if the confidence score is over 0.7. or more information head over to our [production service](/identity-verification/face-match-report) documentation.

{% code %}
{% tab language="javascript" title="" %}
const {
  SandboxBreakdownBuilder,
  SandboxRecommendationBuilder,
  SandboxDocumentFaceMatchCheckBuilder,
} = require('@getyoti/sdk-sandbox');

const faceMatchCheckConfig = new SandboxDocumentFaceMatchCheckBuilder()
  .withRecommendation(
    new SandboxRecommendationBuilder().withValue('APPROVE').build(),
  )
  .withBreakdowns([
    new SandboxBreakdownBuilder()
      .withSubCheck('ai_face_match')
      .withResult('FAIL')
      .withDetail('confidence_score', '0.53')
      .build(),
    new SandboxBreakdownBuilder()
      .withSubCheck('manual_face_match')
      .withResult('PASS')
      .build()
  ])
  .build();
{% /tab %}
{% tab language="java" title="" %}
import com.yoti.api.client.sandbox.docs.request.check.SandboxDocumentFaceMatchCheck;
import com.yoti.api.client.sandbox.docs.request.check.report.SandboxBreakdown;
import com.yoti.api.client.sandbox.docs.request.check.report.SandboxRecommendation;

...
SandboxDocumentFaceMatchCheck faceMatchCheckConfig = SandboxDocumentFaceMatchCheck.builder()
                .withRecommendation(SandboxRecommendation.builder().withValue(("APPROVE")).build())
                .withBreakdown(SandboxBreakdown.builder()
                        .withSubCheck("ai_face_match")
                        .withResult("FAIL")
                        .withDetail("confidence_score", "0.53")
                        .build())
                .withBreakdown(SandboxBreakdown.builder()
                        .withSubCheck("manual_face_match")
                        .withResult("PASS")
                        .build())
                .build();
...
{% /tab %}
{% tab language="php" title="" %}
<?php

use Yoti\Sandbox\DocScan\Request\Check\Report\SandboxBreakdownBuilder;
use Yoti\Sandbox\DocScan\Request\Check\Report\SandboxRecommendationBuilder;
use Yoti\Sandbox\DocScan\Request\Check\SandboxDocumentFaceMatchCheckBuilder;

$faceMatchCheckConfig = (new SandboxDocumentFaceMatchCheckBuilder())
    ->withRecommendation(
        (new SandboxRecommendationBuilder())->withValue('APPROVE')->build()
    )
    ->withBreakdowns([
        (new SandboxBreakdownBuilder())
            ->withSubCheck('ai_face_match')
            ->withResult('FAIL')
            ->withDetail('confidence_score', '0.53')
            ->build(),
        (new SandboxBreakdownBuilder())
            ->withSubCheck('manual_face_match')
            ->withResult('PASS')
            ->build()
    ])
    ->build();
{% /tab %}
{% tab language="python" title="" %}
from yoti_python_sandbox.doc_scan.check import (
    SandboxBreakdownBuilder,
    SandboxRecommendationBuilder,
    SandboxDocumentFaceMatchCheckBuilder,
    SandboxDetail
)

face_match_check_config = (
    SandboxDocumentFaceMatchCheckBuilder()
    .with_recommendation(
        SandboxRecommendationBuilder()
        .with_value("APPROVE")
        .build()
    )
    .with_breakdowns([
        SandboxBreakdownBuilder()
        .with_sub_check("ai_face_match")
        .with_result("FAIL")
        .with_detail(
            SandboxDetail("confidence_score", "0.53")
        )
        .build(),
        SandboxBreakdownBuilder()
        .with_sub_check("manual_face_match")
        .with_result("PASS")
        .build()
    ])
    .build()
)
{% /tab %}
{% tab language="csharp" %}
using System.Collections.Generic;
using System.IO;
using Yoti.Auth;
using Yoti.Auth.Sandbox.DocScan.Request;
using Yoti.Auth.Sandbox.DocScan.Request.Check;
using Yoti.Auth.Sandbox.DocScan.Request.Check.Report;
using Yoti.Auth.Sandbox.DocScan.Request.Task;

var faceMatchCheckConfig = new SandboxDocumentFaceMatchCheckBuilder()
    .WithRecommendation(
    new SandboxRecommendationBuilder()
    .WithValue("APPROVE")
    .Build()
    )
    .WithBreakdown(
    new SandboxBreakdownBuilder()
    .WithSubCheck("ai_face_match")
    .WithResult("FAIL")
    .WithDetail(new SandboxDetail("confidence_score", "0.53"))
    .Build()
    )
    .WithBreakdown(
    new SandboxBreakdownBuilder()
    .WithSubCheck("manual_face_match")
    .WithResult("PASS")
    .Build()
    )
    .Build();
{% /tab %}
{% /code %}

---

## Completing the session

Once you have set your sandbox response config, you will need to complete the session for Identity verification. This will populate the media and will complete the session.

The Agent endpoint /agent uses the SDK ID and .PEM file for authorisation. 

{% code %}
{% tab language="http" %}
POST https://api.yoti.com/sandbox/idverify/v1/agent

AUTH: X-Yoti-Auth-Digest
BODY: {See below}
{% /tab %}
{% /code %}

{% code %}
{% tab language="http" %}
POST https://api.yoti.com/sandbox/idverify/v1/agent

AUTH: X-Yoti-Auth-Digest
BODY: {See below}
{% /tab %}
{% tab language="php" %}
<?php
use Yoti\Http\RequestBuilder;
use Yoti\Http\Payload;

$request = (new RequestBuilder())
   	  ->withBaseUrl('https://api.yoti.com/idverify/v1')
    	->withPemFilePath('<YOTI_KEY_FILE_PATH>')
    	->withEndpoint('/agent')
    	->withPayload(Payload::fromJsonData(BODY))
			->withMethod('POST')
    	->withQueryParam('sdkId', '<YOTI_CLIENT_SDK_ID>')
    	->build()

    	//get Yoti Response
  	->execute();
code
{% /tab %}
{% tab language="csharp" title=".NET" %}
using System;
using System.IO;
using System.Net.Http;
using System.Text;
using Microsoft.AspNetCore.Mvc;
using Yoti.Auth.Web;

HttpClient httpClient = new HttpClient();
StreamReader privateKeyStream = System.IO.File.OpenText(_pemFilePath);

string serializedRequest = Newtonsoft.Json.JsonConvert.SerializeObject(new
{
	BODY
});

byte[] byteContent = Encoding.UTF8.GetBytes(serializedRequest);

Uri _baseUrl = new UriBuilder("https", "api.yoti.com", "sandbox/idverify/v1").Uri;

Yoti.Auth.Web.Request ageScanRequest = new RequestBuilder()
  .WithStreamReader(privateKeyStream)
  .WithBaseUri(_baseUrl)
  .WithEndpoint("/agent")
  .WithHttpMethod(HttpMethod.Post)
  .WithContent(byteContent)
  .WithQueryParam("X-Yoti-Auth-Id", _clientSdkId)
  .Build();

HttpResponseMessage response = ageScanRequest.Execute(httpClient).Result;
{% /tab %}
{% /code %}

### Body

{% code %}
{% tab language="json" %}
{
  "session_id": "UUIDstring",
  "client_session_token": "UUIDstring",
  "resources": {
    "id_documents": [
      {
        "issuing_country": "GBR",
        "document_type": "string",
        "capture_method": "CAMERA"
      },
   {
        "issuing_country": "GBR",
        "document_type": "string",
        "capture_method": "CAMERA"
      }

    ],
    "supplementary_documents": [
      {
        "issuing_country": "GBR",
        "document_type": "string"
      }
    ]
  }
}
{% /tab %}
{% /code %}

{% table %}
| **Field** | **Details** | 
| ---- | ---- | 
| Session ID | The UUID String returned when creating the session | 
| Client Session Token | The UUID String returned when creating the session | 
| Resources | This should match any filters you have set up in the session configuration | 
| Issuing Country | 3-letter ISO code string | 
| Document Type | String eg PASSPORT, DRIVING_LICENCE | 
{% /table %}

### Responses

{% table %}
| **Code** | **Desciption** | 
| ---- | ---- | 
| 204 | OK, completed with no content | 
| 400 | Invalid payload | 
| 401 | Unauthorized | 
| 500 | Server Error | 
| 503 | Temporarily Unavailable | 
{% /table %}

## Retrieving images and user information

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
     Understand how to retrieve the images in production.
   </div>
   <div class="alert-links"> 
      <a href="https://developers.yoti.com/identity-verification/results#retrieve-images">Retrieve Images</a>
   </div>
</div>
{% /html %}

Retrieving the media response is the same as production. Please ensure your base URL is updated to the below:

{% code %}
{% tab language="http" %}
https://api.yoti.com/sandbox/idverify/v1
{% /tab %}
{% /code %}

For further details, please see [Understanding the report.](https://developers.yoti.com/identity-verification/understanding-the-report)