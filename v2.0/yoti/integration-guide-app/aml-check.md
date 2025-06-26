---
type: page
title: AML check
listed: false
slug: aml-check
description: 
index_title: AML check
hidden: 
keywords: 
tags: 
---

Yoti provides an AML (Anti-Money Laundering) check service to allow a deeper KYC process to prevent fraud. This is a chargeable service, so please contact [sdksupport@yoti.com](mailto:sdksupport@yoti.com) for more information.

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
Make sure your application is assigned to your organisation in Yoti Hub.
   </div>
   <div class="alert-links"> 
      <a  target="_self" href="https://developers.yoti.com/yoti/generating-the-api-keys#creating-a-yoti-application"> Create an application </a>
   </div>
</div>
{% /html %}

### AML check types

Yoti will provide a boolean result on the following checks:

- PEP list:- Verify against Politically Exposed Persons list.
- Fraud list:- Verify against US Social Security Administration Fraud (SNN Fraud) list.
- Watch list:- Verify against watch lists from the Office of Foreign Assets Control.

---

## What you need to provide

For an AML check you will need to provide the following:

- Data provided by Yoti – please ensure you have selected the Given name(s) and Family name attributes from the Data tab in Yoti Hub.
- Given name(s).
- Family name.

---

## Data from the user

Data that must be collected from the user:

- Country of residence (must be an ISO 3166 3-letter code).
- Social Security Number (US citizens only).
- Postcode/Zip code (US citizens only)

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

---

## Performing a check

Install Yoti SDK

{% code %}
{% tab language="javascript" %}
npm install -S -E yoti
{% /tab %}
{% tab language="ruby" %}
gem install yoti

# The gem provides a configuration generator for Ruby on Rails:
rails generate yoti:install
{% /tab %}
{% tab language="php" %}
// Get the Yoti PHP SDK library via a Composer package
composer require yoti/yoti-php-sdk
{% /tab %}
{% tab language="python" %}
pip install yoti
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
{% tab language="go" %}
// As of version 2.4.0, modules are used. This means it's not necessary to get a copy or fetch all dependencies 
// as instructed below, as the Go toolchain will fetch them as necessary. 
// You can simply add a `require github.com/getyoti/yoti-go-sdk/v2` to go.mod.
// To download and install the Yoti SDK and its dependencies, run the following command from your terminal:

go get "github.com/getyoti/yoti-go-sdk/v2”
{% /tab %}
{% tab language="csharp" %}
// To install the Yoti NuGet package you will need to install NuGet.
// To import the latest Yoti SDK into your project, enter the following
// command from NuGet Package Manager Console in Visual Studio:

Install-Package Yoti

// For other installation methods, see https://www.nuget.org/packages/Yoti
{% /tab %}
{% /code %}

Initialise Yoti client

{% code %}
{% tab language="javascript" %}
const yoti = require('yoti')
const CLIENT_SDK_ID = 'YOTI_CLIENT_SDK_ID'
const PEM_PATH = 'YOTI_KEY_FILE_PATH'
const PEM_KEY = fs.readFileSync(PEM_PATH)
// For SDK version < 3
const yotiClient = new yoti(CLIENT_SDK_ID, PEM)
// For SDK version >= 3
const yotiClient = new yoti.Client(CLIENT_SDK_ID, PEM_KEY)
{% /tab %}
{% tab language="ruby" %}
Yoti.configuration do |c|
  c.yoti_client_sdk_id = ENV['YOTI_CLIENT_SDK_ID']
  c.yoti_key_file_path = ENV['YOTI_KEY_FILE_PATH']
end
# or
Yoti.configuration do |c|
  c.yoti_client_sdk_id = ENV['YOTI_CLIENT_SDK_ID']
  c.yoti_key = ENV['YOTI_KEY']
end
# Where *YOTI_KEY* is an environment variable that stores the content of the secret key:
# YOTI_KEY="-----BEGIN RSA PRIVATE KEY-----\nMIIEp…"
{% /tab %}
{% tab language="php" %}
<?php
require_once './vendor/autoload.php';
$client = new \Yoti\YotiClient('YOTI_CLIENT_SDK_ID', 'YOTI_KEY_FILE_PATH');
{% /tab %}
{% tab language="python" %}
from yoti_python_sdk import Client

client = Client(YOTI_CLIENT_SDK_ID, YOTI_KEY_FILE_PATH)
{% /tab %}
{% tab language="java" %}
import java.io.File;
import com.yoti.api.client.ActivityDetails;
import com.yoti.api.client.Date;
import com.yoti.api.client.FileKeyPairSource;
import com.yoti.api.client.HumanProfile;
import com.yoti.api.client.HumanProfile.Gender;
import com.yoti.api.client.Image;
import com.yoti.api.client.YotiClient;
import com.yoti.api.client.YotiClientBuilder;

YotiClient client = YotiClientBuilder.newInstance()
    .forApplication(<YOTI_CLIENT_SDK_ID>)
    .withKeyPair(FileKeyPairSource.fromFile(new File("<YOTI_KEY_FILE_PATH>")))
    .build();
{% /tab %}
{% tab language="go" %}
sdkID := "YOTI_CLIENT_SDK_ID";
key, _ := ioutil.ReadFile("YOTI_KEY_FILE_PATH")

client := yoti.Client{
    SdkID: sdkID,
    Key: key}
{% /tab %}
{% tab language="csharp" %}
const string SDK_ID = "YOTI_CLIENT_SDK_ID";
const string PEM_PATH = "YOTI_KEY_FILE_PATH";

var privateKeyStream = System.IO.File.OpenText(PEM_PATH);
var yotiClient = new YotiClient(SDK_ID, privateKeyStream);
{% /tab %}
{% /code %}

Perform check

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
{% tab language="ruby" %}
// Cl# Performing an AML check for a US resident
aml_address = Yoti::AmlAddress.new('USA', '10118')
aml_profile = Yoti::AmlProfile.new('Hunter Avery', 'McCreedy', aml_address, '121341234')
# Performing an AML check outside of the US
aml_address = Yoti::AmlAddress.new('GBR')
aml_profile = Yoti::AmlProfile.new('Edward Rupert', 'Taylor', aml_address)
puts Yoti::Client.aml_check(aml_profile)ick to edit code
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
{% tab language="go" %}
// Performing an AML check for a US resident
amlAddress := yoti.AmlAddress{
    Country:  "USA",
    PostCode: "10118"}
amlProfile := yoti.AmlProfile{
    GivenNames: "Hunter Avery",
    FamilyName: "McCreedy",
    Ssn:        "121341234",
    Address:    amlAddress}
// Performing an AML check outside of the US
amlAddress := yoti.AmlAddress{
    Country: "GBR"}
amlProfile := yoti.AmlProfile{
    GivenNames: "Edward Rupert",
    FamilyName: "Taylor",
    Address:    amlAddress}
result, err := client.PerformAmlCheck(amlProfile)
log.Printf("AML Result for %s %s:", givenNames, familyName)
log.Printf("On PEP list: %s", strconv.FormatBool(result.OnPEPList))
log.Printf("On Fraud list: %s", strconv.FormatBool(result.OnFraudList))
log.Printf("On Watch list: %s", strconv.FormatBool(result.OnWatchList))
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

---

## AML Sandbox

AML functionality can be tested through our sandbox environment. First generate a sandbox key as described in [auto$](/yoti/generate-sandbox-api-keys).

To generate a positive result, specify the name of the check to trigger inside of 'given names'. To generate multiple positive results, concatenate the check name without a space as shown below.

Install Yoti SDK

{% code %}
{% tab language="javascript" %}
npm install -S -E yoti
{% /tab %}
{% tab language="ruby" %}
gem install yoti

# The gem provides a configuration generator for Ruby on Rails:
rails generate yoti:install
{% /tab %}
{% tab language="php" %}
// Get the Yoti PHP SDK library via a Composer package
composer require yoti/yoti-php-sdk
{% /tab %}
{% tab language="python" %}
pip install yoti
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
{% tab language="go" %}
// As of version 2.4.0, modules are used. This means it's not necessary to get a copy or fetch all dependencies 
// as instructed below, as the Go toolchain will fetch them as necessary. 
// You can simply add a `require github.com/getyoti/yoti-go-sdk/v2` to go.mod.
// To download and install the Yoti SDK and its dependencies, run the following command from your terminal:

go get "github.com/getyoti/yoti-go-sdk/v2”
{% /tab %}
{% tab language="csharp" %}
// To install the Yoti NuGet package you will need to install NuGet.
// To import the latest Yoti SDK into your project, enter the following
// command from NuGet Package Manager Console in Visual Studio:

Install-Package Yoti

// For other installation methods, see https://www.nuget.org/packages/Yoti
{% /tab %}
{% /code %}

Initialise **Sandbox** Yoti client

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
To avoid accumulating a cost the Yoti API needs to be updated to point to the sandbox URL. This is language specific and involves passing the sandbox api URL to the Yoti client. For further details on our Yoti sandbox, see our respective sandbox repositories.
    </div>
    <div class="alert-links"> 
        <a target="_self" href="https://developers.yoti.com/yoti/sandbox-app#supported-languages">App Sandbox</a>
   </div>
</div>
{% /html %}

{% code %}
{% tab language="javascript" %}
const yoti = require('yoti')
const SANDBOX_CLIENT_SDK_ID = 'SANDBOX_CLIENT_SDK_ID'
const PEM_PATH = 'YOTI_KEY_FILE_PATH'
const PEM_KEY = fs.readFileSync(PEM_PATH)
// For SDK version < 3
const yotiClient = new yoti(SANDBOX_CLIENT_SDK_ID, PEM)
// For SDK version >= 3
const yotiClient = new yoti.Client(SANDBOX_CLIENT_SDK_ID, PEM_KEY)

/*
Point the Yoti client at the sandbox by setting environment variable YOTI_CONNECT_API to https://api.yoti.com/sandbox/v1
*/
{% /tab %}
{% tab language="ruby" %}
Yoti.configuration do |c|
  c.yoti_client_sdk_id = ENV['SANDBOX_CLIENT_SDK_ID']
  c.yoti_key_file_path = ENV['YOTI_KEY_FILE_PATH']
  C.api_endpoint = 'https://api.yoti.com/sandbox/v1'
end
# or
Yoti.configuration do |c|
  c.yoti_client_sdk_id = ENV['SANDBOX_CLIENT_SDK_ID']
  c.yoti_key = ENV['YOTI_KEY']
  C.api_endpoint = 'https://api.yoti.com/sandbox/v1'
end
# Where *YOTI_KEY* is an environment variable that stores the content of the secret key:
# YOTI_KEY="-----BEGIN RSA PRIVATE KEY-----\nMIIEp…"
{% /tab %}
{% tab language="php" %}
<?php
require_once './vendor/autoload.php';
$client = new \Yoti\YotiClient('SANDBOX_CLIENT_SDK_ID', 'YOTI_KEY_FILE_PATH', [
    'api.url' => 'https://api.yoti.com/sandbox/v1'
]);
{% /tab %}
{% tab language="python" %}
from yoti_python_sdk import Client

client = Client(SANDBOX_CLIENT_SDK_ID, YOTI_KEY_FILE_PATH, api_url="https://api.yoti.com/sandbox/v1")
{% /tab %}
{% tab language="java" %}
import java.io.File;
import com.yoti.api.client.ActivityDetails;
import com.yoti.api.client.Date;
import com.yoti.api.client.FileKeyPairSource;
import com.yoti.api.client.HumanProfile;
import com.yoti.api.client.HumanProfile.Gender;
import com.yoti.api.client.Image;
import com.yoti.api.client.YotiClient;
import com.yoti.api.client.YotiClientBuilder;

YotiClient client = YotiClientBuilder.newInstance()
    .forApplication(<SANDBOX_CLIENT_SDK_ID>)
    .withKeyPair(FileKeyPairSource.fromFile(new File("<YOTI_KEY_FILE_PATH>")))
    .build();

// Point the system sandbox
// System.setProperty("yoti.api.url", "https://api.yoti.com/sandbox/v1");
// -Dyoti.api.url=https://api.yoti.com/sandbox/v1
{% /tab %}
{% tab language="go" %}
sdkID := "SANDBOX_CLIENT_SDK_ID";
key, _ := ioutil.ReadFile("YOTI_KEY_FILE_PATH")

client := yoti.Client{
    SdkID: sdkID,
    Key: key}

client.OverrideAPIURL("https://api.yoti.com/sandbox/v1")
{% /tab %}
{% tab language="csharp" %}
Org.BouncyCastle.Crypto.AsymmetricCipherKeyPair keyPair;

const string sandboxClientSdkid = "SANDBOX_CLIENT_SDK_ID";
const string PEM_PATH = "YOTI_KEY_FILE_PATH";

using (StreamReader stream = File.OpenText(PEM_PATH))
{
	keyPair = Yoti.Auth.CryptoEngine.LoadRsaKey(stream);
}

var yotiClient = new YotiClient(new HttpClient(), sandboxClientSdkid, keyPair);

Uri sandboxUri = new UriBuilder(
	"https",
	"api.yoti.com",
	443,
	"sandbox/v1").Uri;

yotiClient.OverrideApiUri(sandboxUri);
{% /tab %}
{% /code %}

Perform test AML check in sandbox

{% code %}
{% tab language="javascript" %}
// Performing an AML check for a US resident

let amlAddress = new Yoti.AmlAddress('USA', '10118');
let amlProfile = new Yoti.AmlProfile('fraudwatchpep', 'McCreedy', amlAddress, '121341234');
// Performing an AML check outside of the US
let amlAddress = new Yoti.AmlAddress('GBR');
let amlProfile = new Yoti.AmlProfile('fraudwatchpep', 'Taylor', amlAddress);
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
{% tab language="ruby" %}
// Cl# Performing an AML check for a US resident
aml_address = Yoti::AmlAddress.new('USA', '10118')
aml_profile = Yoti::AmlProfile.new('fraudwatchpep', 'McCreedy', aml_address, '121341234')
# Performing an AML check outside of the US
aml_address = Yoti::AmlAddress.new('GBR')
aml_profile = Yoti::AmlProfile.new('fraudwatchpep', 'Taylor', aml_address)
puts Yoti::Client.aml_check(aml_profile)ick to edit code
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\Entity\Country;
use Yoti\Entity\AmlAddress;
use Yoti\Entity\AmlProfile;
// Performing an AML check for a US resident
$amlAddress = new AmlAddress(new Country('USA'), '10118');
$amlProfile = new AmlProfile('fraudwatchpep', 'McCreedy', amlAddress, '121341234');
// Performing an AML check outside of the US
$amlAddress = new AmlAddress(new Country('GBR'));
$amlProfile = new AmlProfile('fraudwatchpep', 'Taylor', amlAddress);
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
aml_profile = aml.AmlProfile("fraudwatchpep", "McCreedy", aml_address, "121341234")
# Performing an AML check outside of the US
aml_address = aml.AmlAddress("GBR")
aml_profile = aml.AmlProfile("fraudwatchpep", "Taylor", aml_address)
aml_result = yotiClient.perform_aml_check(aml_profile)
print("AML Result for {0} {1}:".format(given_names, family_name))
print("On PEP list: " + str(aml_result.on_pep_list))
print("On fraud list: " + str(aml_result.on_fraud_list))
print("On watchlist: " + str(aml_result.on_watch_list))
{% /tab %}
{% tab language="java" %}
// Performing an AML check for a US resident
AmlAddress amlAddress = new AmlAddressBuilder()
                            .withPostcode("10118")
                            .withCountry("USA")
                            .build();

AmlProfile amlProfile = new AmlProfileBuilder()
                            .withGivenNames("fraudwatchpep")
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
{% tab language="go" %}
// Performing an AML check for a US resident
amlAddress := yoti.AmlAddress{
    Country:  "USA",
    PostCode: "10118"}
amlProfile := yoti.AmlProfile{
    GivenNames: "fraudwatchpep",
    FamilyName: "McCreedy",
    Ssn:        "121341234",
    Address:    amlAddress}
// Performing an AML check outside of the US
amlAddress := yoti.AmlAddress{
    Country: "GBR"}
amlProfile := yoti.AmlProfile{
    GivenNames: "fraudwatchpep",
    FamilyName: "Taylor",
    Address:    amlAddress}
result, err := client.PerformAmlCheck(amlProfile)
log.Printf("AML Result for %s %s:", givenNames, familyName)
log.Printf("On PEP list: %s", strconv.FormatBool(result.OnPEPList))
log.Printf("On Fraud list: %s", strconv.FormatBool(result.OnFraudList))
log.Printf("On Watch list: %s", strconv.FormatBool(result.OnWatchList))
{% /tab %}
{% tab language="csharp" %}
// Performing an AML check for a US resident

AmlAddress amlAddress = new AmlAddress(
   country: "USA",
   postCode: "10118");
AmlProfile amlProfile = new AmlProfile(
    givenNames: "fraudwatchpep",
    familyName: "McCreedy",
    ssn: "121341234",
    amlAddress: amlAddress);
// Performing an AML check outside of the US
AmlAddress amlAddress = new AmlAddress(
   country: "GBR");
AmlProfile amlProfile = new AmlProfile(
    givenNames: "fraudwatchpep",
    familyName: "Taylor",
    amlAddress: amlAddress);
AmlResult amlResult = yotiClient.PerformAmlCheck(amlProfile);
bool onPepList = amlResult.IsOnPepList();
bool onFraudList = amlResult.IsOnFraudList();
bool onWatchList = amlResult.IsOnWatchList();
{% /tab %}
{% /code %}