---
type: page
title: Preferences
listed: true
slug: preferences
description: 
index_title: Preferences
hidden: 
keywords: 
tags: 
---

To create your session please start by creating your preferences:- 

1. Configure your client preferences. Camera and preset country options and where the user should be directed after the user journey (success/error redirect URL).
2. Configure your system preferences. Your  session length (seconds), storage and user tracking.

---

## Client Preferences

The method sdkConfig builder is explained below. If parameters are not defined the default below will be set:

{% code %}
{% tab language="javascript" %}
.withSdkConfig(
        new SdkConfigBuilder()
          .withAllowsCameraAndUpload()
          .withPrimaryColour('#2d9fff')
          .withSecondaryColour('#FFFFFF')
          .withFontColour('#FFFFFF')
          .withLocale('en-GB')
          .withPresetIssuingCountry('GBR')
          .withSuccessUrl(`${process.env.YOTI_APP_BASE_URL}/index`)
          .withErrorUrl(`${process.env.YOTI_APP_BASE_URL}/profile`)
          .build()
      )
{% /tab %}
{% tab language="java" %}
SdkConfig sdkConfig = SdkConfig.builder()
                .withAllowsCameraAndUpload()
                .withPrimaryColour("#2d9fff")
                .withSecondaryColour("#FFFFFF")
                .withFontColour("#FFFFFF")
                .withLocale("en-GB")
                .withPresetIssuingCountry("GBR")
                .withSuccessUrl("https://localhost:8443/success")
                .withErrorUrl("https://localhost:8443/error")
                .build();
{% /tab %}
{% tab language="php" %}
<?php

$sdkConfig =
    (new SdkConfigBuilder())
    ->withAllowsCameraAndUpload()
    ->withPrimaryColour('#2d9fff')
    ->withSecondaryColour('#FFFFFF')
    ->withFontColour('#FFFFFF')
    ->withLocale('en-GB')
    ->withPresetIssuingCountry('GBR')
    ->withSuccessUrl('/your/success/url')
    ->withErrorUrl('/your/error/url')
    ->build();
{% /tab %}
{% tab language="python" %}
sdk_config = (
    SdkConfigBuilder()
    .with_allows_camera_and_upload()
    .with_primary_colour("#2d9fff")
    .with_secondary_colour("#FFFFFF")
    .with_font_colour("#FFFFFF")
    .with_locale("en-GB")
    .with_preset_issuing_country("GBR")
    .with_success_url("/your/success/url")
    .with_error_url("/your/error/url")
    .build()
)
{% /tab %}
{% tab language="csharp" %}
var sdkConfig = new SdkConfigBuilder()
                .WithAllowsCameraAndUpload()
                .WithPrimaryColour("#2d9fff")
                .WithSecondaryColour("#FFFFFF")
                .WithFontColour("#FFFFFF")
                .WithLocale("en-GB")
                .WithPresetIssuingCountry("GBR")
                .WithSuccessUrl("/your/success/url")
                .WithErrorUrl("/your/error/url")
                .Build();
{% /tab %}
{% tab language="go" %}
var sdkConfig *create.SDKConfig
sdkConfig, err = create.NewSdkConfigBuilder().
	WithAllowsCameraAndUpload().
	WithPrimaryColour("#2d9fff").
	WithSecondaryColour("#FFFFFF").
	WithFontColour("#FFFFFF").
	WithLocale("en-GB").
	WithPresetIssuingCountry("GBR").
	WithSuccessUrl("https://localhost:8080/success").
	WithErrorUrl("https://localhost:8080/error").
	Build()
{% /tab %}
{% tab language="java" title="Java v2" %}
SdkConfig sdkConfig = SdkConfigBuilderFactory.newInstance().create()
                .withAllowsCameraAndUpload()
                .withPrimaryColour("#2d9fff")
                .withSecondaryColour("#FFFFFF")
                .withFontColour("#FFFFFF")
                .withLocale("en-GB")
                .withPresetIssuingCountry("GBR")
                .withSuccessUrl("https://localhost:8443/success")
                .withErrorUrl("https://localhost:8443/error")
                .build();
{% /tab %}
{% /code %}

{% table %}
| Type | Parameter (examples) | Description | Optional | 
| ---- | ---- | ---- | ---- | 
| Allowed capture methods | withAllowsCameraAndUpload withAllowsCamera | Whether the user must only use the camera on their device to take a photo of their ID document, or whether they can also upload an existing image of the document from a file. | ✅ | 
| withPrimaryColour | #2d9fff(default), #ff0000 | Colours of the button provided in the frontend client as a hexadecimal RGB value. | ✅ | 
| withLocale | en-GB(default) | Force language locale for the frontend client. Full list shown below. | ✅ | 
| withPresetIssuingCountry | USA, GBR | The user must select the issuing country of the document they are uploading. This setting determines which issuing country is selected by default.\n\n\n\nNOTE: Must be a 3 letter ISO 3166 code. | ✅ | 
| withSuccessUrl | [https://yourdomain.com/success](https://yourdomain.com/success) | If the upload/photo is successfully captured redirect your users here. Yoti will then begin to carry out the requested checks and tasks. If undefined, the page will not redirect and you can listen to Yoti's post messages on the same page. | ✅ | 
| withErrorUrl | [https://yourdomain.com/error](https://yourdomain.com/error) | If the upload/photo is unsuccessfully captured redirect your users here. If undefined, the user view will display an error screen, with the error code as a query parameter and won't redirect. (Details on the error codes can be found in [auto$](/identity-verification/render-the-user-view)) | ✅ | 
| withPrivacyPolicyUrl | Allows the relying business to add their privacy policy url into the biometric consent step. | Links to the business provided privacy policy url if the biometric consent screen is enabled. | ✅ | 
{% /table %}

### Translated languages support

Yoti offers the ability to force a language locale for the front end client - see list here:

{% table %}
| Language | Parameter | 
| ---- | ---- | 
| English | en-GB (default) | 
| French  (Français) | fr | 
| Spanish (Español) | es | 
| Thai (ภาษาไทย) | th | 
| Russian (русский) | ru | 
| Brazilian Portuguese (português brasileiro) | pt | 
| Turkish (Türkçe) | tr | 
| Vietnamese (Tiếng Việt) | vi | 
| Czech (čeština) | cs | 
| German (Deutsch) | de | 
| Canadian english | en-CA | 
| Polish (polski) | pl | 
| Italian (Polacco) | it | 
| Danish (Dansk) | da | 
| Finnish (Suomi) | fi | 
| Norwegian (Norsk) | nb | 
| Dutch (Dutch) | nl | 
| Swedish (Svenska) | sv | 
| Japan (日本) | ja | 
| Romania (România) | ro | 
{% /table %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
       Jump to.. 
    </div>
    <div class="alert-text">
If a success URL or error URL is supplied as part of the session creation, check out Yoti's recommendation on using POST messaging to be notified on the if an error occurs in the flow or completion.    
     
    </div>
    <div class="alert-links"> 
        <a href="https://developers.yoti.com/identity-verification/notifications">Event Notifications</a>
   </div>
</div>
{% /html %}

---

## System preferences

Here is where you will determine your session spec. Each of the requested checks are explained in detail over the next few sections. 

{% code %}
{% tab language="javascript" %}
const sessionSpec = new SessionSpecificationBuilder()
    .withClientSessionTokenTtl(600)
    .withResourcesTtl(90000)
    .withUserTrackingId('some-user-tracking-id')
    .withRequestedCheck(documentAuthenticityCheck)
    .withRequestedCheck(livenessCheck)
    .withRequestedCheck(faceMatchCheck)
    .withRequestedTask(textExtractionTask)
    .withSdkConfig(sdkConfig)
    .withNotifications(notificationConfig)
		.withBlockBiometricConsent(false)
    .build();
{% /tab %}
{% tab language="java" %}
SessionSpec sessionSpec = SessionSpec.builder()
                .withClientSessionTokenTtl(600)
                .withResourcesTtl(604800)
                .withUserTrackingId("<YOUR_USER_ID>")
                .withNotifications(notificationConfig)
                .withSdkConfig(sdkConfig)
                .withRequestedCheck(documentAuthenticityCheck)
                .withRequestedCheck(livenessCheck)
                .withRequestedCheck(faceMatchCheck)
                .withRequestedTask(textExtractionTask)
  							.withBlockBiometricConsent(false)
                .build();
{% /tab %}
{% tab language="php" %}
<?php

$sessionSpec = (new SessionSpecificationBuilder())
    ->withClientSessionTokenTtl(600)
    ->withResourcesTtl(90000)
    ->withUserTrackingId('some-user-tracking-id')
    ->withRequestedCheck($documentAuthenticityCheck)
    ->withRequestedCheck($livenessCheck)
    ->withRequestedCheck($faceMatchCheck)
    ->withRequestedTask($textExtractionTask)
    ->withSdkConfig($sdkConfig)
    ->withNotifications($notificationConfig)
  	->withBlockBiometricConsent(false)
    ->build();
{% /tab %}
{% tab language="python" %}
session_spec = (
    SessionSpecBuilder()
    .with_client_session_token_ttl(600)
    .with_resources_ttl(90000)
    .with_user_tracking_id("some-user-tracking-id")
    .with_requested_check(documentAuthenticityCheck)
    .with_requested_check(livenessCheck)
    .with_requested_check(faceMatchCheck)
    .with_requested_task(textExtractionTask)
    .with_sdk_config(sdk_config)
    .with_notifications(notification_config)
  	.with_block_biometric_consent(false)
    .build()
)
{% /tab %}
{% tab language="csharp" %}
var sessionSpec = new SessionSpecificationBuilder()
                .WithClientSessionTokenTtl(600)
                .WithResourcesTtl(90000)
                .WithUserTrackingId("some-user-tracking-id")
                .WithRequestedCheck(documentAuthenticityCheck)
                .WithRequestedCheck(livenessCheck)
                .WithRequestedCheck(faceMatchCheck)
                .WithRequestedTask(textExtractionTask)
                .WithNotifications(notificationConfig)
                .WithSdkConfig(sdkConfig)
  							.WithBlockBiometricConsent(false)
                .Build();
{% /tab %}
{% tab language="go" %}
sessionSpec, err = create.NewSessionSpecificationBuilder().
	WithClientSessionTokenTTL(600).
	WithResourcesTTL(90000).
	WithUserTrackingID("some-tracking-id").
	WithRequestedCheck(faceMatchCheck).
	WithRequestedCheck(documentAuthenticityCheck).
	WithRequestedCheck(livenessCheck).
	WithRequestedTask(textExtractionTask).
	WithSDKConfig(sdkConfig).
	Build()
{% /tab %}
{% tab language="java" title="Java v2" %}
SessionSpec sessionSpec = SessionSpecBuilderFactory.newInstance().create()
                .withClientSessionTokenTtl(600)
                .withResourcesTtl(604800)
                .withUserTrackingId("<YOUR_USER_ID>")
                .withNotifications(notificationConfig)
                .withSdkConfig(sdkConfig)
                .withRequestedCheck(documentAuthenticityCheck)
                .withRequestedCheck(livenessCheck)
                .withRequestedCheck(faceMatchCheck)
                .withRequestedTask(textExtractionTask)
  							.withBlockBiometricConsent(false)
                .build();
{% /tab %}
{% /code %}

The table below explains the optional parameters for the session and data retention configuration.

{% table %}
| Parameters | Description | Optional | 
| ---- | ---- | ---- | 
| withClientSessionTokenTtl | This is how long the full Identity verification session is open for in seconds. This must be longer than 300s (5 minutes). | ✅ | 
| withResourcesTtl | Retention period ("time to live") for uploaded documents/images in number of seconds. Default is one week (`60_60_24*7=604800`). This can be a minimum of 24 hours and must be at least 24 hours longer than the client_session_token_ttl. This starts once the `client_session_token_ttl` is completed. | ✅ | 
| withUserTrackingId | Allows the relying business backend to track the same user across multiple sessions. **Note:** This should not contain any personal identifiable information. | ✅ | 
| WithBlockBiometricConsent | For several American states (Texas, Illinois and Washington US states) , Yoti will need the user’s consent to collect their biometric details for our liveness feature to be compliant with legislations in the US. We have implemented a toggle on / off box for users to give biometric consent before starting the liveness process. | ✅ | 
{% /table %}

### Mobile handoff

To optimise results Yoti has implemented a mobile handoff feature. This allows a user to transfer flow from desktop to a mobile device by scanning a QR code. The user will be guided through the session on their mobile until completed, then Yoti will return the user back to desktop.

#### User flow

The flow is documented below:

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1635263364/v2_2762/psmkgqibahxlzjiv4jny.png" caption="Mobile handoff screen 1" mode="responsive" height="1166" width="1826" %}
{% /image %}

At this point the user can still continue on computer. If they press continue they will see this screen:

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1635263441/v2_2762/p5gvjfyoithqpacznszo.png" caption="Mobile handoff screen 2" mode="responsive" height="1170" width="1818" %}
{% /image %}

The user still has the option to use the desktop. If they scan the QR code the session will be continued on their mobile. If they scan the QR code and continue their session correctly the below screen will show on web until the session is completed:

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1635266147/v2_2762/kqyqume7uxnud8ulbz7w.png" caption="Mobile handoff screen 3" mode="responsive" height="1196" width="1866" %}
{% /image %}