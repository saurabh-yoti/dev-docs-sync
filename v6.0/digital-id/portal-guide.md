---
type: page
title: Portal guide
listed: true
slug: portal-guide
description: 
index_title: Portal guide
hidden: 
keywords: 
tags: 
---

This guide will show you how to get set up using the Digital ID service without code. This service will provide you a Yoti app QR page, your users will scan this and you will receive a receipt transaction of the scan into your Hub account.

The following steps are:

1. Download the Yoti app and create a Yoti.
2. Complete the registration process on our Yoti Hub.
3. Create a QR code page.
4. Managing your data - View your receipts in the hub.

{% badge type="warning" text="Help" /%} If you need any help please email [clientsupport@yoti.com](mailto:clientsupport@yoti.com).

---

## Create your Yoti

1. Download the Yoti app.
2. Add a business email address to create your account.
3. Add an official ID document to your Yoti

Watch the video below to see how to create a Yoti:

{% video %}
{% /video %}

{% badge type="info" text="Hint" /%} If you have any issues with the onboarding of the app please contact our customer service team at [help@yoti.com.](mailto:help@yoti.com)

Below are the download links for our app:

- Download in [App Store](https://apps.apple.com/gb/app/yoti-your-digital-identity/id983980808)
- Download in [Google Play](https://play.google.com/store/apps/details?id=com.yoti.mobile.android.live&amp;hl=en_GB)

---

## Set up

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
      <a  target="_self" href="https://developers.yoti.com/yoti/getting-started"> Onboarding with Yoti </a>
   </div>
</div>
{% /html %}

---

## Create a QR code page

Create a Digital ID application and scenario in the hub. Instructions can be found [here](/yoti-developer-documentation/v6.0/yoti/digital-id/production-keys)[.](https://developers.yoti.com/yoti/production-keys)

You will select: 

- The [auto$](/digital-id/yoti-attributes) that you wish to retrieve from the user.
- Customisation ability to change the logo and background of the QR code page. 

Please ensure you have the following settings in your Digital ID application:

- Please set the domain to: [www.yoti.com](http://www.yoti.com/)
- Please set the callback URL to: [www.yoti.com/connect/thankyou](http://www.yoti.com/connect/thankyou)

Lastly to retrieve the URL of your page:

1. Head over to your scenario (Click **applications**, your application and you will see the **scenario** tab).
2. Click the small arrow in the scenario and press **Edit**.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1602102207/70977/h8ygkzddkcdiogn2rmcx.png" caption="Edit your scenario" mode="responsive" height="557" width="1253" %}
{% /image %}

The URL will be at the top of this page. Copy this URL as it will be the page that users will land on to scan the QR code.

Please see this page as an [example](https://www.yoti.com/connect/32e513d2-4faa-4179-9c0a-cbbb1a673460/scenarios/97483364-1cf0-41cb-be80-bea4babecf78).

---

## Receipts

Whenever details are shared through Yoti, each party involved immediately receives a record of the activity: who they shared with, what was shared, and the date and time the information was shared.

You will see the receipts of your applications in the receipts tab ordered by date. You will need to have your phone connected to Yoti Hub in order to view receipts.

No one at Yoti can ever see your receipts - they are encrypted and we have no access to the key needed to decrypt the receipts. Only you do.

### Download, filter, delete receipts

To download the receipts there is an Export to CSV button - this will download all of the receipts in the selected time period. By default, we display receipts from the last month.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1575293135/20476/etlppfcehkhf9v73yhjn.jpg" caption="Applications &gt; Receipts" mode="responsive" height="652" width="1592" %}
{% /image %}

To filter receipts, you can use our date filter. This will display the receipts from this time period.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1575293186/20476/b1jcberebhi07z52nqlz.jpg" caption="Applications &gt; Receipts" mode="responsive" height="626" width="1620" %}
{% /image %}

You can delete receipts for a certain time period or for a certain user.

To delete receipts by time period, filter the list based on the date range that you want to remove and click the Delete button in the dropdown menu next to Export to CSV.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1575293269/20476/mqu9lssoimdouko4sevh.jpg" caption="Applications &gt; Receipts" mode="responsive" height="626" width="1618" %}
{% /image %}

### Source and verifiers in receipts

To view further information about how Yoti has verified the user's details, you can click on the Show sources and verifiers tick box at the top of an individual receipt.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1575293421/20476/rbtutsg5cpf63vupvqfm.jpg" caption="Applications &gt; Receipts &gt; Click Receipts &gt; Show sources and verifiers" mode="responsive" height="494" width="654" %}
{% /image %}

---

## Complete

Congratulations! You now have set up a Digital ID share page.  

Most of our clients send this page to their customers via email or text to allow them to verify their details.

If you have any questions or need help on the above please email us at [clientsupport@yoti.com](mailto:clientsupport@yoti.com).