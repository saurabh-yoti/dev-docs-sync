---
type: page
title: Create your own credential
listed: true
slug: verifiable-credential
description: 
index_title: Create your own credential
hidden: 
keywords: 
tags: 
---

Yoti allows you to issue your own 'attribute' to a Yoti user. This document will walk you through our API giving the ability to choose who is able to both issue and request these credentials in the credential definition stage. At Yoti we call this a verifiable credential.

{% video %}
{% /video %}

A verifiable credential​ is handled in the same way as all [auto$](/digital-id-legacy/yoti-attributes) but follows the same concept as the [W3C standard](https://www.w3.org/TR/vc-data-model/#what-is-a-verifiable-credential). The definition of an attribute is an assertion made about a user. It can be identity information, something that the user owns and can prove they are in control of.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1604061494/72661/k7rfslsm5vax0lgltljp.png" caption="Credential creation with Yoti" mode="full" height="3692" width="3311" %}
{% /image %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
        If you wish to use this functionality please let us know as this process currently requires us to do a Yoti app change internally.
    </div>
    <div class="alert-links"> 
        <a href="https://support.yoti.com/yotisupport/s/contactsupport">Contact us</a>
   </div>
</div>
{% /html %}

There are three main stages to create and use your credential:

1. Defining the credential.
2. Issuing the credential.
3. Requesting the credential.

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      Please install our Yoti SDK and get familiar with our dynamic QR code.
   </div>
   <div class="alert-links"> 
      <a href="https://developers.yoti.com/digital-id/install-the-sdk">Install the SDK</a>
           <a href="https://developers.yoti.com/digital-id/createbutton#dynamic-qr">Dynamic QR code</a>
   </div>
</div>
{% /html %}