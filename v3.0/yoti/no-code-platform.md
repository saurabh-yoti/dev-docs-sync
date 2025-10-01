---
type: page
title: No code platform
listed: true
slug: no-code-platform
description: 
index_title: No code platform
hidden: 
keywords: 
tags: 
---

If you would like to use Yoti app as your integrated service without code, please see the below on how to achieve this.

This integration will provide you a Yoti app QR page, your users will scan this and you will receive a receipt of the scan into your Hub account. 

The following steps are:

1. [Download the Yoti app and create a Yoti.](https://developers.yoti.com/yoti/code-free-integration#download-yoti)
2. [Complete the registration process on our Yoti Hub](https://developers.yoti.com/yoti/code-free-integration#register-with-the-hub)
3. [Create a QR code page.](https://developers.yoti.com/yoti/code-free-integration#create-an-qr-code-page)
4. [Managing your data](https://developers.yoti.com/yoti/code-free-integration#managing-your-data) - View your receipts in the hub.

---

## Download Yoti

Below are the download links for our app:

[ Download in App Store ](https://apps.apple.com/gb/app/yoti-your-digital-identity/id983980808)

[ Download in Google Play ](https://play.google.com/store/apps/details?id=com.yoti.mobile.android.live&amp;hl=en_GB)

Follow our onboarding process, add your official ID document, a mobile number and an email address to your account.

---

## Register with the hub

1. [**Open Yoti Hub**](https://hub.yoti.com/login-organisations) on a desktop or laptop.
2. Scan the QR code using your Yoti app.
3. Complete the registration on Yoti Hub.

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Jump to
   </div>
   <div class="alert-text" >
      For a step by step guide on how to onboard with the hub head over to the Getting started section.
   </div>
   <div class="alert-links"> 
      <a  target="_self" href="https://developers.yoti.com/yoti/getting-started-hub"> Onboarding with Yoti </a>
   </div>
</div>
{% /html %}

---

## Create an QR code page

Create a Yoti App application in the hub and scenario. Instructions on how to do this is located [here](https://developers.yoti.com/yoti/generate-api-keys#1-create-a-yoti-application).

You will select: 

- Attributes that you wish to retrieve from the user.
- Customisation ability to change the logo and background of the QR code page. 

Please ensure you have the following settings in your Yoti app application:

- Please set the domain to: [www.yoti.com](http://www.yoti.com/)
- Please set the callback URL to: [www.yoti.com/connect/thankyou](http://www.yoti.com/connect/thankyou)

Lastly to retrieve the URL of your page:

1. Head over to your scenario (Click applications, your application and you will see the scenario tab).
2. Click the small arrow in the scenario and press Edit.

{% image url="https://image-archive.developerhub.io/image/upload/70977/h8ygkzddkcdiogn2rmcx/1602102207.png" caption="Edit your scenario" mode="responsive" height="557" width="1253" %}
{% /image %}

1. The URL will be at the top of this page. Copy this URL as it will be the page that users will land on to scan the QR code.

Please see this page as an [example](https://www.yoti.com/connect/32e513d2-4faa-4179-9c0a-cbbb1a673460/scenarios/97483364-1cf0-41cb-be80-bea4babecf78).

---

## Managing your data

In order to view your user transactions Yoti has what we call receipts. Here are some useful documentation for you to read and follow to understand your way around the hub.

- [General attributes](https://developers.yoti.com/yoti/knowledge-base-hub#general-attributes)
- [View receipts ](https://developers.yoti.com/yoti/knowledge-base-hub#customer-receipts)
- [Download, filter and delete receipts](https://developers.yoti.com/yoti/knowledge-base-hub#download-filter-delete-receipts)
- [Add members to your hub](https://developers.yoti.com/yoti/knowledge-base-hub#settings)
- [Delete your application](https://developers.yoti.com/yoti/knowledge-base-hub#deleting-your-application)
- [View source and verifiers in the hub](https://developers.yoti.com/yoti/knowledge-base-hub#source-and-verifiers-in-receipts)