---
type: page
title: Integration guide
listed: true
slug: integration-guide
description: 
index_title: Integration guide
hidden: 
keywords: 
tags: 
---

This document will guide you through the configuration and implementation steps that are necessary in order for your backend to be able to retrieve and send documents for users to electronically sign.

The integration steps are as follows:

1. [Authentication](https://developers.yoti.com/yoti-sign/integration-guide#authentication-token)
2. [Create envelope request](https://developers.yoti.com/yoti-sign/create-an-envelope-request)
3. [Get / Archive documents](https://developers.yoti.com/yoti-sign/get-documents)

The URLs for Yoti Sign endpoints are listed below:

{% table %}
| Environment | URL | 
| ---- | ---- | 
| Sandbox | [https://demo.api.yotisign.com](https://demo.api.yotisign.com/) | 
| Production | [https://api.yotisign.com](https://api.yotisign.com/) | 
{% /table %}

---

## Authentication token

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

Yoti Sign uses an HTTP authentication scheme called ‘bearer authentication’. This involves security tokens called ‘bearer tokens’. They are the predominant type of access token used with [OAuth 2.0](https://oauth.net/2/). A resource should interpret a bearer token as "Give the bearer of this token access". The client must send this token in the Authorization header when making requests to protected resources.

It is important that your API Key remains strictly confidential. It must be stored securely. We advise that you never commit any code containing your API Key, and never share it beyond the authorised party.

If you believe your API key has been compromised, please contact us as soon as possible. This can be done through your account manager or via our support desk by emailing [sdksupport@yoti.com](mailto:sdksupport@yoti.com).