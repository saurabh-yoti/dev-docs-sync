---
type: page
title: Integration guide
listed: true
slug: integration-guide-docscan
description: 
index_title: Integration guide
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
      <a  target="_self" href="https://developers.yoti.com/yoti/generate-api-keys"> Generate API keys </a>
   </div>
</div>
{% /html %}

The integrations steps are as follows, see below or jump straight to the documentation:

1) [Install the SDK](https://developers.yoti.com/yoti/generating-a-session#installing-our-sdk)

2) [Create the session & launch](https://developers.yoti.com/yoti/generating-a-session#creating-the-session)

3) [Retrieve the results](https://developers.yoti.com/yoti/results)

---

## Technical overview

This section describes the SDK interactions for a web, mobile web and native mobile integration. Exchanges of data will occur securely between the relying party backend, Yoti and the client.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1592819888/29752/jegxh7iulszeq67wvtcn.jpg" caption="Yoti Doc Scan walkthrough" mode="responsive" height="3347" width="2626" %}
{% /image %}

A **session** represents one end-to-end use of the ID verification service. Each time the ID verification service is initiated (regardless of which specific tasks/checks are required) a unique session identifier is assigned.

Every time a user elects to supply an ID document on the relying business app or website, you will need to create a session with Yoti to perform the ID checks. 

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Jump to this section.. 
    </div>
    <div class="alert-text">
        To start this please head over to the creating a session section
    </div>
    <div class="alert-links"> 
        <a href="https://developers.yoti.com/yoti/generating-a-session">Create a session</a>
   </div>
</div>
{% /html %}

Next you will define your session preferences to request from the user:

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1592237892/29752/ty4tupweambyfrzbkvmt.png" caption="Session Diagram" mode="responsive" height="1126" width="1865" %}
{% /image %}

Once the Yoti Client SDK has launched it will take the end user through the ID document capture flow, followed by a liveness check (if requested when creating the session). Once this flow is completed the end user is redirected back to the relying business client so that they may continue their journey. These redirects are defined when generating the session.

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Jump to this section
    </div>
    <div class="alert-text">
        To start this please head over to the Launch the user view section
    </div>
    <div class="alert-links"> 
        <a href="https://developers.yoti.com/yoti/render-the-user-view">Launch the user view</a>
   </div>
</div>
{% /html %}

The session can be retrieved by the Yoti SDK using the session ID. The response from this endpoint will detail all information, check and task completion status, resource and media data, along with the associated media identifiers.

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Jump to this section
    </div>
    <div class="alert-text">
        To start this please head over to the Retrieve results section.
    </div>
    <div class="alert-links"> 
        <a href="https://developers.yoti.com/yoti/results">Retrieve results </a>
   </div>
</div>
{% /html %}

This will respond with the media as either an object for data or a buffer string for images.

{% html %}
<div class="alert-know">
    <div class="alert-title" id="know">
        Knowledge base
    </div>
    <div class="alert-text">
        Whilst it is possible to retrieve a given session at any time, relying parties will be notified when a session update occurs, according to the notifications settings provided at session creation time.
    </div>
    <div class="alert-links"> 
       <a target="_self" href="https://developers.yoti.com/yoti/generating-a-session#notifications">More on notifications</a> 
    </div>
</div>
{% /html %}

---

## Extra features

Yoti Doc scan has extra features to enhance your users' experience.

1)[ Multiple documents: -](https://developers.yoti.com/yoti/generating-a-session#request-multiple-documents) Collect multiple documents from your users. 

2) [Remove countries / documents on the iframe](https://developers.yoti.com/yoti/generating-a-session#filtering-documents-and-countries): - This will prevent users from uploading documents from countries / documents you don't support.

3) NFC capabilities on our mobile integrations. Allowing users to simply tap their passport to complete verification.

4)[ Documents supported](https://developers.yoti.com/yoti/generating-a-session#supported-documents)- Allowing you to hit an endpoint to see what documents we support per country.

5) [Translation](https://developers.yoti.com/yoti/generating-a-session#preferences) on our web client.

**Coming soon:**

- Ability to add non ID documents.

---

## The User flow

The user will be asked to prove their identity and are taken through the Yoti verification steps where they will have the option to upload or take a photo of their ID. You will then need to redirect them to a success or error URL, alternatively you can listen to post messaging from the iframe.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1578328573/20556/svmat5elvxufbtxd92bq.png" caption="Yoti Doc Scan flow" mode="full" height="1120" width="2526" %}
{% /image %}

It is up to you how you initiate the service, whether that's via a button or directly.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1575454762/20556/tx9t9br3tjj5jw8thibm.jpg" caption="Yoti Doc Scan user flow" mode="responsive" height="424" width="1288" %}
{% /image %}

1. The user is asked to select the country and type of ID document they are submitting to Yoti Doc Scan. 
2. The image of the ID document is captured using the user’s device.
3. The user is asked to confirm that the image captured is clear.
4. The user performs a liveness test to prove they are a real person. This is the FaceTec ZoOm product where a user is asked to place their face in the oval on the screen, and then move their face toward the screen following the instructions presented to them. FaceTec’s system is certified to Level 2 by a NIST certified testing company for liveness and is also very effective at detecting mask attacks.

Passing a ‘liveness test’ in this way gives us a high confidence that the user attempting to create a Yoti account is a real person (not an automated ‘bot’) and that we have captured an image of their actual facial appearance on that date (rather than them having supplied a pre-existing photograph of themselves or a third party).

---

## Using Yoti responsibly

We pride ourselves on how we handle our users' data. We use tech for good and enable users to securely prove their identity, always being transparent about what happens to their details. We hope you believe in this too.

- Be transparent about why you're collecting data and only use this data for those reasons.
- Only collect the information you actually need. Data minimisation is one of the main benefits of Yoti, giving people ownership of their data.
- Make sure the data you collect is stored securely. Data security is at the heart of what we do and we think it should be important to every organisation.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1575455138/20556/vablirkjbpsgtvngakyl.jpg" caption="Use Yoti responsibly" mode="300" height="584" width="572" %}
{% /image %}