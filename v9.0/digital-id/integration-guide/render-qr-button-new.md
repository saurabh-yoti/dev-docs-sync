---
type: page
title: Render QR button
listed: true
slug: render-qr-button-new
description: 
index_title: Render QR button
hidden: 
keywords: 
tags: 
---

Yoti provides a QR/button generation script to be included in your HTML file. In the examples below, this script has been added to the head of the HTML document.

To render the Yoti QR or button,  please take a look at our range of options below and pick a configuration.

The JavaScript library called Webshare needs to be invoked – you can do this by calling Yoti.createWebShare() in the body of your HTML document. For the config, you will need to specify a ‘domId’ so the script knows where to add the Yoti button on your page.

The Yoti button requires the hosting page to be accessed via HTTPS, so please make sure that your web application has HTTPS enabled.

{% table widths="189,0" %}
| Name | Purpose | Required | 
| ---- | ---- | ---- | 
| name | Identifies the Yoti share on the page. | ✅ | 
| domID | Specifies the ID of the DOM node where Yoti webshare has to be rendered. | ✅ | 
| clientSdkId | Identifies your Yoti Hub application. This value can be found in the Hub, within your application section, in the keys tab. | ✅ | 
| hooks | Object for specifying the functions hooks to be called by Yoti webshare. | ✅ | 
| hooks - sessionIdResolver | Hook Function to resolve the Session ID generated from the creating a Share session using the Yoti backend SDK. | ✅ | 
| hooks - errorListener | Allows you to listen to error messages from the Webshare QR/button. | ❌ | 
| hooks - completionHandler | Allows you to retrieve the Share Receipt ID within the hook function and prevents the automatic redirection to Session Redirect URI. | ❌ | 
| locale | Specifies the the localisation for Yoti QR/button. Default is en. | ❌ | 
| skinId | The theme to be used for the webshare rendering. | ❌ | 
{% /table %}

Finally, the domain and port pair where the button is deployed (i.e. [https://localhost:8000](https://localhost:8000/)) must match the one that you have configured in Yoti Hub. This prevents other web sites from embedding your Yoti button.

---

### Supported Translations (Locale)

Yoti offers the ability to specify a language locale for the front-end webshare client. Only the `yoti` skin supports the localisation - see list here:

{% table widths="402" %}
| Language | Parameter | 
| ---- | ---- | 
| English | en (default) | 
| French (Français) | fr | 
{% /table %}

---

### Modal QR

The Modal QR code option has a button which when clicked opens a modal pop out window with the QR code present. There are three tabs, describing how to scan the QR code, The QR code & attributes to be shared and about Yoti.

{% image url="https://uploads.developerhub.io/prod/kvAX/srcrelbu4df0veellze7cuu1g96r1srnf78yxw2bvh9z74oes6exu7o8x9gq3xie.png" caption="Modal QR button" mode="responsive" height="260" width="560" %}
{% /image %}

{% code %}
{% tab language="html" title="Modal QR button" %}
<head>
  <script src="https://www.yoti.com/share/client/v2"></script>
</head>

<body>
  <!-- Yoti element will be rendered inside this DOM node -->
  <div id="xxx"></div>

  <!-- This script snippet will also be required in your HTML body -->
  <script>
    const loadYoti = async () => {
      const { Yoti } = window;
      if (Yoti) {
        console.info('Waiting for Yoti...');
        await Yoti.ready()
        console.info('Yoti is now ready');
      } else {
        console.error('Yoti client was not found!');
      }
    }

    const createYotiWebShare = async () => {
      const { Yoti } = window;
      if (Yoti) {
        await Yoti.createWebShare({
          name: 'test-share',
          domId: 'xxx',
          sdkId: 'xxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx',
          skinId: 'digital-id-uk', // or skinId: 'yoti'
          flow: "MODAL",
          hooks: {
            sessionIdResolver: onSessionIdResolver,
            errorListener: onErrorListener
          }
        })
      }
    }

    async function onSessionIdResolver() {
      // Make a call to your backend, and return a 'sessionId'
      const response = await fetch('https://localhost:3000/sessions', { method: 'POST' });
      const data = await response.json();
      return data.sessionId;
    }

    function onErrorListener(...data) {
      console.warn('onErrorListener:', ...data);
    }

    const start = async () => {
      await loadYoti();
      await createYotiWebShare();
    }

    start().catch((e) => console.error(`Could not create Yoti WebShare: `, e));
  </script>
</body>
{% /tab %}
{% /code %}

---

### Inline QR

The Inline QR code option has a button which when clicked opens just the QR code. You will need to provide more context on your page as to what the Digital ID button is for. See the example below:

{% image url="https://uploads.developerhub.io/prod/kvAX/6uo16ynh3bo901rrgcle5irsgjiz0d8opouidduitbn8qv3550ffko8fwvlvdoj3.png" caption="Inline QR code" mode="600" height="852" width="600" %}
{% /image %}

{% code %}
{% tab language="html" title="Inline QR button" %}
<head>
  <script src="https://www.yoti.com/share/client/v2"></script>
</head>

<body>
  <!-- Yoti element will be rendered inside this DOM node -->
  <div id="xxx"></div>

  <!-- This script snippet will also be required in your HTML body -->
  <script>
    const loadYoti = async () => {
      const { Yoti } = window;
      if (Yoti) {
        console.info('Waiting for Yoti...');
        await Yoti.ready()
        console.info('Yoti is now ready');
      } else {
        console.error('Yoti client was not found!');
      }
    }

    const createYotiWebShare = async () => {
      const { Yoti } = window;
      if (Yoti) {
        await Yoti.createWebShare({
          name: 'test-share',
          domId: 'xxx',
          sdkId: 'xxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx',
          skinId: 'digital-id-uk', // or skinId: 'yoti'
          flow: "INLINE",
          hooks: {
            sessionIdResolver: onSessionIdResolver,
            errorListener: onErrorListener
          }
        })
      }
    }

    async function onSessionIdResolver() {
      // Make a call to your backend, and return a 'sessionId'
      const response = await fetch('https://localhost:3000/sessions', { method: 'POST' });
      const data = await response.json();
      return data.sessionId;
    }

    function onErrorListener(...data) {
      console.warn('onErrorListener:', ...data);
    }

    const start = async () => {
      await loadYoti();
      await createYotiWebShare();
    }

    start().catch((e) => console.error(`Could not create Yoti WebShare: `, e));
  </script>
</body>
{% /tab %}
{% /code %}

---

### Instant QR

The Instant QR code option is just the QR code with no button. You will need to provide more context on your page as to what the Digital ID QR is for. See the example below:

{% image url="https://uploads.developerhub.io/prod/kvAX/ocl4rgr6lm3y8rnwjq7tdd0h8um9npm37vgst0j77qofk99klhxb8swhl9v5n1qf.png" caption="Instant QR code" mode="responsive" height="846" width="614" %}
{% /image %}

{% code %}
{% tab language="html" title="Instant QR" %}
<head>
  <script src="https://www.yoti.com/share/client/v2"></script>
</head>

<body>
  <!-- Yoti element will be rendered inside this DOM node -->
  <div id="xxx"></div>

  <!-- This script snippet will also be required in your HTML body -->
  <script>
    const loadYoti = async () => {
      const { Yoti } = window;
      if (Yoti) {
        console.info('Waiting for Yoti...');
        await Yoti.ready()
        console.info('Yoti is now ready');
      } else {
        console.error('Yoti client was not found!');
      }
    }

    const createYotiWebShare = async () => {
      const { Yoti } = window;
      if (Yoti) {
        await Yoti.createWebShare({
          name: 'test-share',
          domId: 'xxx',
          sdkId: 'xxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx',
          skinId: 'digital-id-uk', // or skinId: 'yoti'
          flow: "INSTANT",
          hooks: {
            sessionIdResolver: onSessionIdResolver,
            errorListener: onErrorListener
          }
        })
      }
    }

    async function onSessionIdResolver() {
      // Make a call to your backend, and return a 'sessionId'
      const response = await fetch('https://localhost:3000/sessions', { method: 'POST' });
      const data = await response.json();
      return data.sessionId;
    }

    function onErrorListener(...data) {
      console.warn('onErrorListener:', ...data);
    }

    const start = async () => {
      await loadYoti();
      await createYotiWebShare();
    }

    start().catch((e) => console.error(`Could not create Yoti WebShare: `, e));
  </script>
</body>
{% /tab %}
{% /code %}

{% callout type="warning" title="Before you continue" %}
Please have a look at our best practices. We recommend taking them into account for a better performance of the SDK.

[Button design guide](https://developers.yoti.com/digital-id/user-experience#button-design-guide)
{% /callout %}

---

### Static QR

A static QR code has no expiry to reload the QR code. Dynamic QR codes have an expiry of 3 minutes until a reload is required. This provides a low cost/offline verification that users can print out and use as many times as needed. Data sent via a static QR code can be viewed in the hub as a receipt.

The process is:

1. Create an organisation on the hub.
2. Create an application on the hub and add your scenario.
3. Send your SDK ID via our support [web form](https://support.yoti.com/yotisupport/s/contactsupport).

We aim to get your QR code to you in 3-4 working days.

---

### Non-Browser QR

If you're looking to integrating Yoti with a 'Non-browser' client, one of the tasks you will need to do is request a Yoti QR code URI from Yoti's servers. This URI must be transformed into a Yoti QR before it can be scanned with the Yoti app. Yoti provides a simple API to render an official Yoti QR image.

It is possible to manually construct this QR code as this can be necessary in cases where you do not have access to a Web browser on your front end, for example using a kiosk GUI.

Requesting a Yoti QR is broken down into the following steps:

1. Creating a Share session
2. Requesting a QR code from the session
3. Rendering the Yoti QR
4. Receiving the receipt id via the webhook
5. Using the receipt id to retrieve the profile

#### Create a share session

First, you need to create a Yoti share session by specifying a policy and other session configuration. In order to retrieve the share receipt via a webhook endpoint, you have to enable the notifications.

The process to create a session is described [here](/digital-id/create-share-session).

#### Request a QR code

In order to create a Yoti QR, you have to request a new QR code from the share session. To do this, use the following code:

{% code %}
{% tab language="javascript" title="Node.js" %}
yotiClient.createShareQrCode(sessionId)
  .then((shareQrCode) => {
  	const qrCodeId = shareQrCode.getId();
		const qrCodeUri = shareQrCode.getUri();
  }).catch((error) => {
    console.error(error.message);
  });
{% /tab %}
{% tab language="java" %}
// Coming soon
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\Exception\DigitalIdentityException;

try {
  	$shareQrCode = $client->createShareQrCode($sessionId);
  	$qrCodeId = $shareQrCode->getId();
  	$qrCodeUri = $shareQrCode->getUri();
} catch (DigitalIdentityException $e) {
  	throw new DigitalIdentityException($e->getMessage());
}
{% /tab %}
{% tab language="csharp" %}
var shareQrCode = yotiClient.CreateShareQrCode(shareSessionId);

string qrCodeId = shareQrCode.GetId();
Uri qrCodeUri = shareQrCode.GetUri();
{% /tab %}
{% /code %}

A Yoti QR code contains an ID and URI and is returned in following form:

{% code %}
{% tab language="markup" %}
{
    "id": "qr.v2.TSicHeyZQ1ODdtX0XSXEpQ",
    "uri": "https://code.yoti.com/CAEaHHFyLnYyLlRTaWNIZXlaUTFPRGR0WDBYU1hFcFEwAg=="
}
{% /tab %}
{% /code %}

#### Render the Yoti QR

The above QR code URI must be transformed into a Yoti QR before it can be scanned with the Yoti app. Yoti provides a simple API endpoint to transform this URI into an official Yoti QR image - This is important to establish trust between your user base and Yoti.

{% image url="https://uploads.developerhub.io/prod/kvAX/kcclkyn6ay2lu2lhwuzyvcq4rvgs4uuc900yr0ajh1bspry0hki64n86s0agzvif.png" mode="300" height="477" width="300" %}
{% /image %}

{% code %}
{% tab language="markup" %}
POST https://api.yoti.com/api/v1/qrcodes/image
{% /tab %}
{% /code %}

The following headers are required to use the image service:

{% table widths="152,0" %}
| Header | Value | Description | 
| ---- | ---- | ---- | 
| Accept | The follow Accept values can be provided in the header\n\n\n\n- image/svg+xml\n- image/png | Returns a formatted QR code as an svg or png | 
| Content-Type | application/json | Sets the correct content type | 
{% /table %}

The request body should be formed as JSON, specifying a URL (mandatory) and an image size (optional).

{% code %}
{% tab language="json" %}
{
	"url": "https://code.yoti.com/<YotiCode>"
  "size": 200 // Optional
}
{% /tab %}
{% /code %}

{% table widths="" %}
| Field | Type | Value | 
| ---- | ---- | ---- | 
| url | string | This is the URI returned from requesting a Yoti QR | 
| size | number | This is an optional parameter for specifying QR size | 
| skinId | yoti / digital-id-uk | Allows the QR to be displayed in either a Yoti only theme, or Digital ID Connect brand. "digital-id-uk" is only applicable for UK usage. | 
{% /table %}

**Error codes**

{% table widths="" %}
| Code | Description | Resolution | 
| ---- | ---- | ---- | 
| 400 | Missing url field in the request body | Ensure to POST a JSON body containing a url | 
| 406 | Empty Accept header | Send a request Accept header with the required image return type | 
| 406 | An Accept header was sent with an invalid return type | Ensure the Accept header is one of\n\n\n\n- image/svg+xml\n- image/png | 
{% /table %}

#### Receive the Receipt id

After the user scans a Yoti QR and completes the share, a **webhook notification** is sent to the endpoint specified in the Share session. This will be trigged in the case of either a Completed or Failed share. The JSON notification will contain the receipt id and an optional error code. Example of these are provided [here](https://developers.yoti.com/digital-id/retrieve-the-profile#webhook-notifications).

#### Retrieve the profile

Now, you can use the receipt id to decrypt the user share in your backend and retrieve the profile attributes. This process is explained on [this page](/digital-id/retrieve-the-profile).

---

### Completion handler

Yoti webshare provides a way to avoid automatic redirection on share completion by using a hook function. This can also be used to retrieve the Receipt ID and run your own code logic. For example - you can send the Receipt ID to your backend and use it to decrypt the share receipt. Based on the shared user attributes, you can also render your own UI which is especially helpful for non-browser integrations.

{% code %}
{% tab language="javascript" %}
hooks: {
  // optional, prevents redirection when specified
  completionHandler: (receiptId) => {
    // can send the `receiptId` to the server or do something else
    console.log(receiptId);
  },   
},
{% /tab %}
{% /code %}

---

### Query parameters

You can append query params to the landing page URL that displays the Yoti button. These will be added to the callback URL.

For example if you load the landing page containing the Yoti button as follows:

[https://example.com/?iso=test&user_id=6667](https://example.com/?iso=test&amp;user_id=6667)

The query parameters (iso=test&user_id=6667) will be returned in the callback URL.