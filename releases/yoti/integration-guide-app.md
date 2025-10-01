---
type: page
title: Integration guide
listed: true
slug: integration-guide-app
description: 
index_title: Integration guide
hidden: 
keywords: 
tags: 
---

Our app can be seamlessly integrated with your website, app or custom product so you can perform secure identity checks. This is a Yoti App integration. You'll be able to request specific details from a users' Yoti app directly from your website or app.

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
      <a  target="_self" href="https://developers.yoti.com/yoti/generating-the-api-keys"> Generate API Keys </a> 
   </div>
</div>
{% /html %}

The integrations steps are as follows:

[1) Generate a Yoti Button](https://developers.yoti.com/yoti/web-integration#generate-a-yoti-button)

[2) Install the SDK](https://developers.yoti.com/yoti/web-integration#install-sdk)

[3) Retrieve a profile](https://developers.yoti.com/yoti/web-integration#retrieve-a-profile)

## Technical overview

The diagram below describes the login process and how a backend integrated with the Yoti architecture.

{% image url="https://image-archive.developerhub.io/image/upload/12870/j5aji8dciamlodmziekk/1557841032.png" caption="Backend integration process diagram" mode="600" height="1504" width="1244" %}
{% /image %}

---

## How it works

Integrating with Yoti lets your users securely share specific details using their Yoti app. We call these details **attributes**.

To get started, users need to click a **Yoti button** on your website or app. This button opens a full-page overlay on the webpage, showing the details users are about to share.

**On a desktop browser**

This overlay has a two-dimensional barcode that we ask users to scan with the Yoti app. We use these codes to securely pass on information; they're called **Yoti QR codes**.

**On a mobile browser**

Users simply need to tap the **Share details button** to continue. This will launch their Yoti app.

Both methods prompt the Yoti app to display the details users are about to share and a button to confirm the share.

If a user doesn't have the Yoti app, they'll be redirected to a mobile website with more information and download links.

Once they confirm the share, their details are securely sent to your organisation. You can access them through a backend integration or from your **Yoti Hub**.

{% image url="https://image-archive.developerhub.io/image/upload/20473/kgramshxfo4qala15zar/1575299208.jpg" caption="The steps users take on mobile and desktop." mode="600" height="1150" width="1294" %}
{% /image %}

---

## What users will see

When your user clicks the Yoti button on your website or app, a full-page overlay appears. This tell them exactly what details they'll be sharing and who they'll be sharing them with.

{% image url="https://image-archive.developerhub.io/image/upload/20473/viciawwxgwqppmu9tujp/1575299278.jpg" caption="A diagram of our overlay with numbered areas" mode="full" height="1298" width="1324" %}
{% /image %}

1. Your application's logo and name. Make sure they match what's on the website or app your user has come from.
2. The specific details you're requesting users to share.
3. On desktop browsers: a Yoti QR code that users scan with their Yoti app. On mobile browsers: a share button that will automatically open the Yoti app.
4. Your application's contact details and privacy policy. Make sure your provide these.
5. More information for users to find out how Yoti works and how to share details.

Once your user has scanned the Yoti QR code on their desktop or tapped the Share details button on their mobile, the Yoti app automatically presents a share request screen.

{% image url="https://image-archive.developerhub.io/image/upload/20473/tssxstmljcgo0egnqkdx/1575299328.jpg" caption="A diagram of our share details screen in the Yoti app with numbered areas." mode="300" height="952" width="636" %}
{% /image %}

1. Your application's logo and name. Make sure they match what's on the website or app your user has come from.
2. This will only show if you've requested photo authentication in Yoti Hub. If you request this, the user will be asked to scan their face using their front-facing camera.
3. The specific details you're requesting users to share. Any details with a blue tick are verified by Yoti.
4. Tapping Allow shares the requested details with your organisation. The user will then receive a share receipt in their Yoti app.

---

## User journey overview

Yoti can be used in many different situations. It can be used in scenarios where someone would usually share personal, often private, information with an organisation or another person.

{% image url="https://image-archive.developerhub.io/image/upload/20473/mxiacan4oy2nzozyfbaz/1575299455.jpg" caption="A diagram of a generic user flow using Yoti." mode="full" height="798" width="1458" %}
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
        <a href="https://developers.yoti.com/yoti/scenario-examples">View scenario examples</a> 
    </div>
</div>
{% /html %}

---

## Using Yoti responsibly

We pride ourselves on how we handle our users' data. We use tech for good and enable users to securely prove their identity, always being transparent about what happens to their details.

- Be transparent about why you're collecting data and only use this data for those reasons.
- Only collect the information you actually need. Data minimisation is one of the main benefits of Yoti, giving people ownership of their data.
- Make sure the data you collect is stored securely.

{% image url="https://image-archive.developerhub.io/image/upload/20473/vwj6x1hjvfni5rzvlho3/1575299497.jpg" mode="300" height="440" width="438" %}
{% /image %}

$plugin[19ag7p8lxst]