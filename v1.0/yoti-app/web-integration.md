---
type: page
title: Web Integration
listed: true
slug: web-integration
description: 
index_title: Web Integration
hidden: 
keywords: 
tags: 
---

The web integration process involves five simple steps:

1. [Creating an organisation](/yoti-app/web-integration#step-1-creating-an-organisation)
2. [Creating an application](/yoti-app/web-integration#step-2-creating-an-application)
3. [Front-end integration](/yoti-app/web-integration#step-3-front-end-integration)
4. [Installing the SDK](/yoti-app/web-integration#step-4-installing-the-sdk)
5. [Retrieving a profile](/yoti-app/web-integration#step-5-retrieving-a-profile)

Yoti is an identity checking platform that allows organisations to verify who people are, online and in person. For consumers, it’s an app that helps them prove who they are and verify the identities of others.

This document will guide you through the configuration and implementation steps that are necessary in order for your back-end to be able to retrieve a user profile and complete a Yoti share flow. The image below describes the login process and how your back-end integrates with the Yoti architecture.

{% image url="https://image-archive.developerhub.io/image/upload/12870/j5aji8dciamlodmziekk/1557841032.png" mode="responsive" height="1504" width="1244" %}
{% /image %}

Yoti provides a set of SDKs that take care of fetching user profiles from our servers. After a user scans your app’s QR code, Yoti provides a one time use token to your back-end. Your back-end can use that token with the SDK to fetch the user profile from the Yoti servers.

---

## Integration steps

Let’s get started on integrating Yoti with your site!

First, you will need to have the free Yoti app on your phone. If you haven’t got it already, you can find it on both the [App Store](https://itunes.apple.com/gb/app/yoti-your-digital-identity-app/id983980808) and [Google Play](https://play.google.com/store/apps/details?id=com.yoti.mobile.android.live).

## Step 1: Creating an organisation

Open the Yoti app on your phone, tap Scan Code and scan the QR code displayed on your desktop screen via the following url: [https://hub.yoti.com/login-organisations](https://hub.yoti.com/login-organisations)

Once there, you will need to fill out a basic form with the following questions:

- Organisation details as shown on the company register for your jurisdiction. This is required for us to verify your company
- Registered company address. This is required as additional verification and to generate a billing address
- Director information. This will consist of the directors full name and email address for verification
- Yoti terms and conditions. If you require a copy of this please contact [onboarding@yoti.com](mailto:onboarding@yoti.com)
- Billing details

Your organisation is now created. Our onboarding team will review your application and be in touch within 2-3 hours during office hours on the status of your application. However, this will not prevent you from starting your integration.

Check out the video below to see how to create an organisation:

{% video %}
{% /video %}

## Step 2: Creating an application

Once you have created your organisation, the next step is to create an application. Head over to [https://hub.yoti.com/login](https://hub.yoti.com/login) on your desktop computer and follow the next steps.

### **_Log in to Yoti Hub_**

To log in, open the Yoti app on your phone, tap `Scan Code` and scan the QR code displayed on your desktop computer.

If you are an organisation please navigate to your organisation page rather than your personal account.

_Please note: Once you have logged in to Yoti Hub, your phone will show a ‘connected’ screen. To keep your data secure, we make sure that only your phone can decipher it. For this reason, you’ll need to keep the Yoti app active whilst you are using Yoti Hub. If you leave the Yoti app, you will need to log in again._

_**Creating your application**_

To create your application, head over to the Applications tab on the side menu. If this is your first time creating an application, you will see a short explanation and a Get started button.

### [**_Details tab_**](https://yoti-developer-documentation.developerhub.io/yoti-hub/yoti-dashboard#details-tab)

Please fill out your details, Your Application name and logo will be shown on the share screen in the Yoti app. Once you have finished filling out your details click the Create button. You will see a notification when this is successful. After completing the details tab, you’ll need to provide information in the other tabs.

### **_Scenarios tab_**

Scenarios allow you to define different sets of attributes to request from your users, while still using one application. The attributes to request will be defined by the QR code that the user scans when they connect to the app. You control the set of attributes to request by specifying a Scenario ID to use at the start of the user journey. Each individual user is uniquely identifiable by their Remember Me ID, allowing them to be linked across multiple journeys regardless of the scenario each journey has used.

An application will have a single Application ID, Client SDK ID and .pem file, but may use different a Scenario ID for each journey you wish to define.

You will be given your Scenario ID once you activate your app. You will see your Scenario IDs in the scenarios list.

- Scenario ID: This is used to associate the button generator with the appropriate scenario that you wish to use.

**_Keys tab_**

Contains the various IDs and the key pair for your application.

- Application ID: This is required for the Yoti button that you’ll add to your web app’s front end code.
- Yoti Client SDK ID: You will need this on your back­end to initialise the SDK and it is passed in each call to our servers.

You need to download the PEM file containing your private key in order for your app to connect with Yoti. Just click the Generate key pair button in the keys tab to download it. Please keep this safe as this PEM file is essential to Yoti integration. If you lose or corrupt your PEM file you will be able to generate a new one. Remember, regenerating your key pair will break your current application by invalidating your current PEM file and generated keys. This means you will be unable to decrypt new tokens until these are replaced by the newly-generated ones.

### **_Activating your application_**

Once you have completed the above steps, you will be able to activate your Yoti application by clicking the activate button in the dropdown menu in the top right.

---

## Step 3: Front-end integration

You will need to provide a button to allow your users to authenticate with Yoti. Upon clicking this button, we will open a modal view, which contains a QR code for users to scan with their Yoti app on their smartphone. Note that mobile web users will skip the QR code scanning step, as they use the Yoti mobile app directly to authenticate.

Yoti provides a button generator for you to use for this purpose. In order to use the button generator, you will need to include the script in your HTML file. In the accompanying example, the button generator script has been added to the head of the html document. 

This JavaScript library currently needs to be invoked - do this by calling `Yoti.Share.init()` in the body of your HTML document. For the config, you will need to specify a ‘domId’ so we know where we need to add the Yoti button on your page and the ‘scenarioId’ that is being provided by Yoti Hub after creating an application.

The Yoti button requires the hosting page to be accessed via HTTPS, so please make sure that your web application has HTTPS enabled. Finally, the domain port pair where the button is deployed (for example [https://localhost:8000](https://localhost:8000)) must match the one that you have configured on the Yoti Hub. This prevents other web sites from embedding your Yoti button.

Please use the code snippet below:

{% code %}
{% tab language="markup" %}
<head>
  <script src="https://www.yoti.com/share/client/"></script>
</head>

<body>
  <!-- Yoti element will be rendered inside this DOM node -->
  <div id="xxx"></div>

  <!-- This script snippet will also be required in your HTML body -->
  <script>
    window.Yoti.Share.init({
        "elements": [{
            "domId": "xxx",
            "scenarioId": "xxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "clientSdkId": "xxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "button": {
                "label": "xxxxxx"
            }
        }]
    });
  </script>
</body>
{% /tab %}
{% /code %}

{% table %}
| Name | Required | Purpose | 
| ---- | ---- | ---- | 
| domID | True | Specifies the ID of the DOM node where Yoti webshare wants to be rendered. | 
| clientSdkId | True | Identifies your Yoti Hub application. This value can be found in the Hub, within your application section, in the keys tab.&nbsp;&nbsp; | 
| scenarioId | True | Identifies the attributes associated with your Yoti application.   This value can be found on your application page in Yoti Hub (navigate to Scenarios tab) | 
{% /table %}

The privacy policies and logo are all configurable in our Yoti Hub.

## Step 4: Installing the SDK

Once you have a working button you can move on to installing the SDK.

To successfully integrate you will need the following information about your application from Yoti Hub:

SDK ID: This is generated by Yoti when you publish your Yoti application on Yoti Hub. You can find it labelled as Yoti Client SDK ID under the Keys tab within your application. The SDK ID is necessary to initialise the Yoti SDK and it is passed in each call to our servers.

Your application key pair: This is the private key (in .pem format) associated with the Yoti application you created on Hub.

There are three purposes for this PEM file:

- Decrypting the one-time-use token
- Signing your requests to our servers
- Decrypting the fetched user profile so that the profile data can be consumed by your application

If you lose or corrupt your PEM file you will be able to generate a new one. Remember, regenerating your key pair will break your current application by invalidating your current PEM file and generated keys. This means you will be unable to decrypt new tokens until these are replaced by the newly-generated ones.

The Yoti SDKs are available via popular dependency management systems. Further details can be found on the pages of the specific projects.

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

// Or the following Composer dependency:
"require": {
    "yoti/yoti-php-sdk" : "2.4"
}
{% /tab %}
{% tab language="python" %}
pip install yoti
{% /tab %}
{% tab language="java" %}
// If you are using Maven, add the following dependency:
<dependency>
    <groupId>com.yoti</groupId>
    <artifactId>yoti-sdk-impl</artifactId>
    <version>2.0.0</version>
</dependency>

// If you are using Gradle, add the following dependency:

compile group: 'com.yoti', name: 'yoti-sdk-impl', version: '2.0.0'
{% /tab %}
{% tab language="go" %}
// As of version 2.4.0, modules are used. This means it's not necessary to get a copy or fetch all dependencies 
// as instructed below, as the Go toolchain will fetch them as necessary. 
// You can simply add a `require github.com/getyoti/yoti-go-sdk/v2` to go.mod.

// To download and install the Yoti SDK and its dependencies, run the following command from your terminal:
go get "github.com/getyoti/yoti-go-sdk/v2"
{% /tab %}
{% tab language="csharp" %}
// To install the Yoti NuGet package you will need to install NuGet.

// To import the latest Yoti SDK into your project, enter the following
// command from NuGet Package Manager Console in Visual Studio:
Install-Package Yoti

// For other installation methods, see https://www.nuget.org/packages/Yoti
{% /tab %}
{% /code %}

$plugin[nu1bfdxrc7k]

Once you have added the Yoti SDK dependency to your project, it’s time to initialise a Yoti client as shown in the code snippet below.

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

# YOTI_KEY="-----BEGIN RSA PRIVATE KEY-----\nMIIEp..."
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

## Step 5: Retrieving a profile

This part is more the back-end integration which involves receiving a one time use token, decrypting it to get a user profile.

When a user scans a Yoti QR code, Yoti makes a GET request to your callback URL, passing a token as a query string parameter named token.

For a URL set as [https://your-callback-url](https://your-callback-url) in the Yoti Hub, the returned callback URL would look like the following: [https://your-callback-url?token=](https://your-callback-url?token=)

You can set and edit the callback URL within your Yoti application under the Integration tab. Yoti will automatically prefix the URL with your domain.

When your web application receives a token via the exposed endpoint as a query string parameter, you can easily retrieve the user profile. The user profile object provides a set of attributes corresponding to the user attributes you specified during the creation of your Yoti application on Hub.

When you pass the token to the Yoti Client object, the SDK does the following:

- Decrypts the wrapped receipt key attribute, using the application private key
- Uses the decrypted key to decrypt the other party profile content attribute
- Decodes the decrypted profile and returns it to your application

The profile attributes are central to the SDK and allow you to see and work with the information that your users share with you.

{% code %}
{% tab language="javascript" %}
yotiClient.getActivityDetails(oneTimeUseToken)
  .then((activityDetails) => {
    const rememberMeId = activityDetails.getRememberMeId();
    const parentRememberMeId = activityDetails.getParentRememberMeId();
    const receiptId = activityDetails.getReceiptId();
    const timestamp = activityDetails.getTimestamp();
    const base64SelfieUri = activityDetails.getBase64SelfieUri();

    const userProfile = activityDetails.getUserProfile(); // deprecated, use getProfile() instead
    const profile = activityDetails.getProfile();

    const applicationProfile = activityDetails.getApplicationProfile();
    const selfieImageData = profile.getSelfie().getValue();
    const fullName = profile.getFullName().getValue();
    const familyName = profile.getFamilyName().getValue();
    const givenNames = profile.getGivenNames().getValue();
    const phoneNumber = profile.getPhoneNumber().getValue();
    const emailAddress = profile.getEmailAddress().getValue();
    const dateOfBirth = profile.getDateOfBirth().getValue();
    const postalAddress = profile.getPostalAddress().getValue();
    const structuredPostalAddress = profile.getStructuredPostalAddress().getValue();
    const gender = profile.getGender().getValue();
    const nationality = profile.getNationality().getValue();
    const ageVerified = profile.getAgeVerified().getValue();
    const documentDetails = profile.getDocumentDetails().getValue();
    const applicationName = applicationProfile.getName().getValue();
    const applicationUrl = applicationProfile.getUrl().getValue();
    const applicationLogo = applicationProfile.getLogo().getValue();
    const applicationReceiptBgColor = applicationProfile.getReceiptBgColor().getValue();

    // You can retrieve the sources and verifiers for each attribute as follows
    const givenNamesObj = profile.getGivenNames()
    const givenNamesSources = givenNamesObj.getSources(); // list/array of anchors
    const givenNamesVerifiers = givenNamesObj.getVerifiers(); // list/array of anchor

    // You can also retrieve further properties from these respective anchors in the following way:
    // Retrieving properties of the first anchor
    const value = givenNamesSources[0].getValue(); // string
    const subtype = givenNamesSources[0].getSubType(); // string
    const timestamp = givenNamesSources[0].getSignedTimeStamp().getTimestamp(); // Date object
    const originServerCerts = givenNamesSources[0].getOriginServerCerts(); // list of X509 certificates
  })
{% /tab %}
{% tab language="ruby" %}
yoti_activity_details = Yoti::Client.get_activity_details(oneTimeUseToken)

remember_me_id = yoti_activity_details.remember_me_id
parent_remember_me_id = yoti_activity_details.parent_remember_me_id
receipt_id = yoti_activity_details.receipt_id
timestamp = yoti_activity_details.timestamp
base64_selfie_uri = yoti_activity_details.base64_selfie_uri
age_verified = yoti_activity_details.age_verified
profile = yoti_activity_details.profile
application_profile = yoti_activity_details.application_profile

selfie_image_data = profile.selfie.value
full_name = profile.full_name.value
given_names = profile.given_names.value
family_name = profile.family_name.value
phone_number = profile.phone_number.value
email_address = profile.email_address.value
date_of_birth = profile.date_of_birth.value
postal_address = profile.postal_address.value
structured_postal_address = profile.structured_postal_address.value
gender = profile.gender.value
nationality = profile.nationality.value

application_name = application_profile.name.value
application_url = application_profile.url.value
application_logo = application_profile.logo.value
application_receipt_bgcolor = application_profile.receipt_bgcolor.value

# You can retrieve the sources and verifiers for each attribute as follows:
given_names_obj = profile.given_names
given_names_sources = given_names_obj.sources # list of anchors
given_names_verifiers = given_names_obj.verifiers # list of anchors
given_names_anchors = given_names_attribute.anchors

# You can also retrieve further properties from these respective anchors in the following way:

# Retrieving properties of the first anchor
type = given_names_sources[0].type # string
value = given_names_sources[0].value # string
sub_type = given_names_sources[0].sub_type # string
time_stamp = given_names_sources[0].signed_time_stamp.time_stamp # DateTime object
origin_server_certs = given_names_sources[0].origin_server_certs # list of X509 certificates
{% /tab %}
{% tab language="php" %}
<?php
use Yoti\Helper\ActivityDetailsHelper;

$activityDetails = $client->getActivityDetails($oneTimeUseToken);
rememberMeId = $activityDetails->getRememberMeId();
parentRememberMeId = $activityDetails->getParentRememberMeId();
$profile = $activityDetails->getProfile();
$applicationProfile = $activityDetails->getApplicationProfile();

$selfieImageObj = $profile->getSelfie()->getValue();
$selfieImageBase64Content = $selfieImageObj->getBase64Content();
$fullName = $profile->getFullName()->getValue();
$givenNames = $profile->getGivenNames()->getValue();
$familyName = $profile->getFamilyName()->getValue();
$phoneNumber = $profile->getPhoneNumber()->getValue();
$emailAddress = $profile->getEmailAddress()->getValue();
$dateOfBirth = $profile->getDateOfBirth()->getValue();
$postalAddress = $profile->getPostalAddress()->getValue();
$structuredPostalAddress = $profile->getStructuredPostalAddress()->getValue();
$gender = $profile->getGender()->getValue();
$nationality = $profile->getNationality()->getValue();
$ageVerifications = $profile->getAgeVerifications();
$ageUnderVerification = $profile->findAgeUnderVerification($age);
$ageOverVerification = $profile->findAgeOverVerification($age);
$documentDetails = $profile->getDocumentDetails()->getValue();

$applicationName = $applicationProfile->getApplicationName()->getValue();
$applicationUrl = $applicationProfile->getApplicationUrl()->getValue();
$applicationLogo = $applicationProfile->getApplicationLogo()->getValue();
$applicationReceiptBgColor = $applicationProfile->getApplicationReceiptBgColor()->getValue();

// You can retrieve the sources and verifiers for each attribute as follows:
$givenNamesObj = $profile->getGivenNames();
$givenNamesSources = $givenNamesObj->getSources(); // list of anchors
$givenNamesVerifiers = $givenNamesObj->getVerifiers(); // list of anchors

// You can also retrieve further properties from these respective anchors in the following way:

// Retrieving properties of the first anchor
$value = $givenNamesSources[0]->getValue(); // string
$subType = $givenNamesSources[0]->getSubType(); // string
$timeStamp = $givenNamesSources[0]->getSignedTimeStamp()->getTimestamp(); // DateTime object
$originServerCerts = $givenNamesSources[0]->getOriginServerCerts(); // list of X509 certificates
{% /tab %}
{% tab language="python" %}
activity_details = client.get_activity_details(oneTimeUseToken)
profile = activity_details.profile

selfie = profile.selfie.value
given_names = profile.given_names.value
family_name = profile.family_name.value
full_name = profile.full_name.value
phone_number = profile.phone_number.value
date_of_birth = profile.date_of_birth.value
postal_address = profile.postal_address.value
structured_postal_address = profile.structured_postal_address.value
gender = profile.gender.value
nationality = profile.nationality.value

remember_me_id = activity_details.user_id
base64_selfie_uri = activity_details.base64_selfie_uri

# You can retrieve the anchors, sources and verifiers for each attribute as follows:
given_names_attribute = profile.given_names

given_names_anchors = given_names_attribute.anchors
given_names_sources = given_names_attribute.sources
given_names_verifiers = given_names_attribute.verifiers

# You can also retrieve further properties from these respective anchors in the following way:
source_anchor = given_names_sources[0]
value = source_anchor.value
sub_type = source_anchor.sub_type
timestamp = source_anchor.signed_timestamp
origin_server_certs = source_anchor.origin_server_certs
{% /tab %}
{% tab language="java" %}
ActivityDetails activityDetails = client.getActivityDetails(oneTimeUseToken);
HumanProfile profile = activityDetails.getUserProfile();
ApplicationProfile applicationProfile = activityDetails.getApplicationProfile();

String rememberMeId = activityDetails.getRememberMeId();
String parentRememberMeId = activityDetails.getParentRememberMeId();
Date timestamp = activityDetails.getTimestamp();
String receiptId = activityDetails.getReceiptId();

Image selfie = profile.getSelfie().getValue();
String selfieBase64Content = selfie.getBase64Content();
String fullName = profile.getFullName().getValue();
String givenNames = profile.getGivenNames().getValue();
String familyName = profile.getFamilyName().getValue();
String phoneNumber = profile.getPhoneNumber().getValue();
String emailAddress = profile.getEmailAddress().getValue();
Date dateOfBirth = profile.getDateOfBirth().getValue();
String gender = profile.getGender().getValue();
String address = profile.getPostalAddress().getValue();
String nationality = profile.getNationality().getValue();
AgeVerification over18Verification = profile.findAgeOverVerification(18);
if (over18Verification != null) {
  boolean isAgedOver18 = over18Verification.getResult();
}
AgeVerification under55Verification = profile.findAgeUnderVerification(55);
if (under55Verification != null) {
  boolean isAgedUnder55 = under55Verification.getResult();
}
Map<?, ?> structuredPostalAddress = profile.getStructuredPostalAddress().getValue();
DocumentDetails documentDetails = profile.getDocumentDetails().getValue();

String applicationName = applicationProfile.getApplicationName().getValue();
String applicationUrl = applicationProfile.getApplicationUrl().getValue();
Image applicationLogo = applicationProfile.getApplicationLogo().getValue();
String applicationReceiptBgColor = applicationProfile.getApplicationReceiptBgColor().getValue();

// You can retrieve the sources and verifiers for each attribute as follows:
Attribute<String> givenNamesAttr = profile.getGivenNames();
List<Anchor> givenNamesSources = givenNamesAttr.getSources();
List<Anchor> givenNamesVerifiers = givenNamesAttr.getVerifiers();
List<Anchor> givenNamesAnchors = givenNamesAttr.getAnchors();

// You can also retrieve further properties from these respective anchors in the following way:

// Retrieving properties of the first anchor
Anchor firstSourceAnchor = givenNamesSources.get(0);
String type = firstSourceAnchor.getType();
String value = firstSourceAnchor.getValue();
String subType = firstSourceAnchor.getSubType();
SignedTimestamp signedTimestamp = firstSourceAnchor.getSignedTimestamp();
List<X509Certificate> originCertificates = firstSourceAnchor.getOriginCertificates(); // list of X509 certificates
{% /tab %}
{% tab language="go" %}
activityDetails, errStrings := client.GetUserProfile(oneTimeUseToken)

var rememberMeID string = activityDetails.RememberMeID()
var parentRememberMeID string = activityDetails.ParentRememberMeID()
var userProfile yoti.Profile = activityDetails.UserProfile

var selfie = userProfile.Selfie().Value()
var givenNames string = userProfile.GivenNames().Value()
var familyName string = userProfile.FamilyName().Value()
var fullName string = userProfile.FullName().Value()
var mobileNumber string = userProfile.MobileNumber().Value()
var emailAddress string = userProfile.EmailAddress().Value()
var address string = userProfile.Address().Value()
var gender string = userProfile.Gender().Value()
var nationality string = userProfile.Nationality().Value()
var dateOfBirth *time.Time
dobAttr, err := userProfile.DateOfBirth()
if err != nil {
    // handle error
} else {
    dateOfBirth = dobAttr.Value()
}
var structuredPostalAddress map[string]interface{}
structuredPostalAddressAttribute, err := userProfile.StructuredPostalAddress()
if err != nil {
    // handle error
} else {
    structuredPostalAddress := structuredPostalAddressAttribute.Value().(map[string]interface{})
}

// If you have chosen Verify Condition on the Yoti Dashboard with the age condition of "Over 18", 
// you can retrieve the user information with the generic .GetAttribute method, which requires the 
// result to be cast to the original type:
userProfile.GetAttribute("age_over:18").Value().(string)

// GetAttribute returns an interface, the value can be acquired through a type assertion.

// From each attribute you can retrieve the Anchors, and subsets Sources and Verifiers 
// (all as []*anchor.Anchor) as follows:
givenNamesAnchors := userProfile.GivenNames().Anchors()
givenNamesSources := userProfile.GivenNames().Sources()
givenNamesVerifiers := userProfile.GivenNames().Verifiers()

// You can also retrieve further properties from these respective anchors in the following way:
var givenNamesFirstAnchor *anchor.Anchor = givenNamesAnchors[0]

var anchorType anchor.Type = givenNamesFirstAnchor.Type()
var signedTimestamp *time.Time = givenNamesFirstAnchor.SignedTimestamp().Timestamp()
var subType string = givenNamesFirstAnchor.SubType()
var value []string = givenNamesFirstAnchor.Value()
{% /tab %}
{% tab language="csharp" %}
ActivityDetails activityDetails = yotiClient.GetActivityDetails(oneTimeUseToken);
YotiProfile profile = activityDetails.Profile;

Image selfie = profile.Selfie?.GetValue();
string selfieURI = profile.Selfie?.GetValue().GetBase64URI();
string fullName = profile.FullName?.GetValue();
string givenNames = profile.GivenNames?.GetValue();
string familyName = profile.FamilyName?.GetValue();
string mobileNumber = profile.MobileNumber?.GetValue();
string emailAddress = profile.EmailAddress?.GetValue();
DateTime? dateOfBirth = profile.DateOfBirth?.GetValue();       
string address = profile.Address?.GetValue();
Dictionary<string, Newtonsoft.Json.Linq.JToken> structuredPostalAddress = profile.StructuredPostalAddress?.GetValue();
string gender = profile.Gender?.GetValue();
string nationality = profile.Nationality?.GetValue();
Yoti.Auth.Document.DocumentDetails documentDetails = profile.DocumentDetails?.GetValue();
bool? isAgedOver18 = profile.FindAgeOverVerification(18)?.Result();
bool? isAgedUnder55 = profile.FindAgeUnderVerification(55)?.Result();

// You can retrieve the anchors, sources and verifiers for each attribute as follows:
using System.Linq;
using System.Security.Cryptography.X509Certificates;
using Yoti.Auth.Anchors;

List<Anchor> givenNamesAnchors = profile.GivenNames.GetAnchors();
List<Anchor> givenNamesSources = profile.GivenNames.GetSources();
List<Anchor> givenNamesVerifiers = profile.GivenNames.GetVerifiers();

// You can also retrieve further properties from these respective anchors in the following way:
Anchor givenNamesFirstSource = profile.GivenNames.GetSources().First();

AnchorType anchorType = givenNamesFirstSource.GetAnchorType();
List<X509Certificate2> originServerCerts = givenNamesFirstSource.GetOriginServerCerts();
byte[] signature = givenNamesFirstSource.GetSignature();
DateTime signedTimeStamp = givenNamesFirstSource.GetSignedTimeStamp().GetTimestamp();
string subType = givenNamesFirstSource.GetSubType();
string value = givenNamesFirstSource.GetValue();
{% /tab %}
{% /code %}

## Errors

The retrieve profile endpoint might return the following error codes:

{% table %}
| Code | Meaning | 
| ---- | ---- | 
| 400 | Bad Request – Any of the described query parameters is missing, or the request is wrongly formatted&lt;br&gt; | 
| 401 | Unauthorised – We couldn’t verify the request signature or any of the auth headers is missing&lt;br&gt; | 
| 404 | Not Found – The request is correctly signed but there is no profile for the provided one time use token | 
| 500 | Internal Server Error – Something went wrong during the transaction, user should log in again | 
{% /table %}

## Support

For more information, you can check out our [Developer FAQs](https://yoti.zendesk.com/hc/en-us/categories/115000656265-Developer-FAQs).

If you have any other questions please do not hesitate to contact [sdksupport@yoti.com](mailto:sdksupport@yoti.com).

_Once we have answered your question we may contact you again to discuss Yoti products and services. If you’d prefer us not to do this, please let us know when you e-mail._

$plugin[19ag7p8lxst]