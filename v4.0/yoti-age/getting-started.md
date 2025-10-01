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

Welcome to the developer documentation for integrating Yoti Age.

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
This product is in the BETA stage. Any feedback on the product would be much appreciated.    </div>
    <div class="alert-links"> 
       <a href="mailto:sdksupport@yoti.com">SDK Support contact</a>

    </div>
</div>
{% /html %}

This section will guide you through the implementation steps for our age verification service API on mobile or web.  The options for age verification are:

- [Yoti App](https://www.yoti.com/business/digital-id/)
- [Yoti Age Scan](https://www.yoti.com/business/age-verification/)
- [Yoti Doc Scan](https://www.yoti.com/business/doc-scan/)

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
   </div>
</div>
{% /html %}

After you have created an organisation with us please [contact us](mailto:sdksupport@yoti.com) for API keys including your organisation name. We aim to get you api keys within 1-2 working days.

Yoti will provide:

- API Key
- SDK ID

The overview below sets out the entities and data flows involved.

---

## Technical overview of the Yoti Age architecture

This section describes the API interactions for a web and mobile web integration. Data is exchanged securely between the relying party (your backend), Yoti and the client (the end user’s browser or mobile device).

{% image url="https://image-archive.developerhub.io/image/upload/71150/ee3ofsbgr3brehh4zzm1/1603120413.png" caption="Yoti Age Flow" mode="responsive" height="814" width="2086" %}
{% /image %}

A **session** represents one end-to-end request of the age verification service. The session identifier is in the create session request's response. Every time a user elects a method of age verification on your relying business app or website, you will need to create a session with Yoti to perform the checks.

Once the Yoti Client has launched it will take the end user through the appropriate age capture flow. Once this flow is completed the end user is redirected back to the relying business client so that they may continue their journey. These redirects are defined when generating the session.

The session can be retrieved using the session ID. The response from this endpoint contains information on the age of the user, result and method.

---

## The user flow

The user will be asked to prove their age and is taken through the Yoti verification steps where they will be presented with the options you have selected. You will then need to redirect them to a success or error URL, alternatively you can listen to post messaging from the iframe.

{% image url="https://image-archive.developerhub.io/image/upload/72645/msuyaeqcjw0xpdx4cmml/1608731982.png" caption="Three options" mode="responsive" height="707" width="1126" %}
{% /image %}

### Yoti App flow

The user will be presented with a QR code, they will need to open the Yoti App and scan the QR code. We provide context and information on how the Yoti app works. 

{% image url="https://image-archive.developerhub.io/image/upload/72645/ovsypp8tema9jgyud7ir/1608732275.png" caption="Yoti App flow" mode="responsive" height="702" width="1125" %}
{% /image %}

### Age Estimation Flow

Here the user will take a photo of themselves, this photo is never stored with Yoti. They are provided with steps on how do do this. 

{% image url="https://image-archive.developerhub.io/image/upload/72645/dt83zqzzwstxy3mm3a8s/1608732313.png" caption="Age estimation flow" mode="responsive" height="711" width="1117" %}
{% /image %}

{% image url="https://image-archive.developerhub.io/image/upload/72645/x4f9ynyx48s31vrvnzde/1608732408.png" caption="Age estimation flow part 2" mode="responsive" height="701" width="1115" %}
{% /image %}

### Yoti Doc Scan flow

Here the user will be presented with the option to take a photo / upload their ID. 

{% image url="https://image-archive.developerhub.io/image/upload/72645/b2e3ao8fiilzfxtsqju8/1608732502.png" caption="Yoti Doc Scan flow" mode="responsive" height="750" width="1127" %}
{% /image %}

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

{% image url="https://image-archive.developerhub.io/image/upload/72645/m4wu2a4v4d117o6ma00k/1604402402.png" mode="responsive" height="376" width="384" %}
{% /image %}