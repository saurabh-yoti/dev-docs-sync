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

This section will guide you through the implementation steps for our age verification service API on mobile or web. This product incorporates multiple Yoti products and provides all user interaction.  

The services that can be added to the age verification service are:

{% table %}
| Service | Description | 
| ---- | ---- | 
| Digital ID | User shares an Over Age from their Yoti app by scanning a QR code. | 
| Age estimation | User has their age estimated based on facial analysis from a real-time selfie. | 
| Identity document verification | User uploads a scan of their ID document and a selfie (optional). | 
| Credit card check | User enters their credit card details which are verified against the database. | 
| Mobile provider | User enters their mobile number which are verified against the database. | 
| Database check | User’s details are checked against a database. | 
{% /table %}

{% html %}
<div style="padding:56.25% 0 0 0;position:relative;"><iframe src="https://player.vimeo.com/video/647389673?h=f636f24ed1&amp;badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=58479" frameborder="0" allow="autoplay; fullscreen; picture-in-picture" allowfullscreen style="position:absolute;top:0;left:0;width:100%;height:100%;" title="Yoti Age Portal"></iframe></div><script src="https://player.vimeo.com/api/player.js"></script>
{% /html %}

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      You will need to download the Yoti app on your phone and register your business with Yoti.
   </div>
   <div class="alert-links"> 
      <a  target="_self" href="https://developers.yoti.com/yoti/age-verification/getting-started"> Onboarding with Yoti </a>
   </div>
</div>
{% /html %}

The overview below sets out the entities and data flows involved.

{% badge type="warning" text="Help" /%} If you need any help please email [clientsupport@yoti.com](mailto:clientsupport@yoti.com).

---

## Technical overview

This section describes the API interactions for a web and mobile web integration. Data is exchanged securely between the relying party (your backend), Yoti and the client (the end user’s browser or mobile device).

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1618833038/v2_2762/jtm7qamhga1slicjpdz6.png" caption="Technical Flow" mode="responsive" height="1192" width="3242" %}
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
| Digital ID | User shares an Over Age from their Digital ID app by scanning a QR code. | ID document and biometric selfie. | Over or under age, or the age itself. | 
| Age estimation | User has their age estimated based on facial analysis from a real-time selfie. | Real-time selfie using camera on device. | Over or under age, or the age itself. | 
| ID verification | User uploads a scan of their ID document and a selfie (optional). | ID document and biometric selfie. | Over or under age, or the age itself. | 
| Credit card check | User enters their credit card details which are verified against the database.\n\nPlease email us if you want this enabled. | PAN number, expiry date, CV2 number, zip code. | Over 18 | 
| Database check | User’s details are checked against a database. | Name, address, and date of birth. | Over or under age, or the age itself. | 
| Mobile provider | User enters their mobile number which are verified against the database. | Mobile provider details. | Over or under age, or the age itself. | 
| Age tokens | When someone uses the service to prove their age, an age token is added to their browser. \n\n\n\nThis acts as a digital proof that they’ve been age checked by Yoti, and lets them freely access your site without having to prove their age every time. | N/A | N/A | 
{% /table %}

---

## The user flow

The user will be asked to prove their age and is taken through the Yoti verification steps where they will be presented with the options you have selected. You will then need to redirect them to a success or error URL, alternatively you can listen to post messaging from the iframe.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1632336092/v2_2762/f2s1by8zdu85fc6xcqzt.png" caption="Age verification options" mode="responsive" height="1148" width="1910" %}
{% /image %}

{% badge type="info" text="Hint" /%} Yoti offers customisation of this page. See [](/age-verification/launch-the-user-view).

### Digital ID flow

The user will be presented with a QR code, they will need to open the Yoti App and scan the QR code. We provide context and information detailing how the Yoti app works.

{% html %}
<div style="padding:56.25% 0 0 0;position:relative;"><iframe src="https://player.vimeo.com/video/647416655?h=a65d8071f2&amp;badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=58479" frameborder="0" allow="autoplay; fullscreen; picture-in-picture" allowfullscreen style="position:absolute;top:0;left:0;width:100%;height:100%;" title="AVS_YOTI_APP_SHORT.mp4"></iframe></div><script src="https://player.vimeo.com/api/player.js"></script>
{% /html %}

### Age Estimation Flow

Here the user will take a photo of themselves, this photo is never stored with Yoti. They are provided with steps to complete this process. 

{% html %}
<div style="padding:56.25% 0 0 0;position:relative;"><iframe src="https://player.vimeo.com/video/647416816?h=beb50a0088&amp;badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=58479" frameborder="0" allow="autoplay; fullscreen; picture-in-picture" allowfullscreen style="position:absolute;top:0;left:0;width:100%;height:100%;" title="AVS_AGE_ESTIMATION_SHORT.mp4"></iframe></div><script src="https://player.vimeo.com/api/player.js"></script>
{% /html %}

### Identity verification flow

Here the user will be presented with the option to take a photo / upload their ID. 

{% html %}
<div style="padding:56.25% 0 0 0;position:relative;"><iframe src="https://player.vimeo.com/video/647416549?h=e408543512&amp;badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=58479" frameborder="0" allow="autoplay; fullscreen; picture-in-picture" allowfullscreen style="position:absolute;top:0;left:0;width:100%;height:100%;" title="AVS_IDV_SHORT.mp4"></iframe></div><script src="https://player.vimeo.com/api/player.js"></script>
{% /html %}

---

## Translations supported

Our service will detect and support translations by browser locale settings.

Supported translations are:

- German (Deutsch) 🇩🇪
- French (Français) 🇫🇷
- Spanish (Español) 🇪🇸 
- Italian (Italiano) 🇮🇹

---

## Supported browsers

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1608731632/72645/qgn0rlp4llje2hmtuxpi.png" caption="Supported browsers" mode="600" height="940" width="1152" %}
{% /image %}

---

## Using Yoti responsibly

We pride ourselves on how we handle our users' data. We use tech for good and enable users to securely prove their identity or age, always being transparent about what happens to their details.

- Be transparent about why you're collecting data and only use this data for those reasons.
- Only collect the information you actually need. Data minimisation is one of the main benefits of Yoti, so people don't have to provide more information than is actually necessary.
- Make sure any information you export to your own systems is stored securely. Data security is at the heart of what we do and we think it should be important to every organisation.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1604402402/72645/m4wu2a4v4d117o6ma00k.png" mode="300" height="376" width="384" %}
{% /image %}