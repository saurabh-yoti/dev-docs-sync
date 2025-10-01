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

Welcome to the developer documentation for integrating Yoti Doc Scan. 

You can integration Yoti Doc Scan in **three** ways:

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/ciy2mvdfatfdcus9pa2s/1613069708.png" mode="300" height="136" width="472" %}
{% /image %}

- Integration with our [**Yoti SDK's**.](https://developers.yoti.com/yoti-doc-scan/quick-start)
- Integrate with our **API.** Contact [us](https://developers.yoti.com/yoti/get-in-touch) for more information. 
- Use the **[Portal](https://developers.yoti.com/yoti-doc-scan/no-code-platform)** (code free). 

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      You will need the Yoti App on your phone and to have registered your business with Yoti. Click here for more info.
   </div>
   <div class="alert-links"> 
         <a target="_self" href="https://developers.yoti.com/yoti/getting-started-hub">View Onboarding with Yoti</a>
      <a target="_self" href="https://developers.yoti.com/yoti/generate-api-keys-hub">View Generate API Keys</a> 
   </div>
</div>
{% /html %}

The overview below sets out the entities and data flows involved.

---

## Technical overview of the Doc Scan architecture

This section describes the SDK interactions for a web, mobile web and native mobile integration. Exchanges of data will occur securely between the relying party (your backend), Yoti and the client (the end user’s browser or mobile device).

{% image url="https://image-archive.developerhub.io/image/upload/72631/sjpf6er8nekr9boxyv10/1608066500.png" caption="Yoti Doc Scan walkthrough" mode="responsive" height="1334" width="1032" %}
{% /image %}

A **session** represents one end-to-end use of the ID verification service. Each time the ID verification service is initiated (regardless of which specific tasks/checks are required) a unique session identifier is assigned from Yoti's backend.

Every time a user elects to supply an ID document on the relying business app or website, you will need to create a session with Yoti to perform the ID checks.

Once the Yoti Client SDK has launched it will take the end user through the ID document capture flow, followed by a liveness check (if requested when creating the session). Once this flow is completed the end user is redirected back to the relying business client so that they may continue their journey. These redirects are defined when generating the session.

The session can be retrieved by the Yoti SDK using the session ID. The response from this endpoint contains all information, check and task completion statuses and resource and media data, along with the associated media identifiers.

The response will be in the form of either an object for data or a buffer string for images.

---

## The User flow

The user will be asked to prove their identity and is taken through the Yoti verification steps where they will have the option to upload or take a photo of their ID. You will then need to redirect them to a success or error URL, alternatively you can listen to post messaging from the iframe.

{% image url="https://image-archive.developerhub.io/image/upload/72631/yfc2udzwk6nyjvjvq592/1608066673.png" caption="Yoti Doc Scan user flow" mode="responsive" height="734" width="1646" %}
{% /image %}

It is up to you how you initiate the service, whether that's via a button or directly.

{% image url="https://image-archive.developerhub.io/image/upload/20556/tx9t9br3tjj5jw8thibm/1575454762.jpg" caption="Yoti Doc Scan user flow" mode="responsive" height="424" width="1288" %}
{% /image %}

1. The user is asked to select the country and type of ID document they are submitting to Yoti Doc Scan.
2. The image of the ID document is captured using the user’s device.
3. The user is asked to confirm that the image captured is clear.
4. The user performs a liveness test to prove they are a real person. This is the FaceTec ZoOm product where a user is asked to position their face in front of their phone camera, so it fits within the oval on the screen, and then move their face toward the screen following the instructions presented to them. FaceTec’s system is certified to Level 2 by a NIST certified testing company for liveness and is also very effective at detecting mask attacks.

Passing a ‘liveness test’ in this way gives us a high confidence that the user attempting to create a Yoti account is a real person (not an automated ‘bot’) and that we have captured an image of their actual facial appearance on that date (rather than them having supplied a pre-existing photograph of themselves or a third party).

---

## Supported Browsers

{% image url="https://image-archive.developerhub.io/image/upload/29751/zvnjmdfwoalnpibennp4/1596558309.jpg" caption="Supported browsers" mode="600" height="1168" width="1200" %}
{% /image %}

---

## Translations supported

Yoti Doc scan has configuration settings to change the language of the information displayed to the end user. 

Supported languages are:

- French (Français) 🇫🇷
- Spanish (Español) 🇪🇸
- Thai (ภาษาไทย) 🇹🇭
- Russian (русский) 🇷🇺
- Brazilian Portuguese (português brasileiro) 🇧🇷
- Turkish (Türkçe) 🇹🇷
- Vietnamese (Tiếng Việt) 🇻🇳
- Czech (čeština) 🇨🇿
- German (Deutsch) 🇩🇪
- Canadian English 🇨🇦

For information on how to integrate this please go [here](https://developers.yoti.com/yoti-doc-scan/preferences)[.](https://developers.yoti.com/yoti-doc-scan/generating-a-session#preferences) You will need to understand how to [create a session](https://developers.yoti.com/yoti-doc-scan/integration-guide) first.

---

## Using Yoti responsibly

We pride ourselves on how we handle our users' data. We use tech for good and enable users to securely prove their identity, always being transparent about what happens to their details. We ask that you follow these principles.

{% image url="https://image-archive.developerhub.io/image/upload/72631/b05jrh7mspbwl2dym4so/1608066716.png" caption="Use Yoti responsibly" mode="300" height="570" width="580" %}
{% /image %}

- Be transparent about why you're collecting this data and only use the data for those reasons.
- Only collect the information you actually need. Data minimisation is one of the main benefits of Yoti, allowing people only to share what’s really necessary for a particular purpose.
- Make sure the data you collect is stored securely. Data security is at the heart of what we do and we think it should be important to every organisation.