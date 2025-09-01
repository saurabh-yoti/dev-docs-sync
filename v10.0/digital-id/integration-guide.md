---
type: page
title: Integration guide
listed: true
slug: integration-guide
description: 
index_title: Integration guide
hidden: 
keywords: 
tags: 
---

Once you've set up your organisation account on the [Yoti Hub](https://hub.yoti.com), you’re ready to start integrating with Yoti.

Our service can be seamlessly integrated with your website, app or custom product so you can perform secure identity checks. You'll be able to request specific details from a users' Yoti app directly from your website or app.

The integrations steps are as follows:

1. Install the SDK
2. Create Yoti QR/button
3. Retrieve the profile

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know... 
    </div>
    <div class="alert-text">
        Following our user experience guidelines makes for a faster and more enjoyable experience for your users. Please read these sections before you continue.
    </div>
    <div class="alert-links"> 
        <a  target="_self" href="https://developers.yoti.com/digital-id/user-experience"> View User Experience </a> 
        <a href="https://developers.yoti.com/digital-id/scenario-examples"> View Scenario examples </a> 
    </div>
</div>
{% /html %}

You will need to create a dynamic Yoti QR/button to allow your users to authenticate with Yoti. This contains a QR code for users to scan with their Yoti app. Mobile web users will skip the QR code scanning step, as they use the Yoti mobile app directly to authenticate.

Yoti offers five options to display the QR code button.

- Modal QR ⭐️ - most popular
- Inline QR
- Instant QR
- Static QR
- Non-browser QR

We also support Digital ID connect and partnership skins for the above QR codes.

{% callout type="info" title="Good to know..." %}
Most of our buttons support a dynamic learn more page. You can check the link below for more information.

[Learn more](/digital-id/user-experience)
{% /callout %}

To see our Digital ID service live in action, check out our official [demos](https://yoti.world/digital-id/).