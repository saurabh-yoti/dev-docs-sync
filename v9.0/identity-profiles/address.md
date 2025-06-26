---
type: page
title: Address
listed: true
slug: address
description: 
index_title: Address
hidden: 
keywords: 
tags: 
---

It is possible to extend the Identity verification integration by requesting an address verification as part of a session.

{% callout type="info" title="Good to know" %}
An address check is performed when requested through an 'Identity Plus Address' scheme via any target assurance level.
{% /callout %}

This check will facilitate an extra verification of a user by searching a person’s details against a collated database from various sources worldwide.

Yoti will need to capture the user's address so you will need to allow the following checks:

Note: not all ID documents contain the users address.

---

## The user flow

1. The user will be presented with a screen to select their issuing country and document type.
2. The user will be upload their selected document type.

3. If the submitted document contains an address, the user may proceed.
4. If the submitted document does not contain an address, the user will be requested to key in their address, this will be verified through a CRA (soft search) check.
5. The user optionally finishes the journey with a Liveness check, before being redirected to your website.