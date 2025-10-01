---
type: page
title: Double Anonymity
listed: true
slug: double-anonymity
description: 
index_title: Double Anonymity
hidden: 
keywords: 
tags: 
---

## Overview

{% callout type="warning" title="Before you start" %}
This guide assumes you are familiar with the Age Verification Service, if you are looking to review the AVS implementation first, please see [the section here.](/age-verification/create-a-session)
{% /callout %}

Yoti can provide a **Double Anonymity Check**. This check builds on the existing age verification implementation by applying a secondary anonymisation step.

In addition to the core age verification, the configuration includes:

- **Digital ID:** This flag (`digital_id`) requires a one-time onboarding process. Once created, users are verified for life and can use their digital ID to prove their age with businesses online without revealing the original reason for verification source of the verification information. Enable Facial Age Estimation within Digital ID allows the user two options to verify within the App, Age estimation or through an ID Document
- **Yoti Key Flag:** This flag (`yoti_key`) supports the re-verification of users by allowing the use of a pass key combined with two-factor authentication (2FA). A `rule_id` __must be configured to enable this method. Details around the Yoti Key and configuring a `rule_id` can be found in [auto$](/age-verification/age-tokens)
- **Double Blind:** This flag (`double_blind`) updates how the methods are presented to the end user, and it is recommended this is enabled when configuring any double blind methods

Below is an example of how to enable these features in your configuration:

{% badge type="info" text="Note" /%} The user will only be asked to create a Yoti key if the callback url is not configured to automatically redirect. Please ensure your callback options is set to `false`.

{% code %}
{% tab language="json" %}
{
  // ...
  "digital_id": {
    "threshold": 18,
    "allowed": true,
    "age_estimation_allowed": true,
    "age_estimation_threshold": 21
  },
  "yoti_key": {
    "allowed": true,
    "authentication": true // true for Yoti key, false for Age token
  },
  "double_blind": true,
  "callback": {
    "auto": false, // Required for offering a Pass Key at the end of the AV flow
    "url": "https://www.yoti.com"
  }
  // ..
}
{% /tab %}
{% /code %}

### Complete example

{% code %}
{% tab language="json" %}
{
  "type": "OVER",
  "age_estimation": {
    "allowed": true,
    "threshold": 21, // Desired buffer for Age Estimation
    "level": "PASSIVE",
    "retry_limit": 1
  },
  "digital_id": {
    "threshold": 18,
    "allowed": true,
    "age_estimation_allowed": true,
    "age_estimation_threshold": 21
  },
  "doc_scan": {
    "allowed": true,
    "threshold": 18,
    "authenticity": "AUTO",
    "level": "PASSIVE",
    "retry_limit": 1
  },
  "yoti_key": {
    "allowed": true,
    "authentication": true // true for Yoti key, false for Age token
  },
  "rule_id": "your_rule_id",
  "double_blind": true,
  "ttl": 900,
  "callback": {
    "auto": false, // Required for offering a Pass Key at the end of the AV flow
    "url": "https://www.yoti.com"
  },
  "notification_url": "https://yourdomain.example/webhook",
  "cancel_url": "https://www.yoti.com",
  "retry_enabled": true,
  "synchronous_checks": true
}
{% /tab %}
{% /code %}

{% callout type="info" title="Info" %}
For results handling, see the [results](/age-verification/results) section.
{% /callout %}