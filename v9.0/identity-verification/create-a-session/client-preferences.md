---
type: page
title: Client preferences
listed: true
slug: client-preferences
description: 
index_title: Client preferences
hidden: 
keywords: 
tags: 
---

To create your session please start by creating your preferences.

The method sdkConfig builder is explained below. If parameters are not defined the default below will be set:

{% code %}
{% tab language="javascript" title="Node.js" %}
.withSdkConfig(
    new SdkConfigBuilder()
        .withAllowsCamera()
        .withPrimaryColour('#2d9fff')
    		.withLocale('en-GB')
        .withPresetIssuingCountry('GBR')
        .withSuccessUrl(`${process.env.YOTI_APP_BASE_URL}/success`)
        .withErrorUrl(`${process.env.YOTI_APP_BASE_URL}/error`)
        .withAllowHandoff(true)
        .withIdDocumentTextExtractionGenericRetries(3)
        .withIdDocumentTextExtractionReclassificationRetries(3)
        .build()
)
{% /tab %}
{% tab language="java" %}
SdkConfig sdkConfig = SdkConfig.builder()
    .withAllowsCamera()
    .withPrimaryColour("#2d9fff")
  	.withLocale("en-GB")
    .withPresetIssuingCountry("GBR")
    .withSuccessUrl("https://localhost:8443/success")
    .withErrorUrl("https://localhost:8443/error")
    .withAllowHandoff(true)
    .build();
{% /tab %}
{% tab language="php" %}
<?php

$sdkConfig =
    (new SdkConfigBuilder())
    ->withAllowsCamera()
    ->withPrimaryColour('#2d9fff')
  	->withLocale('en-GB')
    ->withPresetIssuingCountry('GBR')
    ->withSuccessUrl('/your/success/url')
    ->withErrorUrl('/your/error/url')
    ->withAllowHandoff(true)
    ->withIdDocumentTextExtractionReclassificationAttempts(3)
    ->withIdDocumentTextExtractionGenericAttempts(3)
    ->build();
{% /tab %}
{% tab language="python" %}
sdk_config = (
    SdkConfigBuilder()
    .with_allows_camera()
    .with_primary_colour("#2d9fff")
  	.with_locale("en-GB")
    .with_preset_issuing_country("GBR")
    .with_success_url("/your/success/url")
    .with_error_url("/your/error/url")
    .build()
)
{% /tab %}
{% tab language="csharp" %}
var sdkConfig = new SdkConfigBuilder()
    .WithAllowsCamera()
  	.WithLocale("en-GB")
    .WithPrimaryColour("#2d9fff")
    .WithPresetIssuingCountry("GBR")
    .WithSuccessUrl("/your/success/url")
    .WithErrorUrl("/your/error/url")
    .WithAllowHandoff(false)
    .WithIdDocumentTextExtractionReclassificationRetries(3)
    .WithIdDocumentTextExtractionGenericRetries(3)
    .Build();
{% /tab %}
{% tab language="go" %}
var sdkConfig *create.SDKConfig
sdkConfig, err = create.NewSdkConfigBuilder().
    WithAllowsCamera()
    WithPrimaryColour("#2d9fff").
		WithLocale("en-GB").
    WithPresetIssuingCountry("GBR").
    WithSuccessUrl("https://localhost:8080/success").
    WithErrorUrl("https://localhost:8080/error").
    WithAllowHandOff(true).
    WithIdDocumentTextExtractionReclassificationAttempts(3).
    WithIdDocumentTextExtractionGenericAttempts(4).
    Build()
{% /tab %}
{% tab language="json" %}
{
    "sdk_config": {
        "allowed_capture_methods": "CAMERA",
        "primary_colour": "#2d9fff",
        "locale": "en-GB",
        "preset_issuing_country": "GBR",
        "success_url": "https://localhost:8443/success",
        "error_url": "https://localhost:8443/error",
        "allow_handoff": true,
        "attempts_configuration": {
            "ID_DOCUMENT_TEXT_DATA_EXTRACTION": {
                "GENERIC": 3,
                "RECLASSIFICATION": 3
            }
        }
    }
}
{% /tab %}
{% /code %}

{% table widths="213,177,0" %}
| Type | Parameter (examples) | Description | Optional | 
| ---- | ---- | ---- | ---- | 
| Allowed capture methods | withAllowsCamera\n\n\n\nwithAllowsCameraAndUpload | Whether the user must only use the camera on their device to take a photo of their ID document, or whether they can also upload an existing image of the document from a file.\n\n\n\nYoti's in-session feedback will still take place for uploaded images. This is an initial check for document image quality. A user may be asked to try again even with an uploaded image, in this case, they can either revert to live capture, or submit a new image from their live system.\n\n\nNote: The uploading of document images is a well documented attack vector for fraudsters and with the emergence of Synthetic Documents we recommend you discuss the use of this functionality with your Yoti representative.  It remains a fast and inclusive way for you to process sessions with Yoti however it could increase the risk of Fraud. | ✅ | 
| withPrimaryColour | #2d9fff(default), #ff0000 | Colours of the button provided in the frontend client as a hexadecimal RGB value. | ✅ | 
| withLocale | en-GB(default) | Force language locale for the frontend client. Full list shown below.\n\n\n\nNote This property should be omitted in order for the UI to auto detect the user's browser language settings. | ✅ | 
| withPresetIssuingCountry | USA, GBR | The user must select the issuing country of the document they are uploading. This setting determines which issuing country is selected by default.\n\n\n\nNOTE: Must be a 3 letter ISO 3166 code. | ✅ | 
| withSuccessUrl | [https://yourdomain.com/success](https://yourdomain.com/success) | If the upload/photo is successfully captured redirect your users here. Yoti will then begin to carry out the requested checks and tasks. If undefined, the page will not redirect and you can listen to Yoti's post messages on the same page. | ✅ | 
| withErrorUrl | [https://yourdomain.com/error](https://yourdomain.com/error) | If the upload/photo is unsuccessfully captured redirect your users here. If undefined, the user view will display an error screen, with the error code as a query parameter and won't redirect. (Details on the error codes can be found in [auto$](/identity-verification/render-the-user-view)) | ✅ | 
| withAllowHandoff | true, false | if enabled will offer the user to transfer flow from desktop to a mobile device by scanning a QR code. | ✅ | 
| TextExtractionGenericAttempts | 3 | The number of attempts a user has to upload their document if we are unable to process it on their initial upload. | ✅ | 
| TextExtractionReclassificationAttempts | 3 | The number of attempts a user has to upload their document if we deem the uploaded document was not the type the user selected. | ✅ | 
{% /table %}

## Translated languages

Yoti offers the ability to force a language locale for the front end client - see list here:

{% table widths="396" %}
| Language | Parameter | 
| ---- | ---- | 
| Arabic (العربية) | ar | 
| Bosnian (bosanski) | bs | 
| Brazilian Portuguese (português brasileiro) | pt | 
| Canadian English (en-CA) | en-CA | 
| Czech (čeština) | cs | 
| Danish (Dansk) | da | 
| Dutch (Dutch) | nl | 
| English (en-GB) | en-GB (default) | 
| Finnish (Suomi) | fi | 
| French (Français) | fr | 
| German (Deutsch) | de | 
| Greece (el-GR) | el-GR | 
| Hindi (हिंदी) | hi | 
| Italian (Italiano) | it | 
| Japan (日本) | ja | 
| Netherlands (Nederlands) | nl | 
| Norwegian (Norsk) | nb | 
| Polish (polski) | pl | 
| Romanian (România) | ro | 
| Russian (русский) | ru | 
| Serbia (српски) | sr | 
| Spanish (Español) | es | 
| Spanish (es-419) | es-419 | 
| Swedish (Svenska) | sv | 
| Thai (ภาษาไทย) | th | 
| American English (en-US) | en-US | 
| Turkish (Türkçe) | tr | 
| Vietnamese (Tiếng Việt) | vi | 
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

## Mobile handoff

To optimise results Yoti has implemented a mobile handoff feature. This allows a user to transfer flow from desktop to a mobile device by scanning a QR code. The user will be guided through the session on their mobile until completed, then Yoti will return the user back to desktop.

### User flow

The flow is documented below:

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/psmkgqibahxlzjiv4jny/1635263364.png" caption="Mobile handoff screen 1" mode="responsive" height="1166" %}
{% /image %}

At this point the user can still continue on computer. If they press continue they will see this screen:

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/p5gvjfyoithqpacznszo/1635263441.png" caption="Mobile handoff screen 2" mode="responsive" height="1170" %}
{% /image %}

The user still has the option to use the desktop. If they scan the QR code the session will be continued on their mobile. If they scan the QR code and continue their session correctly the below screen will show on web until the session is completed:

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/kqyqume7uxnud8ulbz7w/1635266147.png" caption="Mobile handoff screen 3" mode="responsive" height="1196" %}
{% /image %}