---
type: page
title: Results
listed: true
slug: results
description: 
index_title: Results
hidden: 
keywords: 
tags: 
---

This section provides details on how to retrieve session results for an Age verification session. Two options are available:

- Fetching the session status (GET endpoint)
- Webhook notifications

{% callout type="info" title="Good to know" %}
By default, the document scan and credit card age verification method does not return an immediate result upon user redirection.

We recommend polling the result endpoint every 5 seconds, up to three times, or utilising webhooks if using the document scan or credit card method.

Alternatively, enabling the property synchronous_checks will hold the user in the Yoti AVS flow and only redirect once results have finished processing.
{% /callout %}

{% code %}
{% tab language="http" %}
GET https://age.yoti.com/api/v1/sessions/<sessionId>/result
{% /tab %}
{% /code %}

{% table widths="" %}
| Header | Description | 
| ---- | ---- | 
| Authorization | API Key to call the Yoti Age API. Should be sent as a 'Bearer {{API_TOKEN}}'. | 
| Content-Type | application/json | 
| Yoti-SDK-Id | Your unique SDK ID (uuid) | 
{% /table %}

## Example response

{% code %}
{% tab language="json" title="Complete" %}
{
    "sdk_id": "5d3add31-3a3a-4d3b-a6b4-347edb35264c",
    "account_id": "",
    "callback_url": "https://www.yoti.com",
    "callback": {
        "url": "https://www.yoti.com",
        "auto": true
    },
    "notification_url": "https://webhook.site/0d11f3a1-cb6f-4df4-9b84-25afd378ff15",
    "cancel_url": "https://www.google.com",
    "type": "OVER",
    "age_estimation": {
        "threshold": 21,
        "allowed": true,
        "level": "NONE",
        "authenticity": "AUTO",
        "attempts": 0,
        "attempts_remaining": 1
    },
    "digital_id": {
        "threshold": 18,
        "allowed": true,
        "level": "NONE",
        "authenticity": "NOT_APPLICABLE",
        "attempts": 1,
        "attempts_remaining": 1
    },
    "doc_scan": {
        "threshold": 18,
        "allowed": true,
        "level": "PASSIVE",
        "authenticity": "AUTO",
        "attempts": 0,
        "attempts_remaining": 2
    },
    "credit_card": {
        "threshold": 0,
        "allowed": false,
        "level": "",
        "authenticity": "",
        "attempts": 0,
        "attempts_remaining": 0
    },
    "mobile": {
        "threshold": 0,
        "allowed": false,
        "level": "",
        "authenticity": "",
        "attempts": 0,
        "attempts_remaining": 0
    },
    "login": {
        "threshold": 0,
        "allowed": false,
        "level": "",
        "authenticity": "",
        "attempts": 0,
        "attempts_remaining": 0
    },
    "age_key": {
        "threshold": 0,
        "allowed": false,
        "level": "",
        "authenticity": "",
        "attempts": 0,
        "attempts_remaining": 0
    },
    "la_wallet": {
        "threshold": 0,
        "allowed": false,
        "level": "",
        "authenticity": "",
        "attempts": 0,
        "attempts_remaining": 0
    },
    "social_security_number": {
        "threshold": 0,
        "allowed": false,
        "level": "",
        "authenticity": "",
        "attempts": 0,
        "attempts_remaining": 0
    },
    "us_florida_hb3": {
        "threshold": 0,
        "allowed": false,
        "level": "",
        "authenticity": "",
        "attempts": 0,
        "attempts_remaining": 0
    },
    "double_anonymity": {
        "threshold": 0,
        "allowed": false,
        "level": "",
        "authenticity": "",
        "attempts": 0,
        "attempts_remaining": 0
    },
    "electronic_id": {
        "threshold": 0,
        "allowed": false,
        "sub_methods": null,
        "attempts": 0,
        "attempts_remaining": 0
    },
    "age": 18,
    "status": "COMPLETE",
    "method": "DIGITAL_ID",
    "reference_id": "over_18_example",
    "created_at": "2025-04-16T08:54:34.739262Z",
    "expires_at": "2025-04-16T09:04:34.739262Z",
    "updated_at": "2025-04-16T08:55:45.426737Z",
    "id": "14010f56-3f04-4f1f-84e7-a43ff723ef86",
    "evidence_id": "4786ecb7-c10c-4037-9947-aaa6507e7414",
    "biometric_consent_required": true,
    "rule_id": "",
    "retry_enabled": true,
    "resume_enabled": true,
    "blocked_locations": [],
    "biometric_consent_given_at": "",
    "terminal_id": "",
    "synchronous_checks": true
}
{% /tab %}
{% tab language="json" title="Pending" %}
{
    "sdk_id": "5d3add31-3a3a-4d3b-a6b4-347edb35264c",
    "account_id": "",
    "callback_url": "https://www.yoti.com",
    "callback": {
        "url": "https://www.yoti.com",
        "auto": true
    },
    "notification_url": "https://yourdomain.example/webhook",
    "cancel_url": "https://www.google.com",
    "type": "OVER",
    "age_estimation": {
        "threshold": 21,
        "allowed": true,
        "level": "NONE",
        "authenticity": "AUTO",
        "attempts": 0,
        "attempts_remaining": 1
    },
    "digital_id": {
        "threshold": 18,
        "allowed": true,
        "level": "NONE",
        "authenticity": "NOT_APPLICABLE",
        "attempts": 0,
        "attempts_remaining": 2
    },
    "doc_scan": {
        "threshold": 18,
        "allowed": true,
        "level": "PASSIVE",
        "authenticity": "AUTO",
        "attempts": 0,
        "attempts_remaining": 2
    },
    "credit_card": {
        "threshold": 0,
        "allowed": false,
        "level": "",
        "authenticity": "",
        "attempts": 0,
        "attempts_remaining": 0
    },
    "mobile": {
        "threshold": 0,
        "allowed": false,
        "level": "",
        "authenticity": "",
        "attempts": 0,
        "attempts_remaining": 0
    },
    "login": {
        "threshold": 0,
        "allowed": false,
        "level": "",
        "authenticity": "",
        "attempts": 0,
        "attempts_remaining": 0
    },
    "age_key": {
        "threshold": 0,
        "allowed": false,
        "level": "",
        "authenticity": "",
        "attempts": 0,
        "attempts_remaining": 0
    },
    "la_wallet": {
        "threshold": 0,
        "allowed": false,
        "level": "",
        "authenticity": "",
        "attempts": 0,
        "attempts_remaining": 0
    },
    "social_security_number": {
        "threshold": 0,
        "allowed": false,
        "level": "",
        "authenticity": "",
        "attempts": 0,
        "attempts_remaining": 0
    },
    "us_florida_hb3": {
        "threshold": 0,
        "allowed": false,
        "level": "",
        "authenticity": "",
        "attempts": 0,
        "attempts_remaining": 0
    },
    "double_anonymity": {
        "threshold": 0,
        "allowed": false,
        "level": "",
        "authenticity": "",
        "attempts": 0,
        "attempts_remaining": 0
    },
    "electronic_id": {
        "threshold": 0,
        "allowed": false,
        "sub_methods": null,
        "attempts": 0,
        "attempts_remaining": 0
    },
    "status": "PENDING",
    "reference_id": "over_18_example",
    "created_at": "2025-04-09T12:34:33.455033Z",
    "expires_at": "2025-04-10T16:21:13.455033Z",
    "updated_at": "2025-04-09T12:34:33.455033Z",
    "id": "bb005956-650d-4368-a4d6-212268a8f875",
    "biometric_consent_required": true,
    "rule_id": "",
    "retry_enabled": true,
    "resume_enabled": true,
    "blocked_locations": [],
    "biometric_consent_given_at": "",
    "terminal_id": "",
    "synchronous_checks": true
}
{% /tab %}
{% /code %}

{% table widths="" %}
| Field | Value | Description | 
| ---- | ---- | ---- | 
| sdk_id | uuid | SDK ID for a given session. | 
| callback_url | string | Configured callback_url property in session creation. | 
| notification_url | string | Configured notification_url property in session creation. | 
| type | AGE, \n\nOVER,\n\nUNDER | Configured type property in session creation. | 
| age_estimation | object | Configured age_estimation properties in session creation. | 
| digital_id | object | Configured digital_id properties in session creation. | 
| doc_scan | object | Configured doc_scan properties in session creation. | 
| credit_card | object | Configured credit_card properties in session creation. | 
| mobile | object | Configured mobile properties in session creation. | 
| login | object | Configured login properties in session creation. | 
| la_wallet | object | Configured la_wallet properties in session creation. | 
| social_security_number | object | Configured social_security_number properties in session creation. | 
| age | integer | Returns the actual age if type AGE. Otherwise returns the threshold value. | 
| status | PENDING\n\n\n\nIN_PROGRESS\n\n\n\nFAIL\n\n\n\nCOMPLETE\n\n\n\nERROR\n\n\n\nCANCELLED\n\n\n\nEXPIRED | PENDING - User has not started any checks.\n\n\nIN_PROGRESS - Checks have begun on the session, awaiting result to be returned.\n\n\nFAIL - The session has been completed, however the user has failed to meet the age threshold. FAIL will be returned only for 'OVER' and 'UNDER' attempts.\n\n\nCOMPLETE - The session has been completed, the user has passed the required threshold or an age has been returned. Always 'COMPLETE' if AGE type is configured.\n\n\nERROR - We could not provide an age result or calculate the threshold. This may be because the face was not recognised during age estimation or if the ID document was processed via Doc Scan, but we do not believe that it is a genuine document.\n\n\nCANCELLED - The user no longer wishes to prove their age, and aborts the session.\n\n\nEXPIRED - The session has expired and is no longer useable\n\n\nAdditional states may be added in future releases, any mapping methods should account for 'unknown' values. | 
| method | string | The AV method used to complete the session. | 
| reference_id | string | Configured reference_id property in session creation. | 
| created_at | timestamp | Timestamp of session creation. | 
| expires_at | timestamp | Timestamp of session expiry. | 
| updated_at | timestamp | Timestamp of last session update. | 
| id | uuid | ID of session. | 
| evidence_id | uuid | An ID relating to a specific Age verification attempt. | 
| biometric_consent_required | boolean | Configured biometric_consent_required properties in session creation. | 
| biometric_consent_given_at | timestamp | Timestamp of biometric consent. | 
| terminal_id | string | Value set for the Yoti-Terminal-Id header in session creation. | 
| synchronous_checks | true / false | Value set for the synchronous_checks property. | 
{% /table %}