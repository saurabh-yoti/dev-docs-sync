---
type: page
title: AML Check
listed: false
slug: aml
description: 
index_title: AML Check
hidden: 
keywords: 
tags: 
---

Yoti provides an AML (Anti-Money Laundering) check service to allow a deeper KYC process to prevent fraud.

{% html %}
<div class="alert-BYS">

   <div class="alert-title" id="BYS">

      Before you start

   </div>

   <div class="alert-text" >

  Make sure your application is assigned to your organisation in Yoti Hub.

   </div>

   <div class="alert-links"> 

         <a href="https://developers.yoti.com/yoti/welcome#creating-a-yoti-application">Create an application</a>

   </div>

</div>
{% /html %}

### Yoti will provide a boolean result on the following checks:

- PEP list:- Verify against Politically Exposed Persons list.
- Fraud list:- Verify against US Social Security Administration Fraud (SNN Fraud) list.
- Watch list:- Verify against watch lists from the Office of Foreign Assets Control

---

## AML data required

{% html %}
<div class="alert-GTK">

    <div class="alert-title" id="GTK">

       Important information

    </div>

    <div class="alert-text">

      Performing an AML check on a person requires their consent. You must ensure you have user consent before using this service.
    </div>


</div>
{% /html %}

For an AML check you will need to provide the following data provided:–

{% table %}
| Data | Source | 
| ---- | ---- | 
| First name | Yoti | 
| Family name | Yoti | 
| Country of residence (must be an ISO 3166 3-letter code). | Manually | 
| Social Security Number (US citizens only). | Manually | 
| Postcode/Zip code (US citizens only) | Yoti | 
{% /table %}

{% html %}
<div class="alert-know">
    <div class="alert-title" id="know">
        Knowledge base
    </div>
    <div class="alert-text">
For information on Yoti attributes please head over to the User Profile section    </div>
    <div class="alert-links"> 
       <a href="">User Profile</a>
 
    </div>
</div>
{% /html %}

---

## Integrate AML

### Install Yoti SDK

The Yoti SDKs are available via popular dependency management systems. Further details can be found on the pages of the specific projects.

To install the Yoti SDK using NPM:

{% code %}
{% tab language="javascript" %}
npm install -S -E yoti
{% /tab %}
{% tab language="java" %}
// If you are using Maven, add the following dependency:
<dependency>
    <groupId>com.yoti</groupId>
    <artifactId>yoti-sdk-impl</artifactId>
    <version>2.6.0</version>
</dependency>

// If you are using Gradle, add the following dependency:
compile group: 'com.yoti', name: 'yoti-sdk-impl', version: ‘2.6.0'
{% /tab %}
{% tab language="php" %}
// Get the Yoti PHP SDK library via a Composer package
composer require yoti/yoti-php-sdk
{% /tab %}
{% tab language="python" %}
pip install yoti
{% /tab %}
{% tab language="csharp" %}
// Click to edit c// To install the Yoti NuGet package you will need to install NuGet.
// To import the latest Yoti SDK into your project, enter the following
// command from NuGet Package Manager Console in Visual Studio:

Install-Package Yoti

// For other installation methods, see https://www.nuget.org/packages/Yotiode
{% /tab %}
{% /code %}

Once you have added the Yoti SDK dependency to your project, it’s time to initialise a Yoti client as shown in the code snippet below.

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
Important information
    </div>
    <div class="alert-text">
For Information on where to get your API keys from please head to the hub.
          </div>
  
  <div class="alert-links"> 
       <a href="https://developers.yoti.com/yoti/getting-started-hub">Generate API Keys</a>

    </div>
</div>
{% /html %}

{% code %}
{% tab language="javascript" %}
const path = require('path');
const fs = require("fs");

const {
    DocScanClient,
    SessionSpecificationBuilder,
    RequestedDocumentAuthenticityCheckBuilder,
    RequestedTextExtractionTaskBuilder,
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
// Click to edit code
{% /tab %}
{% /code %}

## AML Check

Please see below for code snippets of the AML check configuration:-

{% code %}
{% tab language="javascript" %}
// Performing an AML check for a US resident

let amlAddress = new Yoti.AmlAddress('USA', '10118');
let amlProfile = new Yoti.AmlProfile('Hunter Avery', 'McCreedy', amlAddress, '121341234');
// Performing an AML check outside of the US
let amlAddress = new Yoti.AmlAddress('GBR');
let amlProfile = new Yoti.AmlProfile('Edward Rupert', 'Taylor', amlAddress);
yotiClient.performAmlCheck(amlProfile).then((amlResult) => {
  console.log(amlResult.isOnPepList);
  console.log(amlResult.isOnFraudList);
  console.log(amlResult.isOnWatchList);
  // Or
  console.log(amlResult);
}).catch((err) => {
  console.error(err);
})
{% /tab %}
{% tab language="java" %}
// Performing an AML check for a US resident
AmlAddress amlAddress = new AmlAddressBuilder()
                            .withPostcode("10118")
                            .withCountry("USA")
                            .build();

AmlProfile amlProfile = new AmlProfileBuilder()
                            .withGivenNames("Hunter Avery")
                            .withFamilyName("McCreedy")
                            .withSsn("121341234")
                            .withAddress(amlAddress)
                            .build();

// Perform the check
AmlResult amlResult = client.performAmlCheck(amlProfile); // where client is the initialised Yoti Client

// Result returned in a POJO
System.out.println(amlResult.isOnFraudList());
System.out.println(amlResult.isOnWatchList());
System.out.println(amlResult.isOnPepList());
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\Entity\Country;
use Yoti\Entity\AmlAddress;
use Yoti\Entity\AmlProfile;
// Performing an AML check for a US resident
$amlAddress = new AmlAddress(new Country('USA'), '10118');
$amlProfile = new AmlProfile('Hunter Avery', 'McCreedy', amlAddress, '121341234');
// Performing an AML check outside of the US
$amlAddress = new AmlAddress(new Country('GBR'));
$amlProfile = new AmlProfile('Edward Rupert', 'Taylor', amlAddress);
$amlResult = $yotiClient->performAmlCheck($amlProfile);
var_dump($amlResult->isOnPepList());
var_dump($amlResult->isOnFraudList());
var_dump($amlResult->isOnWatchList());
// Or
echo $amlResult;
{% /tab %}
{% tab language="python" %}
from yoti_python_sdk import aml
from yoti_python_sdk import Client
# Performing an AML check for a US resident
aml_address = aml.AmlAddress("USA", "10118")
aml_profile = aml.AmlProfile("Hunter Avery", "McCreedy", aml_address, "121341234")
# Performing an AML check outside of the US
aml_address = aml.AmlAddress("GBR")
aml_profile = aml.AmlProfile("Edward Rupert", "Taylor", aml_address)
aml_result = yotiClient.perform_aml_check(aml_profile)
print("AML Result for {0} {1}:".format(given_names, family_name))
print("On PEP list: " + str(aml_result.on_pep_list))
print("On fraud list: " + str(aml_result.on_fraud_list))
print("On watchlist: " + str(aml_result.on_watch_list))
{% /tab %}
{% tab language="csharp" %}
// Performing an AML check for a US resident

AmlAddress amlAddress = new AmlAddress(
   country: "USA",
   postCode: "10118");
AmlProfile amlProfile = new AmlProfile(
    givenNames: "Hunter Avery",
    familyName: "McCreedy",
    ssn: "121341234",
    amlAddress: amlAddress);
// Performing an AML check outside of the US
AmlAddress amlAddress = new AmlAddress(
   country: "GBR");
AmlProfile amlProfile = new AmlProfile(
    givenNames: "Edward Rupert",
    familyName: "Taylor",
    amlAddress: amlAddress);
AmlResult amlResult = yotiClient.PerformAmlCheck(amlProfile);
bool onPepList = amlResult.IsOnPepList();
bool onFraudList = amlResult.IsOnFraudList();
bool onWatchList = amlResult.IsOnWatchList();
{% /tab %}
{% /code %}

To see the data that is obtained from a Doc Scan request please see the user profile section.