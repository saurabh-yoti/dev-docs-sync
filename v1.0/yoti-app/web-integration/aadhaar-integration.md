---
type: page
title: Aadhaar Integration
listed: true
slug: aadhaar-integration
description: 
index_title: Aadhaar Integration
hidden: 
keywords: 
tags: 
---

If you are doing an Aadhaar integration this document should clarify any queries you have on integration.

There’s not much difference between a standard Yoti integration and a business that wishes to integrate Yoti and accept customers who have on-boarded with their Aadhaar card. From an integration perspective, the steps remain the same. The main difference here is about the attribute types you select in the Yoti Hub. This document will outline the steps you need to take to onboard your organisation with Yoti.

---

## Onboarding with Yoti

First, you will need to have the free Yoti app on your phone. If you haven’t got it already, you can find it on both the [App Store](https://itunes.apple.com/gb/app/yoti-your-digital-identity-app/id983980808) and [Google Play](https://play.google.com/store/apps/details?id=com.yoti.mobile.android.live).

There are two different methods you can use to add your Aadhaar through the Yoti app. These are:

- Uploading Aadhaar File - Download your Aadhaar file from the UIDAI website and upload it, then we’ll verify your details. This should only take a few minutes.
- Scan Aadhaar Card - Scan the QR code on the Aadhaar card to instantly add your details, which will be unverified. Some businesses will only accept verified details.

{% video %}
{% /video %}

---

## Registering your business with Yoti

Open the Yoti app on your phone, tap Scan Code and scan the QR code displayed on your desktop screen via the following url:[https://hub.yoti.com/login-organisations](https://hub.yoti.com/login-organisations). Please head over to [this section](/yoti-app/web-integration#step-1-creating-an-organisation) for more information.

Any individual can register on behalf of your business but will need to have company information available to them. For example, the registered company name and director details in order to complete the onboarding process.

_**Please note: The individual registering for the Yoti Organisation must have on-boarded with Yoti using their valid passport rather than Aadhaar card currently.**_

---

## Creating an application

Once you have created your organisation, the next step is to create an application. Head over to [https://hub.yoti.com/login](https://hub.yoti.com/login) on your desktop computer and follow the next steps. Please head over to [this section](/yoti-app/web-integration#step-2-creating-an-application) for more information.

If you would like to support customers who may have on-boarded for Yoti using their Aadhaar card, you will need to make sure that the attributes (where applicable) are set to Allow unverified {attribute name}. As an example, please see a subset of available attributes below where support for unverified has been selected:

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1567084209/18168/idoxf6vir2lbkh4dwszq.jpg" mode="responsive" height="408" width="506" %}
{% /image %}

Attributes supported from the Aadhaar card:

{% table %}
| Attribute | Description | 
| ---- | ---- | 
| full_name | &lt;p&gt;The user's full name. If family_name/given_names are&nbsp;&lt;span&gt;present, this will be equal to the string ${given_names} + " " + ${family_name}.&lt;/span&gt;&lt;/p&gt; | 
| gender&lt;br&gt; | Corresponds to the gender on the registered document; will be one of the strings "MALE", "FEMALE", "TRANSGENDER" or "OTHER". | 
| date_of_birth | Date of birth of the user.&lt;br&gt; | 
| structured_postal_address | Please see the following &lt;a href="https://app.developerhub.io/Corresponds%20to%20the%20gender%20in%20the%20registered%20document;%20will%20be%20one%20of%20the%20strings%20%22MALE%22,%20%22FEMALE%22,%20%22TRANSGENDER%22%20or%20%22OTHER%22."&gt;section&lt;/a&gt;. | 
{% /table %}

You can now complete the integration as normal from [step 3](/yoti-app/web-integration#step-3-front-end-integration).

---

## Example integration video

Please see the below for an example of an integration:

{% video %}
{% /video %}

If you would like to try a demo, please download Yoti and add your Aadhaar card then try this: [https://yoti.world/aadhaar/](https://yoti.world/aadhaar/)

---

## Support

For more information, you can check out our [Developer FAQs](https://yoti.zendesk.com/hc/en-us/categories/115000656265-Developer-FAQs).

If you have any other questions please do not hesitate to contact [sdksupport@yoti.com](mailto:sdksupport@yoti.com).

_Once we have answered your question we may contact you again to discuss Yoti products and services. If you’d prefer us not to do this, please let us know when you e-mail._