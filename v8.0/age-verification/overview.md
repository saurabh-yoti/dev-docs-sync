---
type: page
title: Overview
listed: true
slug: overview
description: 
index_title: Overview
hidden: 
keywords: 
tags: 
---

Welcome to the developer documentation for integrating our Age verification as a service solution.

Yoti Age Verification gives people simple ways to prove their age, using things like a selfie or a mobile number. Designed to only share the result of the age check with a business, it’s an easy way to deliver age-appropriate services without collecting user data.

This section will guide you through the implementation steps for our age verification service API on mobile or web, and leverages our hosted web user interface. This product incorporates multiple Yoti products and provides all user interaction.

{% html %}
<div style="padding:56.25% 0 0 0;position:relative;"><iframe src="https://player.vimeo.com/video/647389673?h=f636f24ed1&amp;badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=58479&dnt=1" frameborder="0" allow="autoplay; fullscreen; picture-in-picture" allowfullscreen style="position:absolute;top:0;left:0;width:100%;height:100%;" title="Yoti Age Portal"></iframe></div><script src="https://player.vimeo.com/api/player.js"></script>
{% /html %}

The six services that can be added to the age verification service are:

{% table %}
| Service | Description | 
| ---- | ---- | 
| Age estimation | User has their age estimated based on facial analysis from a real-time selfie. | 
| Digital ID | User shares an Over Age from their Yoti app by scanning a QR code. | 
| Identity document verification | User uploads a scan of their ID document and a selfie (optional). | 
| Credit card check | User enters their credit card details which are verified against the database. | 
| Mobile provider | User enters their mobile number which are verified against the database. | 
| Database check | User’s details are checked against a database. | 
{% /table %}

Three types of age checks are available:

- A standard **AGE** check that returns the age of a user.
- An **OVER** check that informs you if a user is over a defined age threshold, but protects the user’s details by not sharing their actual age is not shared.
- An **UNDER** check that informs you if a user is under a defined age threshold, but protects the user’s details by not sharing their actual age is not shared.

The overview below sets out the entities and data flows involved.

{% badge type="warning" text="Help" /%} If you need any help please contact us [here](https://yoti.force.com/yotisupport/s/contactsupport).

---

## Technical overview

This section describes the API interactions for a web and mobile web integration. Data is exchanged securely between the relying party (your backend), Yoti and the client (the end user’s browser or mobile device).

{% image url="https://uploads.developerhub.io/prod/kvAX/p9iro8hv5fx822xx17shodjesl4fa58jpz6t9ani36qsxjvrfibgw5039vwfixon.png" caption="Technical Flow" mode="600" height="184" width="759" %}
{% /image %}

A **session** represents one end-to-end request of the age verification service. The session identifier is in the create session request's response. Every time a user elects a method of age verification on your relying business app or website, you will need to create a session with Yoti to perform the checks.

Once the Yoti Client has launched, it will take the end user through the appropriate age capture flow. Once this flow is completed the end user is redirected back to the relying business, so that they may continue their journey. These redirects are defined when generating the session.

The session can be retrieved using the session ID. The response from this endpoint contains information on the age of the user, result and method.

---

## Feature list

The Age verification service is very adaptable, please see below for features available for you to configure within your session.

{% table %}
| Feature | Description | Data requested | Data received | 
| ---- | ---- | ---- | ---- | 
| Age estimation | User has their age estimated based on facial analysis from a real-time selfie. | Real-time selfie using camera on device. | Over or under age, or the age itself. | 
| Digital ID | User shares an Over Age from their Digital ID app by scanning a QR code. | ID document and biometric selfie in the Digital ID app. | Over or under age, or the age itself. | 
| ID verification | User uploads a scan of their ID document and a selfie (optional). | ID document and biometric selfie. | Over or under age, or the age itself. | 
| Credit card check | User enters their credit card details which are verified against the database.\n\nPlease email us if you want this enabled. | PAN number, expiry date, CV2 number, zip code. | Over 18 | 
| Database check | User’s details are checked against a database. | Name, address, and date of birth. | Over or under age, or the age itself. | 
| Mobile provider | User enters their mobile number which are verified against the database. | Mobile provider details. | Over or under age, or the age itself. | 
| Age tokens | When someone uses the service to prove their age, an age token is added to their browser. \n\n\n\nThis acts as a digital proof that they’ve been age checked by Yoti, and lets them freely access your site without having to prove their age every time. | N/A | N/A | 
| Age accounts | Users can store their age tokens in an age account. This allows users to access your website on another browser or device, without having to prove your age again. | N/A | N/A | 
{% /table %}

---

## The user flow

The user will be asked to prove their age and is taken through the Yoti verification steps where they will be presented with the options you have selected. You will then need to redirect them to a success or error URL, alternatively you can listen to post messaging from the iframe.

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/f2s1by8zdu85fc6xcqzt/1632336092.png" caption="Age verification options" mode="responsive" height="1148" width="1910" %}
{% /image %}

{% badge type="info" text="Hint" /%} Yoti offers customisation of this page. See [auto$](/age-verification/launch-the-user-view).

Our product will walk the user through their chosen option of age verification. 

{% image url="https://uploads.developerhub.io/prod/kvAX/15s7yteht954dqgrdh38brisd7kv5hbc13efku6n44pc2faqdm1pljqt8b3h1z00.png" mode="responsive" height="490" width="1181" %}
{% /image %}

---

## Translations supported

Our service will detect and support translations by browser locale settings.

Supported translations are:

- Arabic (العربية) 🇸🇦
- Brazilian Portuguese (Português Brasileiro) 🇧🇷
- Chinese (中文) 🇨🇳
- Danish (Dansk) 🇩🇰
- Finnish (Suomi) 🇫🇮
- French (Français) 🇫🇷
- German (Deutsch) 🇩🇪
- Italian (Italiano) 🇮🇹
- Japanese (日本語) 🇯🇵
- Korean (한국어) 🇰🇷
- Latin-American Spanish (Español Latinoamericano)
- Polish (Polski) 🇵🇱
- Portuguese (Português) 🇵🇹
- Russian (Русский) 🇷🇺
- Spanish (Español) 🇪🇸
- Swedish (Svenska) 🇸🇪
- Tagalog 🇵🇭
- Thai (ไทย) 🇹🇭
- Turkish (Türkçe) 🇹🇷
- Vietnamese (Tiếng Việt) 🇻🇳

Please note: Some age verification methods may not be available in all the languages listed above. For queries around supported languages, please contact us via [support.yoti.com](https://support.yoti.com).

---

## Supported browsers

{% image url="https://image-archive.developerhub.io/image/upload/72645/qgn0rlp4llje2hmtuxpi/1608731632.png" caption="Supported browsers" mode="600" height="940" width="1152" %}
{% /image %}

---

## Using Yoti responsibly

We pride ourselves on how we handle our users' data. We use tech for good and enable users to securely prove their identity or age, always being transparent about what happens to their details.

- Be transparent about why you're collecting data and only use this data for those reasons.
- Only collect the information you actually need. Data minimisation is one of the main benefits of Yoti, so people don't have to provide more information than is actually necessary.
- Make sure any information you export to your own systems is stored securely. Data security is at the heart of what we do and we think it should be important to every organisation.

{% image url="https://image-archive.developerhub.io/image/upload/72645/m4wu2a4v4d117o6ma00k/1604402402.png" mode="300" height="376" width="384" %}
{% /image %}