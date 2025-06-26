---
type: page
title: Overview
listed: false
slug: overview
description: 
index_title: Overview
hidden: 
keywords: 
tags: 
---

Yoti Doc Scan can be seamlessly integrated with your website, app or custom product so you can perform secure identity checks.  You'll be able to request specific ID documents from users directly from your website or app.

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      You will need to download the Yoti app on your phone and to register your business with Yoti.
   </div>
   <div class="alert-links"> 
      <a href="https://developers.yoti.com/yoti/getting-started-hub">Onboarding with Yoti</a>
      <a  target="_self" href="https://developers.yoti.com/yoti/generate-api-keys-hub"> Generate API keys </a>
   </div>
</div>
{% /html %}

You can integration Yoti Doc Scan in three ways:

1. Integration with our Yoti SDK's
2. Integrate with our API
3. Use the Portal (code free)

The overview below sets out the entities and data flows involved.

## Technical overview of the Doc Scan architecture

This section describes the SDK interactions for a web, mobile web and native mobile integration. Exchanges of data will occur securely between the relying party (your backend), Yoti and the client (the end user’s browser or mobile device).

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1592819888/29752/jegxh7iulszeq67wvtcn.jpg" caption="Yoti Doc Scan walkthrough" mode="responsive" height="3347" width="2626" %}
{% /image %}

A **session** represents one end-to-end use of the ID verification service. Each time the ID verification service is initiated (regardless of which specific tasks/checks are required) a unique session identifier is assigned from Yoti's backend.

Every time a user elects to supply an ID document on the relying business app or website, you will need to create a session with Yoti to perform the ID checks. 

Next you will define your session preferences to request from the user:

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1592237892/29752/ty4tupweambyfrzbkvmt.png" caption="Session Diagram" mode="responsive" height="1126" width="1865" %}
{% /image %}

Once the Yoti Client SDK has launched it will take the end user through the ID document capture flow, followed by a liveness check (if requested when creating the session). Once this flow is completed the end user is redirected back to the relying business client so that they may continue their journey. These redirects are defined when generating the session.

The session can be retrieved by the Yoti SDK using the session ID. The response from this endpoint contains all information, check and task completion statuses and resource and media data, along with the associated media identifiers.

The response will be in the form of either an object for data or a buffer string for images.

{% html %}
<div class="alert-know">
    <div class="alert-title" id="know">
        Knowledge base
    </div>
    <div class="alert-text">
        Whilst it is possible to retrieve a given session at any time, relying parties will be notified when a session update occurs, according to the notifications settings provided at session creation time.
    </div>
    <div class="alert-links"> 
       <a target="_self" href="https://developers.yoti.com/yoti-doc-scan/notifications">More on notifications</a> 
    </div>
</div>
{% /html %}

---

## The User flow

The user will be asked to prove their identity and is taken through the Yoti verification steps where they will have the option to upload or take a photo of their ID. You will then need to redirect them to a success or error URL, alternatively you can listen to post messaging from the iframe.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1578328573/20556/svmat5elvxufbtxd92bq.png" caption="Yoti Doc Scan user flow" mode="full" height="1120" width="2526" %}
{% /image %}

It is up to you how you initiate the service, whether that's via a button or directly.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1575454762/20556/tx9t9br3tjj5jw8thibm.jpg" caption="Yoti Doc Scan user flow" mode="responsive" height="424" width="1288" %}
{% /image %}

1. The  user is asked to select the country and type of ID document they are submitting to Yoti Doc Scan. 
2. The  image of the ID document is captured using the user’s device.
3. The user is asked to confirm that the image captured is clear.
4. The user performs a liveness test to prove they are a real person. This is the FaceTec ZoOm product where a user is asked to position  their face in front of their phone camera, so it fits within the oval on the screen, and then move their face toward the screen following the instructions presented to them. FaceTec’s system is certified to Level 2 by a NIST certified testing company for liveness and is also very effective at detecting mask attacks.

Passing a ‘liveness test’ in this way gives us a high confidence that the user attempting to create a Yoti account is a real person (not an automated ‘bot’) and that we have captured an image of their actual facial appearance on that date (rather than them having supplied a pre-existing photograph of themselves or a third party).

---

## Using Yoti responsibly

We pride ourselves on how we handle our users' data. We use tech for good and enable users to securely prove their identity, always being transparent about what happens to their details. We ask that you follow these principles.

- Be transparent about why you're collecting this data and only use the data for those reasons.
- Only collect the information you actually need. Data minimisation is one of the main benefits of Yoti, allowing people only to share what’s really necessary for a particular purpose.
- Make sure the data you collect is stored securely. Data security is at the heart of what we do and we think it should be important to every organisation.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1575455138/20556/vablirkjbpsgtvngakyl.jpg" caption="Use Yoti responsibly" mode="300" height="584" width="572" %}
{% /image %}