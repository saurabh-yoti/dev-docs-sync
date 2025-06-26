---
type: page
title: Integration guide
listed: true
slug: integration-guide-sign
description: 
index_title: Integration guide
hidden: 
keywords: 
tags: 
---

This document will guide you through the configuration and implementation steps that are necessary in order for your backend to be able to retrieve and send documents for users to electronically sign.

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

{% html %}
<div class="alert-API">

    <div class="alert-title" id="API">

    <i _ngcontent-cvo-c21="" class="fas fa-external-link-alt" style="margin-left: -35px; margin-right: 15px"></i>  

      API Link

    </div>

    <div class="alert-text">

     Jump straight to our API references with code snippets if you prefer.

    </div>

    <div class="alert-links"> 

        <a href="https://www.yoti.com/api-reference/#yoti-sign">Yoti Sign API</a>

    </div>

</div>
{% /html %}

The integration steps are as follows:

1. [Authentication](https://developers.yoti.com/yoti/authentication)
2. [Create envelope request](https://developers.yoti.com/yoti/create-an-envelope-request)
3. [Get / Archive documents](https://developers.yoti.com/yoti/recipients)

---

## The integration explained

The roles of the Sender, Yoti and Recipient is described below:

- **Sender:** These are your organisation's users, who want to send out documents to be signed. They will upload their documents, and specify who should sign them.
- **Yoti:** Yoti stores the documents on our servers during the signing process, and sends signing requests by email.
- **Recipient**: Recipient will receive signing requests by email. The email will have a link to a document where they can sign.

The diagram below describes the Yoti Sign process and how a backend can be integrated with the Yoti architecture.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1590497419/29754/xmpbfuxkvkcum5bcawxr.jpg" caption="Yoti Sign explained" mode="600" height="4080" width="2479" %}
{% /image %}

---

## General concepts

The API consists of the following:

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1588682332/20563/nxmb2wo35h8xkxm7u4dy.png" caption="YotiSign structure" mode="responsive" height="1076" width="1600" %}
{% /image %}

{% table %}
| Object | Description | 
| ---- | ---- | 
| [Authentication](https://developers.yoti.com/yoti/authentication) | A bearer token required to create an envelope. | 
| [Envelope](https://developers.yoti.com/yoti/create-an-envelope-request#what-is-an-envelope) | The fundamental object the components are held in. This will contain the document ID, recipient ID, auth configuration and status. | 
| [Recipient](https://developers.yoti.com/yoti/create-an-envelope-request#recipient-object) | The person that will receive the email and document to sign, with a level of authorisation set and signature placement (tags) | 
| [Documents](https://developers.yoti.com/yoti/create-an-envelope-request#file-object) | The documents that the recipients will receive. | 
{% /table %}

---

### Extra features

Yoti Sign has extra features to enhance your users' experience. 

**[1) Document tagging](https://developers.yoti.com/yoti/create-an-envelope-request#recipient-object)**

A tag is an array of objects used to place signature fields on a given document. 

**[2) Sign order grouping](https://developers.yoti.com/yoti/create-an-envelope-request#recipient-object)**

This defines an order in which recipients receive invitations to sign a document. 

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1589460216/20563/w0e4odsf85vciqb2huc0.jpg" caption="Signing order" mode="responsive" height="266" width="738" %}
{% /image %}

For example, all recipients within sign group 1 will be the first to receive a document to sign. Once all recipients from sign group 1 have signed, the document will be sent to sign group 2. If no sign group is specified, a default of 1 will be assumed.