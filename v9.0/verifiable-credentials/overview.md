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

Yoti allows you to issue your own 'attribute' to a Yoti user. This document will walk you through our API giving the ability to choose who is able to both issue and request these credentials in the credential definition stage. At Yoti we call this a verifiable credential.

{% video %}
{% /video %}

A verifiable credential​ is handled in the same way as all [auto$](/digital-id-legacy/yoti-attributes) but follows the same concept as the [W3C standard](https://www.w3.org/TR/vc-data-model/#what-is-a-verifiable-credential). The definition of an attribute is an assertion made about a user. It can be identity information, something that the user owns and can prove they are in control of.

{% image url="https://image-archive.developerhub.io/image/upload/72661/k7rfslsm5vax0lgltljp/1604061494.png" caption="Credential creation with Yoti" mode="full" height="3692" width="3311" %}
{% /image %}

{% callout type="info" title="Good to know" %}
If you wish to use this functionality please let us know as this process currently requires us to do a Yoti app change internally.

[Contact us](https://support.yoti.com/yotisupport/s/contactsupport)
{% /callout %}

There are three main stages to create and use your credential:

1. Defining the credential.
2. Issuing the credential.
3. Requesting the credential.

{% callout type="warning" title="Before you start" %}
Please install our Yoti SDK and get familiar with Yoti QR integration.

[auto$](/digital-id/quick-start)
{% /callout %}