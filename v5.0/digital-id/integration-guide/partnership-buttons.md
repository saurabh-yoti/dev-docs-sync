---
type: page
title: Partnership buttons
listed: true
slug: partnership-buttons
description: 
index_title: Partnership buttons
hidden: 
keywords: 
tags: 
---

Yoti offers different skins to our Yoti button. 

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      You will need to download the Yoti app on your phone and register your business with Yoti.
   </div>
   <div class="alert-links"> 
      <a  target="_self" href="https://developers.yoti.com/yoti/getting-started"> Onboarding with Yoti </a>
      <a  target="_self" href="https://developers.yoti.com/yoti/production-keys"> Generate API Keys </a> 
   </div>
</div>
{% /html %}

The new set of Yoti buttons and QR code styles use the client-side JavaScript library provided by Yoti and follow the same structure as described [here](https://developers.yoti.com/digital-id/createbutton).

The addition of the element: **skinId.** The Different options are as follows:

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1631884840/v2_2762/jj9qqt7qg8hc7wznuapq.png" caption="Button options" mode="responsive" height="600" width="890" %}
{% /image %}

{% table %}
| Brand | skinID configuration | 
| ---- | ---- | 
| Yoti | Leave this blank | 
| Partnership | yoti-with-post-office\nTo use this skin your organisation must be in the UK. | 
| Post office | post-office\nIf you would like to use this skin please email us at [clientsupport@yoti.com.](mailto: clientsupport@yoti.com) | 
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