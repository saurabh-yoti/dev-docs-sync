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

Welcome to the developer documentation for integrating the Identity verification service.

You can integrate the Identity verification service in two ways:

{% badge type="custom" text="PORTAL" /%} No need to write any code.

{% badge type="custom" text="SDKS" /%} A wrapper around our backend API to simplify the integration process.

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      You will need to create a Yoti Hub account with an e-mail & password or using the Yoti App on your phone and register your business with Yoti. Click below for more info.
   </div>
   <div class="alert-links"> 
         <a target="_self" href="https://developers.yoti.com/identity-profiles/getting-started">View Onboarding with Yoti</a>
   </div>
</div>
{% /html %}

The overview below details the entities and data flows.

{% badge type="warning" text="Help" /%} If you need any help please contact us [here](https://yoti.force.com/yotisupport/s/contactsupport).

{% html %}
<div class="alert-know">
    <div class="alert-title" id="know">
        Not sure what to integrate?
    </div>
    <div class="alert-text">
This product is designed for Identity Verification, if you need an Age Verfication solution please check our our Age verification service. 
  
  </div>
    <div class="alert-links"> 
       <a href="https://developers.yoti.com/age-verification/overview">Age verification</a>
    </div>
</div>
{% /html %}

---

## Technical overview

This section describes the SDK interactions for a web, mobile web and native mobile integration. Data Exchanges will occur securely between the relying party (your backend), Yoti and the client (the end user’s browser or mobile device).

A **session** represents one end-to-end use of the ID verification service. Each time the ID verification service is initiated (regardless of which specific tasks/checks are required) a unique session identifier is assigned by Yoti's backend.

{% image url="https://uploads.developerhub.io/prod/kvAX/kxg47nuhbr0yt1wm1d9889qogljewb554kb6sycr3oovyeksz77vh6x13mj3uhx5.png" caption="Identity verification walkthrough" mode="responsive" height="1334" width="1032" %}
{% /image %}

Every time a user elects to supply an ID document on the relying business app or website, you will need to create a session with Yoti to perform the ID checks.

Once the Yoti Client SDK has launched, it will take the end user through the ID document capture flow, followed by a liveness check (if requested when creating the session). Once this flow is completed the end user is redirected back to the relying business client, so that they may continue their journey. These redirects are defined when generating the session.

The session can be retrieved by the Yoti SDK using the session ID. The response from this endpoint contains all information, check and task completion statuses and resource and media data, along with the associated media identifiers.

The response will be in the form of either an object for data or a buffer string for images.

---

## Feature list

The Identity verification service is very adaptable, please see below for features available for you to configure within your session.

{% table widths="0,0,242" %}
| Name | Description | Resources | Manual check available | 
| ---- | ---- | ---- | ---- | 
| Document authenticity | A request to assess the characteristics of a document, to determine the validity of the ID document. Yoti will perform multiple checks on a ID document. | Minimum 1x Document Resource | ✅ | 
| Text extraction | A request to obtain the data printed visually on a document, in structured form. | Minimum 1x Document Resource | ❌ | 
| Document comparison | If you request your users to upload more than one document we offer the ability to cross check the data | Minimum 2x Document Resource | ❌ | 
| Filters | Restriction of documents / countries. If you do not wish to accept all documents or countries you can configure your session to add / remove which countries and document types are displayed to the user on the user view. | N/A | N/A | 
| Liveness check | A requested check to assess whether the document scan is being performed by a real person, and not someone wearing a mask or an automated system. | Minimum 1x Liveness Resource | ❌ | 
| Face match check | A request to assess whether the user's face matches the face on the ID document. | Minimum 1x Doc Resource & 1x Liveness Resource | ✅ | 
{% /table %}

---

## The User flow

The user will be asked to prove their identity and is taken through the Yoti verification steps where they will have the option to upload or take a photo of their ID. You will then need to redirect them to a success or error URL, alternatively you can listen to post messaging from the iframe.

{% image url="https://uploads.developerhub.io/prod/kvAX/4ouftiur4dekck3vugvto63umrfrd1drx1h8d0o0ejlo3o0jgdu98sbdqm27jvq7.png" caption="Identity verification user flow" mode="responsive" height="734" width="1646" %}
{% /image %}

It is up to you how you initiate the service, whether that's via a button or directly.

{% image url="https://uploads.developerhub.io/prod/kvAX/j342b2t5g0lmb77tn8hewv18tyecqzc1j6bfb6ogdms176bcse9rnfqzcz1zked4.jpg" caption="Identity verification user flow" mode="responsive" height="424" width="1288" %}
{% /image %}

1. The user is asked to select the country and type of ID document they are submitting.
2. The image of the ID document is captured using the user’s device.
3. The user is asked to confirm that the image captured is clear.
4. The user performs a liveness test to prove they are a real person. This is the FaceTec ZoOm product where a user is asked to position their face in front of their phone camera, so it fits within the oval on the screen, and then move their face toward the screen following the instructions presented to them. FaceTec’s system is certified to Level 2 by a NIST certified testing company for liveness and is also very effective at detecting mask attacks.

Passing a ‘liveness test’ in this way gives us a high confidence that the user attempting to create a Yoti account is a real person (not an automated ‘bot’) and that we have captured an image of their actual facial appearance on that date (rather than them having supplied a pre-existing photograph of themselves or a third party).

{% html %}
<div style="padding:56.25% 0 0 0;position:relative;"><iframe src="https://player.vimeo.com/video/647392006?h=6c95831bb6&amp;badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=58479&dnt=1" frameborder="0" allow="autoplay; fullscreen; picture-in-picture" allowfullscreen style="position:absolute;top:0;left:0;width:100%;height:100%;" title="Seamless identity verification directly on your website or app"></iframe></div><script src="https://player.vimeo.com/api/player.js"></script>
{% /html %}

---

## Supported browsers

{% table %}
| Device (Web SDK) | Browser | Version | 
| ---- | ---- | ---- | 
| Android | Chrome | Last 3 versions | 
| iOS | Safari | Last 3 versions | 
| Desktop | Chrome | Last 4 versions | 
|  | Safari | Last 4 versions | 
|  | Edge | Last 2 versions | 
{% /table %}

---

Using Yoti responsibly

We pride ourselves on how we handle our users' data. We use tech for good and enable users to securely prove their identity, always being transparent about what happens to their details. We ask that you follow these principles.

{% image url="https://uploads.developerhub.io/prod/kvAX/n9mfwpaw2bwzn7b0103a9pvacvazv619i2f6c5vufterdq6j2vvrv083090mwwrg.png" caption="Use Yoti responsibly" mode="300" height="570" width="580" %}
{% /image %}

- Be transparent about why you're collecting this data and only use the data for those reasons.
- Only collect the information you actually need. Data minimisation is one of the main benefits of Yoti, allowing people only to share what’s really necessary for a particular purpose.
- Make sure the data you collect is stored securely. Data security is at the heart of what we do and we think it should be important to every organisation.