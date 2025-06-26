---
type: page
title: Email address check
listed: false
slug: email-address-check
description: 
index_title: Email address check
hidden: 
keywords: 
tags: 
---

If you already have a verified email address for a user, you can ask Yoti to check if it is likely to be associated with someone aged over 18.

Yoti checks the email source, if it is linked to an employer and for any financial transactions tied to it.

{% badge type="warning" text="Note:" /%} To use this service, please contact our [support team](https://support.yoti.com/yotisupport/s/contactsupport) as the integration has to be whitelisted. The check should be only done on users who have verified ownership of their email address.

### Endpoint

The API endpoint to request the email address check for age:

{% code %}
{% tab language="http" %}
POST /api/v2/non-interactive
{% /tab %}
{% /code %}

### Request

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
| type | OVER | To determine the user is OVER the threshold. | 
| threshold | 18 | Age threshold for over age check. | 
| evidence | email, country | User's verified email address and country code. | 
{% /table %}

- All the values are required.
- US check is based on databases and has the greatest coverage.
- Non-US is based on heuristics about the type of email address and has limited coverage.
- We will attempt to filter out bad emails.

### Response

The JSON structure for the API response:

{% code %}
{% tab language="json" %}
{
    "type": "OVER",
    "age": 18,
    "status": "COMPLETE",
    "method": "EMAIL",
    "attempts": 0,
    "created_at": "2025-04-09T10:54:28.843Z",
    "evidence_id": "string"
}
{% /tab %}
{% /code %}

{% table widths="142,266" %}
| Field | Value | Description | 
| ---- | ---- | ---- | 
| type | OVER | Configured type property. | 
| age | 18 | Configure age threshold. | 
| status | ERROR, FAIL, \n\nCOMPLETE, PENDING | Status of the check. | 
| method | EMAIL | The method used to run the check. | 
| created_at | Timestamp (UTC) | Timestamp of the request. | 
| evidence_id | String | Unique evidence ID for the check. | 
{% /table %}