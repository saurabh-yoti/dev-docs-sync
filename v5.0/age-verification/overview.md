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

- Digital ID
- Age estimation
- Identity verification

{% video %}
{% /video %}

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
   </div>
</div>
{% /html %}

After you have created an organisation with us please [contact us](mailto:clientsupport@yoti.com) for API keys including your organisation name. We aim to get you api keys within 1-2 working days.

Yoti will provide:

- API Key
- SDK ID

The overview below sets out the entities and data flows involved.

{% badge type="warning" text="Help" /%} If you need any help please email [clientsupport@yoti.com](mailto:clientsupport@yoti.com).

---

## Technical overview

This section describes the API interactions for a web and mobile web integration. Data is exchanged securely between the relying party (your backend), Yoti and the client (the end user’s browser or mobile device).

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/jtm7qamhga1slicjpdz6/1618833038.png" caption="Technical Flow" mode="responsive" height="1192" width="3242" %}
{% /image %}

A **session** represents one end-to-end request of the age verification service. The session identifier is in the create session request's response. Every time a user elects a method of age verification on your relying business app or website, you will need to create a session with Yoti to perform the checks.

Once the Yoti Client has launched, it will take the end user through the appropriate age capture flow. Once this flow is completed the end user is redirected back to the relying business, so that they may continue their journey. These redirects are defined when generating the session.

The session can be retrieved using the session ID. The response from this endpoint contains information on the age of the user, result and method.

---

## The user flow

The user will be asked to prove their age and is taken through the Yoti verification steps where they will be presented with the options you have selected. You will then need to redirect them to a success or error URL, alternatively you can listen to post messaging from the iframe.

{% image url="https://image-archive.developerhub.io/image/upload/72645/msuyaeqcjw0xpdx4cmml/1608731982.png" caption="Three options" mode="responsive" height="707" width="1126" %}
{% /image %}

{% badge type="info" text="Hint" /%} Yoti offers customisation of this page. See [](/age-verification/launch-the-user-view).

### Digital ID flow

The user will be presented with a QR code, they will need to open the Yoti App and scan the QR code. We provide context and information detailing how the Yoti app works. 

{% video %}
{% /video %}

### Age Estimation Flow

Here the user will take a photo of themselves, this photo is never stored with Yoti. They are provided with steps to complete this process. 

{% video %}
{% /video %}

### Identity verification flow

Here the user will be presented with the option to take a photo / upload their ID. 

{% video %}
{% /video %}

---

## Translations supported

Our service will detect and support translations by browser locale settings.

Supported translations are:

- German (Deutsch) 🇩🇪
- French (Français) 🇫🇷
- Spanish (Español) 🇪🇸 

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