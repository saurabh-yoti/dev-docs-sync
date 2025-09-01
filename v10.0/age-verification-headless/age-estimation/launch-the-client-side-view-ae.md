---
type: page
title: Launch the client side view
listed: true
slug: launch-the-client-side-view-ae
description: 
index_title: Launch the client side view
hidden: 
keywords: 
tags: 
---

## Overview

We have developed a Face capture module (FCM) to aid in capturing images that closely meet the age estimation and anti-spoofing API requirements.

The Face capture module provides a simplified way to capture a face and provides an image output. However, it does not handle transactions with the age estimation API; these calls should be made separately and are documented in the next section.

---

## Web SDK

Our web component for the face capture module is available as a React and Vanilla JS library.

[NPM Package](https://www.npmjs.com/package/@getyoti/react-face-capture)

The module captures the facial image automatically and provides the output in following format:

{% code %}
{% tab language="json" %}
{
  "img": "<base64_img>",
  "secure": {
    "version": "<fcm_version>",
    "token": "<session_token>",
    "signature": "<result_signature>",
    "verification": "<verification_data>"
  }
}
{% /tab %}
{% /code %}

It's essential to save both `img` and `secure` fields without modification for the next step.