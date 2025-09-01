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

Welcome to the developer documentation for integrating our Age verification as a service solution.

This section will guide you through the implementation steps for our age verification service API on mobile or web, without the use of our age verification portal web UI. This API incorporates multiple Yoti products**,** leverages their individual SDKs and  is purpose built to provide only age related attributes. It is particularly suited for native app integrations.

If you are looking to use our fully hosted Age Verification UI, including for Web integrations, please refer to [Age verification portal](/age-verification/getting-started) instead.

The services that can be used under this API are:

{% table widths="" %}
| Service | Description | 
| ---- | ---- | 
| Age estimation | User has their age estimated based on facial analysis from a real-time selfie. | 
| ID verification | User uploads a scan of their ID document and a selfie (optional). | 
| Mobile number | Optional OTP and age verification via a mobile phone number. | 
| Database | A check against third party databases, such as credit ref agencies. | 
| Electronic ID | Age verification through EID schemes. | 
| Email address check | Age verification with a pre-existing verified email address. | 
{% /table %}

Three types of age checks are available:

- A standard **AGE** check that returns the age of a user.
- An **OVER** check that informs you if a user is over a defined age threshold, but protects the user’s details by not sharing their actual age is not shared.
- An **UNDER** check that informs you if a user is under a defined age threshold, but protects the user’s details by not sharing their actual age is not shared.

The overview below sets out the entities and data flows involved.

{% badge type="warning" text="Help" /%} If you need any help please contact us [here](https://yoti.force.com/yotisupport/s/contactsupport).

---

## Using Yoti responsibly

We pride ourselves on how we handle our users' data. We use tech for good and enable users to securely prove their identity or age, always being transparent about what happens to their details.

- Be transparent about why you're collecting data and only use this data for those reasons.
- Only collect the information you actually need. Data minimisation is one of the main benefits of Yoti, so people don't have to provide more information than is actually necessary.
- Make sure any information you export to your own systems is stored securely. Data security is at the heart of what we do and we think it should be important to every organisation.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1604402402/72645/m4wu2a4v4d117o6ma00k.png" mode="300" height="376" width="384" %}
{% /image %}