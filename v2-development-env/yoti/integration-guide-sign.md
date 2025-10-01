---
type: page
title: Integration guide Dev
listed: true
slug: integration-guide-sign
description: 
index_title: Integration guide Dev
hidden: 
keywords: 
tags: 
---

Yoti Sign offers the convenience and simplicity of e-signing platforms, but with the optional added security of biometric verification providing immutable proof of the signee's identity.

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      You will need to complete the Yoti Sign onboarding process which is a short form. 
   </div>
   <div class="alert-links"> 
         <a href="https://www.yotisign.com/app/free-trial/">Onboard here</a>
   </div>
</div>
{% /html %}

## Technical Overview

This document will guide you through the configuration and implementation steps that are necessary in order for your backend to be able to retrieve and send PDFs for users to electronically sign.

There are two types of users in the Yoti Sign flow:

- **The Sender** - This user will be sending out the PDF and requesting a signed document back.
- **The Signee** - This user will be receiving the PDF and sending the digitally signed document to the sender.

{% image url="https://image-archive.developerhub.io/image/upload/20563/h97ql7n0ovqcqzpucm7n/1572532255.jpg" caption="Yoti Sign API walkthrough" mode="600" height="4080" width="2479" %}
{% /image %}

---

## API Endpoints

The endpoints you need are below.

{% table %}
| Environment | URL | 
| ---- | ---- | 
| Sandbox | [https://demo.api.yotisign.com](https://demo.api.yotisign.com) | 
| Production | [https://api.yotisign.com](https://api.yotisign.com) | 
{% /table %}

## Security

It is important to note that your API Key is strictly confidential to you and should be stored securely. It is never advisable to commit any code containing your API Key and it should never be shared beyond the authorised party.

If you believe your Key has been compromised, please contact us as soon as possible. This can be done through your account manager or via our support support by emailing [sdksupport@yoti.com](mailto:sdksupport@yoti.com).