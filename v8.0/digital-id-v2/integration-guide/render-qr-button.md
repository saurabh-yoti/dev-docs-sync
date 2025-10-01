---
type: page
title: Render QR button
listed: true
slug: render-qr-button
description: 
index_title: Render QR button
hidden: 
keywords: 
tags: 
---

{% callout type="info" title="Good to know" %}
A Yoti QR code is valid for 3 minutes until the user is asked to refresh.
{% /callout %}

Yoti provides a QR/button generation script to be included in your HTML file. In the examples below, this script has been added to the head of the HTML document.

To render the Yoti QR or button,  please take a look at our range of options below and pick a configuration.

This JavaScript library needs to be invoked – you can do this by calling Yoti.createWebShare() in the body of your HTML document. For the config, you will need to specify a ‘domId’ so the script knows where to add the Yoti button on your page.

The Yoti button requires the hosting page to be accessed via HTTPS, so please make sure that your web application has HTTPS enabled.

{% table widths="189,0" %}
| Name | Purpose | Required | 
| ---- | ---- | ---- | 
| name | Identifies the Yoti share on the page. | ✅ | 
| domID | Specifies the ID of the DOM node where Yoti webshare has to be rendered. | ✅ | 
| clientSdkId | Identifies your Yoti Hub application. This value can be found in the Hub, within your application section, in the keys tab. | ✅ | 
| hooks | Object for specifying the functions hooks to be called by Yoti webshare. | ✅ | 
| hooks - sessionIdResolver | Hook Function to resolve the Session ID generated from the creating a Share session using the Yoti backend SDK. | ✅ | 
| hooks - completionHandler | Allows you to retrieve the Share Receipt ID within the hook function and prevents the automatic redirection to Session Redirect URI. | ❌ | 
| hooks - errorListener | Allows you to listen to error messages from the Webshare QR/button. | ❌ | 
| flow | Specifies the type of rendering mode for Yoti QR/button and corresponding share flow. Default is modal. | ❌ | 
| skinId | The theme to be used for the webshare rendering. | ❌ | 
{% /table %}

Finally, the domain and port pair where the button is deployed (i.e. [https://localhost:8000](https://localhost:8000/)) must match the one that you have configured in Yoti Hub. This prevents other web sites from embedding your Yoti button.

---

### Supported Translations (Locale)

Yoti offers the ability to force a language locale for the front-end webshare client - see list here:

{% table %}
| Language | Parameter | 
| ---- | ---- | 
| English | en-GB (default) | 
| French (Français) | fr | 
| Spanish (Español) | es | 
| German (Deutsch) | de | 
| Czech (čeština) | cz | 
| Polish (polski) | pl | 
{% /table %}

---

### Modal QR

The modal QR code option has a button which when clicked opens a modal pop out window with the QR code present. There are three tabs, describing how to scan the QR code, The QR code & attributes to be shared and about Yoti.

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
          hooks: {
            sessionIdResolver: onSessionIdResolver,
            errorListener: onErrorListener
          },
          flow: "REVEAL_MODAL"
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

The inline QR code option has a button which when clicked opens just the QR code. You will need to provide more context as to what Yoti button is for. See the example below:

{% image url="https://image-archive.developerhub.io/image/upload/20477/vwoytddmqogp7sjjrblk/1585935832.jpg" caption="Inline QR code" mode="300" height="312" width="468" %}
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
          hooks: {
            sessionIdResolver: onSessionIdResolver,
            errorListener: onErrorListener
          },
          flow: "REVEAL_INLINE_QR"
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

The instant QR code option is just the QR code with no button. You will need to provide more context as to what Yoti QR is for. See the example below:

{% image url="https://image-archive.developerhub.io/image/upload/20477/bifs7i78su52yjcwsbyl/1588180782.png" caption="Instant QR code" mode="300" height="365" width="296" %}
{% /image %}

{% code %}
{% tab language="html" title="" %}
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
          hooks: {
            sessionIdResolver: onSessionIdResolver,
            errorListener: onErrorListener
          },
          flow: "INLINE_QR"
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

### Query parameters

You can append query params to the landing page URL that displays the Yoti button. These will be added to the callback URL.

For example if you load the landing page containing the Yoti button as follows:

[https://example.com/?iso=test&user_id=6667](https://example.com/?iso=test&amp;user_id=6667)

The query parameters (iso=test&user_id=6667) will be returned in the callback URL.