---
type: page
title: Partnership button
listed: true
slug: partnership-button
description: 
index_title: Partnership button
hidden: 
keywords: 
tags: 
---

Yoti offers different skins to our Yoti button. 

The new set of Yoti buttons and QR code styles use the client-side JavaScript library provided by Yoti and follow the same structure as described [here](/yoti-developer-documentation/v6.0/digital-id/lcreatebutton).

The addition of the element: **skinId.** The Different options are as follows:

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1631884840/v2_2762/jj9qqt7qg8hc7wznuapq.png" caption="Button options" mode="responsive" height="600" width="890" %}
{% /image %}

{% table %}
| Brand | skinID configuration | 
| ---- | ---- | 
| Yoti | Leave this blank | 
| Partnership | yoti-with-post-office\nTo use this skin your organisation must be in the UK. | 
| Post office | post-office\nIf you would like to use this skin please email us at [clientsupport@yoti.com](mailto:clientsupport@yoti.com) | 
{% /table %}

{% code %}
{% tab language="json" title="Simple button" %}
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
          skinId:"yoti-with-post-office"

        }
      ]
    });
  </script>
</body>
{% /tab %}
{% /code %}