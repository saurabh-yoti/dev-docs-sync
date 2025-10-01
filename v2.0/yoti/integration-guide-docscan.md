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
      <a href="https://developers.yoti.com/yoti/getting-started-hub">View Onboarding with Yoti</a>
      <a target="_self" href="https://developers.yoti.com/yoti/generating-the-api-keys">View Generate API keys</a> 
   </div>
</div>
{% /html %}

## Technical overview

This section describes the API interactions for a web, mobile web and native mobile integration. Exchanges of data will occur securely between the relying party backend, Yoti API and the client.

{% image url="https://image-archive.developerhub.io/image/upload/20556/irhbroquzgkiv15neklg/1572633198.jpg" caption="Yoti Doc Scan API walkthrough" mode="600" height="3525" width="2479" %}
{% /image %}

---

## How it works

A **session** represents one end-to-end use of the ID verification service. Each time the ID verification service is initiated (regardless of which specific tasks/checks are required) a unique session identifier is assigned.

Every time an end user elects to supply an ID document on the relying business app or website, you will need to create a session (end to end use of the ID Verification service) with Yoti to perform the ID checks.

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Jump to this section.. 
    </div>
    <div class="alert-text">
        To start this please head over to the creating a request section
    </div>
    <div class="alert-links"> 
        <a href="https://developers.yoti.com/yoti/generating-a-session">Create a session</a>
   </div>
</div>
{% /html %}

Here you will define:

- [Preferences](https://developers.yoti.com/yoti/generating-a-session) - customisation of the session
- [Checks ](https://developers.yoti.com/yoti/generating-a-session#2-checks-configuration)- Which verification steps are required for the user
- [Tasks ](https://developers.yoti.com/yoti/generating-a-session#3-tasks-configuration)- What tasks should be performed

{% table %}
| Check / Task | Description | 
| ---- | ---- | 
| Check | Document Authenticity |  | 
| Check | Liveness | 
| Check | Face Match | 
| Task | Document Text Data Extraction | 
{% /table %}

### 2. Launch the Yoti Client SDK

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

### 3. Retrieve results and data

The session can be retrieved by sending a request to the Yoti API, using the session ID. The response from this endpoint will detail all information, check and task completion status, resource and media data, along with the associated media identifiers.

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Jump to this section
    </div>
    <div class="alert-text">
        To start this please head over to the Retrieve results and data section
    </div>
    <div class="alert-links"> 
        <a href="https://developers.yoti.com/yoti/session-and-media-retrieval">Results and data</a>
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
       <a target="_self" href="https://developers.yoti.com/yoti/knowledge-base-docscan#notifications">More on notifications</a> 
    </div>
</div>
{% /html %}

---

## Quick Start

## The User flow

Yoti Doc Scan is an embedded identity verification solution powered by Yoti. The process is quick, simple and secure; your customers will be able to prove who they are without leaving your flow or system.

{% image url="https://image-archive.developerhub.io/image/upload/20556/svmat5elvxufbtxd92bq/1578328573.png" caption="Yoti Doc Scan flow" mode="full" height="1120" width="2526" %}
{% /image %}

The user will be asked to prove their identity and are taken through the Yoti verification steps where they will have the option to upload or take a photo of their ID. You will then need to redirect them to a success or error URL, alternatively you can listen to post messaging from the iframe.

It is up to you how you initiate the service, whether that's via a button or directly.

{% image url="https://image-archive.developerhub.io/image/upload/20556/tx9t9br3tjj5jw8thibm/1575454762.jpg" caption="Yoti Doc Scan user flow" mode="responsive" height="424" width="1288" %}
{% /image %}

1. The user is asked to select the country and type of ID document they are submitting to Yoti Doc Scan. Yoti can accept ID documents from 206 countries and states.
2. The image of the ID document is captured using the user’s device. If the user has selected an ID document with identity information on the back, then the user is asked to submit the back of their ID document as well.
3. The user is asked to confirm that the image captured is clear.
4. The user must perform a liveness test to prove they are a real person. This is the FaceTec ZoOm product where a user is asked to place their face in the oval on the screen, and then move their face toward the screen following the instructions presented to them. FaceTec’s system is certified to Level 2 by a NIST certified testing company for liveness and is also very effective at detecting mask attacks.

Passing a ‘liveness test’ in this way gives us a high confidence that the user attempting to create a Yoti account is a real person (not an automated ‘bot’) and that we have captured an image of their actual facial appearance on that date (rather than them having supplied a pre-existing photograph of themselves or a third party).

---

## Using Yoti responsibly

We pride ourselves on how we handle our users' data. We use tech for good and enable users to securely prove their identity, always being transparent about what happens to their details. We hope you believe in this too.

- Be transparent about why you're collecting data and only use this data for those reasons.
- Only collect the information you actually need. Data minimisation is one of the main benefits of Yoti, giving people ownership of their data.
- Make sure the data you collect is stored securely. Data security is at the heart of what we do and we think it should be important to every organisation.

{% image url="https://image-archive.developerhub.io/image/upload/20556/vablirkjbpsgtvngakyl/1575455138.jpg" caption="Use Yoti responsibly" mode="300" height="584" width="572" %}
{% /image %}