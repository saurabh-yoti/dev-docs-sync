---
type: page
title: Web integration
listed: true
slug: web-integration
description: 
index_title: Web integration
hidden: 
keywords: 
tags: 
---

Once you've set up your organisation account on the Yoti Hub, you’re ready to start integrating with Yoti. This section explains how to complete a basic web integration.

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      Please have a look at our best practices for a better performance of the SDK.
   </div>
   <div class="alert-links"> 
      <a target="_self"  href="https://developers.yoti.com/yoti/user-experience"> See User Experience </a>
   </div>
</div>
{% /html %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know... 
    </div>
    <div class="alert-text">
        Following our user experience guidelines makes for a faster and more enjoyable experience for your users. Please read these sections before you continue.
    </div>
    <div class="alert-links"> 
        <a  target="_self" href="https://developers.yoti.com/yoti/user-experience"> View User Experience </a> 
        <a href="https://developers.yoti.com/yoti/scenario-examples"> View Scenario examples </a> 
    </div>
</div>
{% /html %}

---

## The QR codes

You will need to create a button to allow your users to authenticate with Yoti. See **[Button design guide](https://developers.yoti.com/yoti/user-experience-digitalid#button-design-guide)** before you start the integration. 

This contains a QR code for users to scan with their Yoti app. Mobile web users will skip the QR code scanning step, as they use the Yoti mobile app directly to authenticate. 

Yoti has seven options to display the QR code.

**Standard QR codes:**

- Modal QR
- Instant QR
- Inline QR
- Yoti QR code page - No technical work required.

**Advanced QR codes:**

- Static QR
- Non Browser QR
- Dynamic QR

### Standard QR codes

**Modal QR**

The modal QR code option has a button which when clicked opens a modal pop out window with the QR code present. There are three tabs, describing how to scan the QR code, The QR code and attributes to be shared and about Yoti - Please give it a click to see it working:

{% html %}
<div id="yoti-button"></div>
{% /html %}

**Inline QR**

The inline QR code option has a button which when clicked opens just the QR code. You will need to provide more context as to what Yoti is for this. See [scenario example ](https://developers.yoti.com/yoti/scenario-examples-app)section for more detail.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1585935832/20477/vwoytddmqogp7sjjrblk.jpg" mode="300" height="312" width="468" %}
{% /image %}

**Instant QR**

The instant QR code option is just the QR code with no button. You will need to provide more context as to what Yoti is for this. See [scenario example ](https://developers.yoti.com/yoti/scenario-examples-app)section for more detail. Example below:

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1588180782/20477/bifs7i78su52yjcwsbyl.png" mode="300" height="365" width="296" %}
{% /image %}

**Yoti QR code page**

This is automatically generated when you create an[ application](https://developers.yoti.com/yoti/generate-api-keys) in the hub. You will define the following inside the hub.

- Attributes
- Call back URL
- Customisation (logo and background) 

This service can also be [technical integration **free**,](https://developers.yoti.com/yoti/code-free-integration) you can be live in a matter of minutes.

Please see this page as an [example](https://www.yoti.com/connect/32e513d2-4faa-4179-9c0a-cbbb1a673460/scenarios/97483364-1cf0-41cb-be80-bea4babecf78).

### Advanced QR codes

**Static QR**

A static QR code has no expiry to reload the QR code, this can be printed or integrated. To request this QR code please contact us directly on [sdksupport@yoti.com.](mailto:sdksupport@yoti.com)

**Non Browser QR**

If you're looking at integrating Yoti with a 'Non-browser' client, one of the tasks you will need to do is request a Yoti QR code from Yoti's servers. This URL must be transformed into a QR code before it can be scanned with the Yoti app. Yoti provides a simple API to transform this URL into an official Yoti QR.

**Dynamic QR**

This QR code is generated differently. By "dynamic" we mean that the attributes must be provided as part of the QR code request as opposed to where the attributes is defined upfront in [hub](https://hub.yoti.com/). This allows for higher flexibility, for example as part of your integration you can create a set of fields that must be filled in by the user, the set of required attributes is intrinsically dynamic from Yoti as it depends on the type of information received manually.

Please launch this demo to view how this works: [https://yoti.world/dynamicqr/](https://yoti.world/dynamicqr/).

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Jump to
   </div>
   <div class="alert-text" >
      For infromation on how to integrate the advanced QR codes please head over to the advanced features section. 
  
   </div>
   <div class="alert-links"> 
         <a href="https://developers.yoti.com/yoti/advanced-features">Advanced Featuress</a>
   </div>
</div>
{% /html %}

---

## Generate a Yoti button

Yoti provides a button generator for you to include in your HTML file. In the example below, the button generator script has been added to the head of the HTML document.

To generate the Yoti button use the code snippet below:

**Modal QR**

{% code %}
{% tab language="markdown" title="Simple Button" %}
<!-- Simple Button Generation -->

<head>
  <script src="https://www.yoti.com/share/client/"></script>
</head>

<body>
  <!-- Yoti element will be rendered inside this DOM node -->
  <div id="xxx"></div>

  <!-- This script snippet will also be required in your HTML body -->
  <script>
    window.Yoti.Share.init({
      elements: [
        {
          domId: "xxx",
          scenarioId: "xxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
          clientSdkId: "xxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
          displayLearnMoreLink: true,
        }
      ]
    });
  </script>
</body>
{% /tab %}
{% tab language="markup" title="Advanced button" %}
<!-- Advanced Button Generation -->

<head>
  <script src="https://www.yoti.com/share/client/"></script>
</head>

<body>
  <!-- Yoti element will be rendered inside this DOM node -->
  <div id="xxx"></div>

  <!-- This script snippet will also be required in your HTML body -->
  <script>
    window.Yoti.Share.init({
      elements: [
        {
          domId: "xxx",
          scenarioId: "xxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
          clientSdkId: "xxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
               displayLearnMoreLink: true,
          
          button: {
            label: "Use Yoti",
            align: "center", // "left" | "right"
            width: "full" // "auto"
          },
          modal: {
            zIndex: 9999 // default to 9999, min of 0 - max of 2147483647
          },
	      // shareComplete is currently not supported on Mobile
          shareComplete: {
            closeDelay: 4000, // default to 4000, min of 500 - max of 10000
            tokenHandler: (token, done) => {
                    console.log(`Received the token: ${token}`);
                    done(); //done() will overwrite the closeDelay
                }
          }
        }
      ]
    });
  </script>
</body>
{% /tab %}
{% tab language="javascript" title="React" %}
// Example React Component

const YotiButton = props => { 
  const buttonRef=useRef(null) 
 
  useEffect(() =>{ 
    const yoti=window.Yoti.Share.init({ 
      'elements': [{ 
        'clientSdkId': props.clientSdkId, 
        'scenarioId': props.scenarioId, 
        'domId': buttonRef.current.id, 
        'button': { 
          'label': props.text 
        } 
      }] 
    }) 
 
    return yoti.destroy 
  }, [props.clientSdkId]) 
  return( 
    <div 
      style={{ height: props.height, width: props.width}} 
      ref={buttonRef} 
      id="button-ref" 
    /> 
  ) 
}
{% /tab %}
{% tab language="javascript" title="Angular" %}
// Example Angular Component

// Include the yoti client script in the head of your index.html file
// <script src="https://www.yoti.com/share/client/"></script>
// You can directly refer to the window object, but it is a good practice to create wrapper service that gets the native window object.
// Create target <div> with an id, in you template and initialize the Yoti Init() method within your Angular component in the below format

import { Component, OnInit, OnDestroy} from '@angular/core';
import { WindowRefService } from '../window-ref.service';

@Component({
 selector: 'app-yoti-button',
 templateUrl: './yoti-button.component.html',
})

export class YotiButtonComponent implements OnInit, OnDestroy {
private WinObj : any;
private YotiButton : any;
 constructor(private winRef:WindowRefService) {
   this.WinObj = winRef.nativeWindow;
  }

 ngOnInit(): void {
   this.YotiButton = this.WinObj.Yoti.Share.init({
       elements: [
         {
           domId: "yotibutton",
           scenarioId: "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
           clientSdkId: "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
           button: {
             label: "Use Yoti",
             align: "center", // "left" | "right"
             width: "auto" // "full"
           },
           modal: {
             zIndex: 9999 // default to 9999, min of 0 - max of 2147483647
           },
         }
       ]
     });
  }
}

// To destroy the Yoti-Button object, before re-initializing it, eg: on Router Path Changes.
ngOnDestroy(): void { this.YotiButton.destroy(); }
{% /tab %}
{% tab language="javascript" title="Programmatic QR Code" %}
<!-- Advanced Button Generation -->

<head>
  <script src="https://www.yoti.com/share/client/"></script>
</head>

<body>
  <!-- Yoti element will be rendered inside this DOM node -->
  <div id="xxx"></div>

  <!-- This script snippet will also be required in your HTML body -->
  <script>
    window.Yoti.Share.init({
      elements: [
        {
          domId: "xxx",
          // For use with programmatic qr codes ONLY
          shareUrlProvider() {
            return fetch(('/location of QR code'))
              .then(response => response.json())
              .then(data => data.qr); // where 'qr' is your dynamic qr url);
          },
          // For use with programmatic qr codes ONLY
          shareUrl: "your programmatic qr url", 
          // Do not use scenarioId with shareUrl or shareUrlProvider
          clientSdkId: "xxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
          button: {
            label: "Use Yoti",
            align: "center", // "left" | "right"
            width: "full" // "auto"
          },
          modal: {
            zIndex: 9999 // default to 9999, min of 0 - max of 2147483647
          },
	        // shareComplete is currently not supported on Mobile
          shareComplete: {
            closeDelay: 4000, // default to 4000, min of 500 - max of 10000
            tokenHandler: (token, done) => {
                    console.log(`Received the token: ${token}`);
                    done(); //done() will overwrite the closeDelay
                }
          }
        }
      ]
    });
  </script>
</body>
{% /tab %}
{% /code %}

**Inline QR**

{% code %}
{% tab language="html" %}
<!-- Simple Button Generation -->

<head>
  <script src="https://www.yoti.com/share/client/"></script>
</head>

<body>
  <!-- Yoti element will be rendered inside this DOM node -->
  <div id="xxx"></div>

  <!-- This script snippet will also be required in your HTML body -->
  <script>
    window.Yoti.Share.init({
      elements: [
        {
          domId: "xxx",
          scenarioId: "xxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
          clientSdkId: "xxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
          type: "inline",
          displayLearnMoreLink: true,
          button: {
            label: " Use Yoti",
            title: " Scan with the Yoti app"
          }
        }
      ]
    });
  </script>
</body>
{% /tab %}
{% /code %}

**Instant QR**

{% code %}
{% tab language="markdown" title="mar" %}
<!-- Simple Button Generation -->

<head>
  <script src="https://www.yoti.com/share/client/"></script>
</head>

<body>
  <!-- Yoti element will be rendered inside this DOM node -->
  <div id="xxx"></div>

  <!-- This script snippet will also be required in your HTML body -->
  <script>
    window.Yoti.Share.init({
      elements: [
        {
          domId: "xxx",
          scenarioId: "xxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
          clientSdkId: "xxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
          type: "inline",
          displayLearnMoreLink: true,
          qr: {
            title: " Scan with the Yoti app"
          }
        }
      ]
    });
  </script>
</body>
{% /tab %}
{% /code %}

This JavaScript library currently needs to be invoked – do this by calling Yoti.Share.init() in the body of your HTML document. For the config, you will need to specify a ‘domId’ so we know where we need to add the Yoti button on your page and the ‘scenarioId’ that is being provided by Yoti Hub after creating an application.

The Yoti button requires the hosting page to be accessed via HTTPS, so please make sure that your web application has HTTPS enabled. 

Finally, the domain port pair where the button is deployed (i.e. [https://localhost:8000](https://localhost:8000)) must match the one that you have configured in Yoti Hub. This prevents other web sites from embedding your Yoti button.

{% table %}
| Name | Purpose | Required | 
| ---- | ---- | ---- | 
| domID | Specifies the ID of the DOM node where Yoti webshare wants to be rendered. | Yes | 
| clientSdkId | Identifies your Yoti Hub application. This value can be found in the Hub, within your application section, in the keys tab. | Yes | 
| scenarioId | Identifies the attributes associated with your Yoti application. This value can be found on your application page in Yoti Hub (navigate to Scenarios tab) | Yes | 
| Button | Config for the button styling. | No | 
| Button - Label | Text on the button. Should be relevant for your use case. | No | 
| Button - align | Alignment of the button in the parent div - "center", "left", "right" | No | 
| Button - width | Width of the button - "auto" will set to fit the label. "full" - will fill the width of the parent div. | No | 
| Modal - zIndex | Sets the z-index of the modal. This is defaulted to 9999. | No | 
| shareComplete | Allows token handling to be performed without redirecting the webpage. | No | 
| shareComplete - closeDelay | How long the modal will stay open before handling the token or redirecting. Default to 4000ms with a min of 500ms and a max of 1000ms | No | 
| shareComplete - tokenHandler | Allows you to run your own function to handle the token without a redirect. Calling done() will close the modal; overwriting any closeDelay you have. | No | 
| label | This is the text on the button and is customisable | Yes | 
| title | This is the text around the QR code and is customisable | No | 
| shareUrl | This is used with programmatic QR code creation. It allows you to render a Yoti QR created via the Yoti SDK. If using a shareUrl then you should not specify a scenarioId. | No | 
| shareUrlProvider | shareUrlProvider is a function which resolves to a share url generated from using programmatic QR code creation. If using this method, a scenarioId should not be specified. Using this function allows us to retrieve a new programmatic QR from your server in the original QR times out. | No | 
| [displayLearnMoreLink](https://developers.yoti.com/yoti/user-experience-app#learn-more-page) | Creates a dynamic page which informs and gives context to your users of steps they need to complete to download Yoti and scan the QR code. Provided as a link below the button. This can be turned off by changing to false. | No | 
{% /table %}

Make use of our [learn more ](https://developers.yoti.com/yoti/user-experience-app#learn-more-page)pages to help guide customers through the Yoti flow. 

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1595873300/29762/kxo76phd25iler6kn7eh.jpg" caption="Learn More page" mode="300" height="168" width="342" %}
{% /image %}

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you continue
   </div>
   <div class="alert-text" >
      Please have a look at our best practices. We recommend taking them into account for a better performance of the SDK.
   </div>
   <div class="alert-links"> 
      <a  target="_self" href="https://developers.yoti.com/yoti/user-experience#button-design-guide">See Button design guide</a>
   </div>
</div>
{% /html %}

---

## Install SDK

Once you have a working button, you can move on to installing the SDK. To successfully integrate you will need the following information about your application from Yoti Hub:

**SDK ID**

This is generated by Yoti when you publish your Yoti application in Yoti Hub. You can find it labelled as Yoti Client SDK ID under the Keys tab within your application. The SDK ID is necessary to initialise the Yoti SDK and it is passed in each call to our system.

**Your application key pair**

This is the private key (in .pem format) associated with the Yoti application you created in Yoti Hub.

There are three purposes for this PEM file:

- Decrypting the one-time-use token.
- Signing your requests to our system.
- Decrypting the fetched user profile so that the profile data can be consumed by your application.

If you lose or corrupt your PEM file you will be able to generate a new one. Regenerating your key pair will break your current application by invalidating your current PEM file and generated keys. This means you will be unable to decrypt new tokens until these are replaced by the newly-generated ones.

The Yoti SDKs are available via popular dependency management systems. Further details can be found on the pages of the specific projects.

To install the Yoti SDK:

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

go get "github.com/getyoti/yoti-go-sdk/v3”
{% /tab %}
{% tab language="csharp" %}
// To install the Yoti NuGet package you will need to install NuGet.
// To import the latest Yoti SDK into your project, enter the following
// command from NuGet Package Manager Console in Visual Studio:

Install-Package Yoti

// For other installation methods, see https://www.nuget.org/packages/Yoti
{% /tab %}
{% /code %}

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

client, err := yoti.NewClient(sdkId, key)
{% /tab %}
{% tab language="csharp" %}
const string SDK_ID = "YOTI_CLIENT_SDK_ID";
const string PEM_PATH = "YOTI_KEY_FILE_PATH";

var privateKeyStream = System.IO.File.OpenText(PEM_PATH);
var yotiClient = new YotiClient(SDK_ID, privateKeyStream);
{% /tab %}
{% /code %}

{% html %}
<div class="alert-SAND">
    <div class="alert-title" id="SAND">
      Sandbox
    </div>
    <div class="alert-text">
       To see how to do this using our sandbox, please head over to the link below.
    </div>
    <div class="alert-links"> 
        <a href="https://developers.yoti.com/yoti/sandbox-app#creating-a-sandbox-request">Creating a sandbox request</a>
    </div>
</div>
{% /html %}

---

## Retrieve a profile

Retrieving a profile involves receiving a one-time-use token, and decrypting it to get a user profile.

When a user scans a Yoti QR code, Yoti makes a GET request to your callback URL, passing a token as a query string parameter.

For a URL set as **[https://your-callback-url](https://your-callback-url)** in Yoti Hub, the returned callback URL would look like the following: **[https://your-callback-url?token=](https://your-callback-url?token=)**

You can set and edit the callback URL within your Yoti application under the Integration tab. Yoti will automatically prefix the URL with your domain.

When your web application receives a token via the exposed endpoint as a query string parameter, you can easily retrieve the user profile. The user profile object provides a set of attributes corresponding to the user attributes you specified during the creation of your Yoti application on Hub.

**SDK process**

When you pass the token to the Yoti Client object, the SDK does the following:

- Decrypts the wrapped receipt key attribute, using the application private key.
- Uses the decrypted key to decrypt the other party profile content attribute.
- Decodes the decrypted profile and returns it to your application.

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
activityDetails, err := client.GetActivityDetails(yotiOneTimeUseToken)

	rememberMeID := activityDetails.RememberMeID()
	parentRememberMeID := activityDetails.ParentRememberMeID()

	userProfile := activityDetails.UserProfile
	selfie := userProfile.Selfie().Value().Data()
	givenNames := userProfile.GivenNames().Value()
	familyName := userProfile.FamilyName().Value()
	fullName := userProfile.FullName().Value()
	mobileNumber := userProfile.MobileNumber().Value()
	emailAddress := userProfile.EmailAddress().Value()
	address := userProfile.Address().Value()
	gender := userProfile.Gender().Value()
	nationality := userProfile.Nationality().Value()
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
		structuredPostalAddress = structuredPostalAddressAttribute.Value()
	}

	// If you have chosen Verify Condition on the Yoti Dashboard with the age condition of "Over 18",
	// you can retrieve the user information with the generic .GetAttribute method, which requires the
	// result to be cast to the original type:
	age_over := userProfile.GetAttribute("age_over:18").Value().(string)

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
	var value string = givenNamesFirstAnchor.Value()
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

{% html %}
<div class="alert-SAND">
    <div class="alert-title" id="SAND">
      Sandbox
    </div>
    <div class="alert-text">
       To see how to do this using our sandbox, please head over to the link below.
    </div>
    <div class="alert-links"> 
        <a href="https://developers.yoti.com/yoti/sandbox-app#reading-the-request">Reading the request</a>
    </div>
</div>
{% /html %}

## Further information

### Query parameters

You can append query params to the landing page URL that displays the Yoti button. These will be added to the callback URL.

For example if you load the landing page containing the Yoti button as follows:

[https://example.com/?iso=test&user_id=6667](https://example.com/?iso=test&amp;user_id=6667)

The query parameters (iso=test&user_id=6667) will be returned in the callback URL.