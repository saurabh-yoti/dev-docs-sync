---
type: page
title: Email address check
listed: true
slug: email-address-check
description: 
index_title: Email address check
hidden: 
keywords: 
tags: 
---

If you already have a verified email address for a user, you can ask Yoti to check if it is likely to be associated with someone aged over 18.

Yoti checks the email source, if it is linked to an employer and for any financial transactions tied to it.

### Request

The JSON structure for the API request (payload):

{% code %}
{% tab language="json" %}
{
  "callback": {
    "url": "https://www.yoti.com",
    "auto": true
  },
  "ttl": 9000, 
  "type": "OVER",
  "age_estimation": { 
    "allowed": true,
    "threshold": 23,
    "level": "PASSIVE"
  },
  "email": {
    "data": {
        "verified_email": "melissa.peterson@yoti.com",
        "country_code": "gb"
    }
  },
  "resume_enabled": true
}
{% /tab %}
{% /code %}

{% table widths="" %}
| Field | Value | Description | 
| ---- | ---- | ---- | 
| verified_email | email | Verified email address of the user. | 
| country_code | country code | Two letter ISO country code. | 
{% /table %}

- All the values are required.
- We will attempt to filter out bad emails.

If the email check is enabled, we will automatically run it when an age verification session is created. If the check passes you will receive the status of "COMPLETE" in the API response, however if it fails we will return "INSUFFICENT_DATA". In which case integrators can launch the Yoti user interface to allow the user to try a different method.

{% callout type="warning" title="Warning" %}
resume_enabled must be set to "true" to allow a user to try a different method.
{% /callout %}

### Response

The JSON structure for the API response:

{% code %}
{% tab language="json" title="COMPLETE" %}
{
    "id": "cbe1df01-5868-4470-951e-5eb07ff76ab7",
    "status": "COMPLETE",
    "expires_at": "2025-08-09T23:27:58Z"
}
{% /tab %}
{% tab language="json" title="PENDING" %}
{
    "id": "cbe1df01-5868-4470-951e-5eb07ff76ab7",
    "status": "INSUFFICENT_DATA",
    "expires_at": "2025-08-09T23:27:58Z"
}
{% /tab %}
{% /code %}