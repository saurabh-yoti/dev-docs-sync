---
type: page
title: Getting started
listed: true
slug: getting-started
description: 
index_title: Getting started
hidden: 
keywords: 
tags: 
---

Welcome to the developer documentation for integrating the Yoti app.

You can integration Yoti App in **two** ways:

- Integration with our [**Yoti SDK's**.](https://developers.yoti.com/yoti-doc-scan/quick-start)
- Use our [portal](https://developers.yoti.com/yoti-app/yoti-app-portal) (code free).

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      You will need to download the Yoti app on your phone and register your business with Yoti.
   </div>
   <div class="alert-links"> 
      <a  target="_self" href="https://developers.yoti.com/yoti/getting-started-hub"> Onboarding with Yoti </a>
      <a  target="_self" href="https://developers.yoti.com/yoti/generating-the-api-keys-hub"> Generate API Keys </a> 
   </div>
</div>
{% /html %}

{% html %}
<div class="alert-SAND">
    <div class="alert-title" id="SAND">
      Sandbox
    </div>
    <div class="alert-text">
       We offer a sandbox for Yoti App integration. If you wish to integrate sandbox please click the link below.
    </div>
    <div class="alert-links"> 
        <a target="_self" href="https://developers.yoti.com/yoti-app/sandbox">Sandbox</a> 
    </div>
</div>
{% /html %}

The overview below sets out the entities and data flows involved.

## Technical overview of Yoti App architecture

The diagram below describes the login process and how a backend integrated with the Yoti architecture.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1557841032/12870/j5aji8dciamlodmziekk.png" caption="Backend integration process diagram" mode="600" height="1504" width="1244" %}
{% /image %}

Integrating with Yoti lets your users securely share specific details using their Yoti app. We call these details **attributes**.

To get started, users need to click a **Yoti button** on your website or app. This button opens a full-page overlay on the webpage, showing the details users are about to share.

**On a desktop browser**

This overlay has a two-dimensional barcode that we ask users to scan with the Yoti app. We use these codes to securely pass on information; they're called **Yoti QR codes**.

**On a mobile browser**

Users simply need to tap the **Share details button** to continue. This will launch their Yoti app.

Both methods prompt the Yoti app to display the details users are about to share and a button to confirm the share.

If a user doesn't have the Yoti app, they'll be redirected to a mobile website with more information and download links.

Once they confirm the share, their details are securely sent to your organisation. You can access them through a backend integration or from your **Yoti Hub**.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1575299208/20473/kgramshxfo4qala15zar.jpg" caption="The steps users take on mobile and desktop." mode="600" height="1150" width="1294" %}
{% /image %}

---

## The user flow

When your user clicks the Yoti button on your website or app, a full-page overlay appears. This tell them exactly what details they'll be sharing and who they'll be sharing them with.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1575299278/20473/viciawwxgwqppmu9tujp.jpg" caption="A diagram of our overlay with numbered areas" mode="full" height="1298" width="1324" %}
{% /image %}

1. Your application's logo and name. Make sure they match what's on the website or app your user has come from.
2. The specific details you're requesting users to share.
3. On desktop browsers: a Yoti QR code that users scan with their Yoti app. On mobile browsers: a share button that will automatically open the Yoti app.
4. Your application's contact details and privacy policy. Make sure your provide these.
5. More information for users to find out how Yoti works and how to share details.

Once your user has scanned the Yoti QR code on their desktop or tapped the Share details button on their mobile, the Yoti app automatically presents a share request screen.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1575299328/20473/tssxstmljcgo0egnqkdx.jpg" caption="A diagram of our share details screen in the Yoti app with numbered areas." mode="300" height="952" width="636" %}
{% /image %}

1. Your application's logo and name. Make sure they match what's on the website or app your user has come from.
2. This will only show if you've requested photo authentication in Yoti Hub. If you request this, the user will be asked to scan their face using their front-facing camera.
3. The specific details you're requesting users to share. Any details with a blue tick are verified by Yoti.
4. Tapping Allow shares the requested details with your organisation. The user will then receive a share receipt in their Yoti app.

Yoti can be used in many different situations. It can be used in scenarios where someone would usually share personal, often private, information with an organisation or another person.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1575299455/20473/mxiacan4oy2nzozyfbaz.jpg" caption="A diagram of a generic user flow using Yoti." mode="full" height="798" width="1458" %}
{% /image %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
        You have control over what you want your users to see before they use Yoti. Please read our page on scenarios to ensue you provide the correct information, using the correct layout.
    </div>
    <div class="alert-links"> 
        <a href="https://developers.yoti.com/yoti-app/scenario-examples">View scenario examples</a> 
    </div>
</div>
{% /html %}

---

## Supported Browsers

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1608728857/72625/rypdac67giybzfpxz5tg.png" caption="Supported browsers" mode="responsive" height="1256" width="1178" %}
{% /image %}

---

## Using Yoti responsibly

We pride ourselves on how we handle our users' data. We use tech for good and enable users to securely prove their identity or age, always being transparent about what happens to their details.

- Be transparent about why you're collecting data and only use this data for those reasons.
- Only collect the information you actually need. Data minimisation is one of the main benefits of Yoti, so people don't have to provide more information than is actually necessary.
- Make sure any information you export to your own systems is stored securely. Data security is at the heart of what we do and we think it should be important to every organisation.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1575299497/20473/vwj6x1hjvfni5rzvlho3.jpg" mode="300" height="440" width="438" %}
{% /image %}

$plugin[19ag7p8lxst]