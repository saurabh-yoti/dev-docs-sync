---
type: page
title: US Partner
listed: true
slug: us-partner
description: 
index_title: US Partner
hidden: 
keywords: 
tags: 
---

Yoti Age Verification works with a network of partners, including a US owned and controlled company to perform age verification.

When using a Yoti Partner, the reason for age verification is not revealed to the the partner, ensuring the end user's behaviour is protected.

In order to use the US partner an organisation must be registered with Yoti.

For information on how to do this, please refer to our **[Onboarding guide.](https://developers.yoti.com/age-verification/getting-started)** 

Details you will need:

- A verified organisation through the Yoti Hub
- Age Verification API Key consisting of an SDK ID and Bearer Token

US Partner checks can be enabled alongside any existing Age verification methods

{% callout type="info" title="Info" %}
At least one of Document Scan, Facial Age Estimation or Digital ID Age verification methods must be enabled to use this check
{% /callout %}

Configuration:

{% code %}
{% tab language="json" title="" %}
{
  ... // Existing Age verification configuration
  "us_florida_hb3": {
    "allowed": true,
    "threshold": 18,
    "retry_limit": 1
  }
  ...
}
{% /tab %}
{% /code %}

For the complete create session payload, please refer to [auto$](/age-verification/create-a-session).

{% table widths="" %}
| Field | Values | Description | 
| ---- | ---- | ---- | 
| allowed | true / false | Configure whether to enable or disable this check. Default false. | 
| threshold | 18 / 21 | Configure the age verification threshold for this check. | 
| retry_limit | number | Configure the number of retries available to the user in the event of a failure. | 
{% /table %}