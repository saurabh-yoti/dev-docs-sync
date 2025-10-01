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

Welcome to the developer documentation for integrating the Yoti Sign. Yoti Sign offers the convenience and simplicity of e-signing platforms, but with the added security of biometric verification and cryptographic signatures.

You can integration Yoti Sign in **two** ways:

- Integration with our API.
- Use our [portal ](https://www.yotisign.com/app/account/login)(code free).

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      Request your API keys, please let us know if you want to use sandbox or production. 
   </div>
   <div class="alert-links"> 
         <a href="https://www.yotisign.com/app/contact-us/">Get API keys</a>
   </div>
</div>
{% /html %}

## Technical overview of Yoti Sign architecture

The roles of the Sender, Yoti and Recipient is described below:

- **Sender:** These are your organisation's users, who want to send out documents to be signed. They will upload their documents, and specify who should sign them.
- **Yoti:** Yoti stores the documents on our servers during the signing process, and sends signing requests by email.
- **Recipient**: Recipient will receive signing requests by email. The email will have a link to a document where they can sign.

The diagram below describes the Yoti Sign process and how a backend can be integrated with the Yoti architecture.

{% image url="https://image-archive.developerhub.io/image/upload/29754/xmpbfuxkvkcum5bcawxr/1590497419.jpg" caption="Yoti Sign explained" mode="600" height="4080" width="2479" %}
{% /image %}

---

## General concepts

The API consists of the following:

{% image url="https://image-archive.developerhub.io/image/upload/20563/nxmb2wo35h8xkxm7u4dy/1588682332.png" caption="YotiSign structure" mode="responsive" height="1076" width="1600" %}
{% /image %}

{% table %}
| Object | Description | 
| ---- | ---- | 
| [Authentication](https://developers.yoti.com/yoti-sign/authentication) | A bearer token required to create an envelope. | 
| [Envelope](https://developers.yoti.com/yoti-sign/create-an-envelope-request#what-is-an-envelope) | The fundamental object the components are held in. This will contain the document ID, recipient ID, auth configuration and status. | 
| [Recipient](https://developers.yoti.com/yoti-sign/create-an-envelope-request#recipient-object) | The person that will receive the email and document to sign, with a level of authorisation set and signature placement (tags) | 
| [Documents](https://developers.yoti.com/yoti-sign/create-an-envelope-request#file-types) | The documents that the recipients will receive. | 
{% /table %}

---

### Extra features

Yoti Sign has extra features to enhance your users' experience. 

**1) [Document tagging](https://developers.yoti.com/yoti-sign/create-an-envelope-request#auto-tagging)**

A tag is an array of objects used to place signature fields on a given document. 

**2) [Sign order ](https://developers.yoti.com/yoti-sign/create-an-envelope-request#recipient-object)grouping**

This defines an order in which recipients receive invitations to sign a document. 

{% image url="https://image-archive.developerhub.io/image/upload/20563/w0e4odsf85vciqb2huc0/1589460216.jpg" caption="Signing order" mode="responsive" height="266" width="738" %}
{% /image %}

For example, all recipients within sign group 1 will be the first to receive a document to sign. Once all recipients from sign group 1 have signed, the document will be sent to sign group 2. If no sign group is specified, a default of 1 will be assumed.

---

## Using Yoti responsibly

We pride ourselves on how we handle our users' data. We use tech for good and enable users to securely prove their identity or age, always being transparent about what happens to their details.

- Be transparent about why you're collecting data and only use this data for those reasons.
- Only collect the information you actually need. Data minimisation is one of the main benefits of Yoti, so people don't have to provide more information than is actually necessary.
- Make sure any information you export to your own systems is stored securely.  Data security is at the heart of what we do and we think it should be important to every organisation.

{% image url="https://image-archive.developerhub.io/image/upload/72634/v6aoulx2jig4gnxmio0r/1604402472.png" mode="responsive" height="376" width="384" %}
{% /image %}