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

Welcome to the developer documentation for integrating the eSignatures service. The eSignatures service offers the convenience and simplicity of e-signing platforms, but with the added security of biometric verification and cryptographic signatures.

You can integrate with our eSignatures service in **two** ways:

{% badge type="custom" text="PORTAL" /%} No need to write any code

{% badge type="custom" text="API" /%} Yoti gives you the option to use our API directly.

{% badge type="warning" text="Help" /%} If you need any help please email [clientsupport@yoti.com](mailto:clientsupport@yoti.com).

{% html %}
<div class="alert-know">
    <div class="alert-title" id="know">
        Knowledge base
    </div>
    <div class="alert-text">
Have a look at our FAQs for more information.    </div>
    <div class="alert-links"> 
       <a href="https://support.yoti.com/hc/en-us/sections/360000855254-Yoti-Sign">Yoti Sign FAQs</a>

    </div>
</div>
{% /html %}

---

## Technical overview

Yoti Sign has 3 personas:-  Sender, Yoti and Recipient is described below.

- **Sender:** These are your organisation's users, who want to send out documents to be signed. They will upload their documents, and specify who should sign them.
- **Yoti:** Yoti stores the documents on our servers during the signing process, and sends signing requests by email.
- **Recipient**: Recipient will receive signing requests by email. The email will have a link to a document where they can sign.

The diagram below describes the process and how a backend can be integrated with the Yoti architecture.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1590497419/29754/xmpbfuxkvkcum5bcawxr.jpg" caption="eSignatures explained" mode="600" height="4080" width="2479" %}
{% /image %}

---

## Feature list

{% table widths="343" %}
| Feature | Description | 
| ---- | ---- | 
| Send document | Upload and send a document to be signed. | 
| Tags | A tag is an array of objects used to place signature fields on a given document. | 
| Auto-tagging | Dynamically tag a document by including special anchor tags inside the document itself. | 
| Signing order | Mandate that a certain signee signs before/after the rest.\n\n\n\nFor example, all recipients within sign group 1 will be the first to receive a document to sign.\n\n\n\nOnce all recipients from sign group 1 have signed, the document will be sent to sign group 2. If no sign group is specified, a default of 1 will be assumed. | 
| Yoti auth | A unique feature for our eSignatures platform is the ability to add a Yoti verification on top the signature. | 
| Reminders | Send a reminder to your signers. | 
| One time password | Enhance security when sending across your document you can enable OTP (one time password). | 
| Witness | You can add a witness to each document in the envelope. | 
| Templates | Templates are ideal for frequently sent documents. | 
| Sandbox | Only available in the API | 
{% /table %}

---

## General concepts

Yoti Sign consists of the following concepts:

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1588682332/20563/nxmb2wo35h8xkxm7u4dy.png" caption="eSignatures structure" mode="600" height="1076" width="1600" %}
{% /image %}

{% table widths="136" %}
| Object | Description | 
| ---- | ---- | 
| Envelope | The fundamental object the components are held in. This will contain the document ID, recipient ID, auth configuration and status. | 
| Recipient | The person that will receive the email and document to sign, with a level of authorisation set and signature placement (tags) | 
| Documents | The documents that the recipients will receive. | 
{% /table %}

{% badge type="info" text="Hint" /%} If using our API, Yoti requires you to use a bearer token required to create an envelope. 

---

## Using Yoti responsibly

We pride ourselves on how we handle our users' data. We use tech for good and enable users to securely prove their identity or age, always being transparent about what happens to their details.

- Be transparent about why you're collecting data and only use this data for those reasons.
- Only collect the information you actually need. Data minimisation is one of the main benefits of Yoti, so people don't have to provide more information than is actually necessary.
- Make sure any information you export to your own systems is stored securely.  Data security is at the heart of what we do and we think it should be important to every organisation.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1604402472/72634/v6aoulx2jig4gnxmio0r.png" mode="300" height="376" width="384" %}
{% /image %}