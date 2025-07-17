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

Digital ID Connect is a UK network of reusable Digital ID apps that allow businesses and people to trust who they’re connecting with.

The network is built by Yoti, Post Office and Lloyds Bank to make the digital world easier and safer for everybody.

Digital ID Connect buttons and QR code styles use the client-side JavaScript library provided by Yoti and follow the same structure as described [here](/digital-id/createbutton).

You can add the Digital ID Connect button using either the JavaScript approach or the NPM module. See below for both examples.

The configuration of the element `skinId` determines the button and QR code styles. An example is shown below:

{% table widths="326" %}
| Brand | skinId configuration | 
| ---- | ---- | 
| Yoti | `yoti` | 
| Digital ID Connect | `digital-id-uk` | 
{% /table %}

{% callout type="info" title="Info" %}
To use the Digital ID Connect skin, your organisation must operate in the United Kingdom, Isle of Man or the Channel Islands
{% /callout %}

{% code %}
{% tab language="json" title="Simple button" %}
<!-- Simple Modal Button Generation -->

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
          skinId: "digital-id-uk"
        }
      ]
    });
  </script>
</body>
{% /tab %}
{% tab language="javascript" title="Node.js / NPM Module" %}
// Install the Yoti Share Client Core module
npm install @getyoti/share-client-core

// Import and use in your JavaScript/TypeScript project
import { startYotiModalShare } from '@getyoti/share-client-core';

await startYotiModalShare({
  clientSdkId: 'xxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx',
  domId: 'xxx',
  controls: {
    scenarioId: 'xxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx',
  },
  options: {
    skin: 'digital-id-uk',
    displayLearnMoreLink: true,
    button: {
      width: 'full'
    },
  },
});

// Note: Make sure to have a <div id="xxx"></div> in your HTML
{% /tab %}
{% /code %}