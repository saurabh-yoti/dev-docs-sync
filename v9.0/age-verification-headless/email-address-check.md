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

{% callout type="info" title="Info" %}
Email address check requires provisioning through Yoti. Please get in touch through [support.yoti.com](https://support.yoti.com/yotisupport/s/contactsupport) if interested in using this solution.
{% /callout %}

## Endpoint

The API endpoint to request the email address check for age:

{% code %}
{% tab language="http" %}
POST https://age.yoti.com/api/v2/non-interactive
{% /tab %}
{% /code %}

## Headers

The HTTP headers for the API request:

{% table widths="" %}
| Header | Description | 
| ---- | ---- | 
| Authorization | API Key to call the Yoti Age API. Should be sent as a 'Bearer {{API_TOKEN}}'. | 
| Content-Type | application/json | 
| Yoti-SDK-Id | Your unique Yoti-Sdk-Id (uuid) | 
{% /table %}

## Payload

{% callout type="info" title="Info" %}
You must verify that the email is in the control of the the target user, i.e. through OTP or registration.
{% /callout %}

The JSON structure for the API request (payload):

{% code %}
{% tab language="json" %}
{
    "type": "OVER",
    "threshold": 18,
    "evidence": {
        "email": {
            "address": "<email address>"
        },
        "country": "<country code>"
    }
}
{% /tab %}
{% /code %}

{% table widths="" %}
| Field | Value | Description | 
| ---- | ---- | ---- | 
| type | OVER | Must be configured to 'OVER' as this is the only supported type. | 
| threshold | 18 | Age threshold; must be configured to 18. | 
| evidence | email, country | Verified email address of the user, and two letter ISO country code. | 
{% /table %}

{% badge type="warning" text="Note:" /%} All the values are required. We will attempt to filter out bad emails.

## Example Response

The JSON structure for the API response:

{% code %}
{% tab language="json" %}
{
    "evidence_id": "<UUID>",
    "method": "EMAIL",
    "created_at": "<timestamp>",
    "attempts": 1,
    "status": "COMPLETE",
    "result": true,
    "age": 18,
    "type": "OVER"
}
{% /tab %}
{% /code %}

{% table widths="" %}
| Field | Description | 
| ---- | ---- | 
| evidence_id | Unique ID related to the request check being performed. | 
| method | The age verification method performed. | 
| created_at | A timestamp for when the age verification method was attempted. | 
| attempts | Attempt count for given method (for email age estimation through API, this is expected to be '1'). | 
| status | COMPLETE - The email address has been associated with an Over 18 individual.\n\n\nERROR - We could not provide an email age estimation result, because we didn't have enough info associated with that email address.\n\n\nFAIL - The email address has been associated with an Under 18 individual. | 
| result | Returns true if the threshold (18) has been met. Returns false if not met, or on error. | 
| age | The threshold of the check (18). | 
| type | Whether an OVER/UNDER or AGE type has been requested. Only OVER is supported for Email. | 
{% /table %}