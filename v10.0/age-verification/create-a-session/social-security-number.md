---
type: page
title: Social security number
listed: true
slug: social-security-number
description: 
index_title: Social security number
hidden: 
keywords: 
tags: 
---

Yoti offers the additional method of using a social security number to verify a users age. This check is only available to individuals from the USA that have a social security number.

The Social security number method checks the basic identity details of a user can be matched to an known social security number in order to verify a user’s age. Yoti will send the user’s details, including their social security number to one of our data providers. Once the check is complete, the provider confirms the social security number can be linked to the validation identity which is then used to determine that the user is over the age threshold.

We never store or share the user’s details with anyone other than the provider.

{% badge type="error" text="Important" /%} Please contact Yoti before enabling this method.

{% code %}
{% tab language="json" %}
{
    "type": "OVER",
    "social_security_number": {
      "allowed" : true,
      "threshold": 18
    },
    "ttl": 900,
    "reference_id": "over_18_example",
    "callback": {
       "auto": true,
       "url": "https://www.yoti.com"
    },
    "notification_url": "https://yourdomain.example/webhook",
    "cancel_url": "https://www.yoti.com"
}
{% /tab %}
{% /code %}

{% table widths="94,94" %}
| Parameter | Types | Description | 
| ---- | ---- | ---- | 
| allowed | true / false | Enable the verification method to be available for the user to use. | 
| threshold | Integer | Age threshold for AV method. Only a threshold of 18+ is supported for SSN. | 
{% /table %}