---
type: page
title: Digital ID Connect button
listed: true
slug: digital-id-connect-button
description: 
index_title: Digital ID Connect button
hidden: 
keywords: 
tags: 
---

[Digital ID Connect](https://www.digitalidconnect.com) is a UK network of reusable Digital ID apps that allow businesses and people to trust who they’re connecting with.

The network is built by Yoti, Post Office and Lloyds Bank to make the digital world easier and safer for everybody.

Digital ID Connect buttons and QR code styles use the client-side JavaScript library provided by Yoti and follow the same structure as described [here](/digital-id/render-qr-button-modal).

The configuration of the element `skinId` determines the button and QR code styles. An example is shown below:

{% table widths="326" %}
| Brand | skinId configuration | 
| ---- | ---- | 
| Yoti | `yoti` | 
| Digital ID Connect | `digital-id-uk` | 
{% /table %}

{% callout type="info" title="Info" %}
To use the Digital ID Connect skin, your organisation must operate in the United Kingdom, Isle of Man or the Channel Islands.
{% /callout %}

### Modal QR

{% code %}
{% tab language="json" title="Simple button" %}
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