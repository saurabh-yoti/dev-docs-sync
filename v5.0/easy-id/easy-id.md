---
type: page
title: EasyID integration
listed: true
slug: easy-id
description: 
index_title: EasyID integration
hidden: 
keywords: 
tags: 
---

Welcome to the developer documentation for integrating the Identity verification service and EasyID.

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

You can integrate the EasyID integration using [**Yoti SDK's**.](https://developers.yoti.com/identity-verification/integration-guide) Please read this documentation before integrating.

Once you've set up your organisation account on the [Yoti Hub](https://hub.yoti.com/logout), you’re ready to start integrating with EasyID.

The app can be seamlessly integrated with your website, app or custom product so you can perform secure identity checks. You'll be able to request specific details from a users' EasyID app directly from your website or app.

This integration is very similar to the Yoti Digital ID integration. Please review the document below:

Step 1:[ Create EasyID button](https://developers.yoti.com/digital-id/createbutton) {% badge type="info" text="Hint" /%} See configuration below.

Step 2: [Install the SDK](https://developers.yoti.com/digital-id/install-the-sdk)

Step 3: [Retrieve the profile](https://developers.yoti.com/digital-id/retrieve-the-profile)

---

## EasyID button configuration

The new set of Yoti buttons and QR code styles use the client-side JavaScript library provided by Yoti and follow the same structure as described [here](https://developers.yoti.com/digital-id/createbutton).

The addition of the element: **skinId.** The Different options are as follows:

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1621274203/v2_2762/czy4d5wai8nxldsxd61d.png" caption="Button options" mode="600" height="582" width="860" %}
{% /image %}

{% table %}
| Brand | skinID configuration | 
| ---- | ---- | 
| Yoti | Leave this blank | 
| Partnership | yoti-with-post-office | 
| Post office | post-office | 
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