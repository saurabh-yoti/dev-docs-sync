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

This page details how to retrieve session results for an Age verification session. Two options are available:

- Fetching the session status (GET endpoint)
- Webhook notifications

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
     Webhook notifications should be subscribed to for the Identity verification AV method as this does not return an immediate result.
    </div>
</div>
{% /html %}

## Session retrieval

{% code %}
{% tab language="http" %}
GET https://age.yoti.com/api/v1/sessions/<sessionId>/result
{% /tab %}
{% /code %}

{% table %}
| Header | Description | 
| ---- | ---- | 
| Authorization | API Key to call the Yoti Age API. This must be sent as a bearer token | 
| Content-Type | application/json | 
| Yoti-SDK-Id | Your unique SDK ID (uuid) | 
{% /table %}

Example response:

{% code %}
{% tab language="json" title="Complete" %}
{
    "sdk_id": "<uuid>",
    "callback_url": "https://your.callback.url",
    "notification_url": "https://your.webhook.url",
    "type": "OVER",
    "age_estimation": {
        "threshold": 18,
        "allowed": true,
        "level": "NONE"
    },
    "digital_id": {
        "threshold": 19,
        "allowed": true,
        "level": "NONE"
    },
    "doc_scan": {
        "threshold": 25,
        "allowed": true,
        "level": "NONE"
    },
    "age": 18,
    "status": "COMPLETE",
    "method": "AGE_ESTIMATION",
    "reference_id": "",
    "created_at": "2021-04-28T14:44:00.263517Z",
    "expires_at": "2030-10-30T20:04:00.263517Z",
    "updated_at": "2021-04-28T14:44:36.056933Z",
    "id": "<uuid>",
    "evidence_id": "<uuid>",
    "biometric_consent_required": true
}
{% /tab %}
{% tab language="json" title="Pending" %}
{
    "sdk_id": "<uuid>",
    "callback_url": "https://your.callback.url",
    "notification_url": "https://your.webhook.url",
    "type": "OVER",
    "age_estimation": {
        "threshold": 18,
        "allowed": true,
        "level": "NONE",
        "authenticity": "NOT_APPLICABLE"
    },
    "digital_id": {
        "threshold": 19,
        "allowed": true,
        "level": "NONE",
        "authenticity": "NOT_APPLICABLE"
    },
    "doc_scan": {
        "threshold": 25,
        "allowed": true,
        "level": "NONE",
        "authenticity": "MANUAL"
    },
    "status": "PENDING",
    "reference_id": "",
    "created_at": "2021-05-20T15:53:22.173259Z",
    "expires_at": "2030-11-21T21:13:22.173259Z",
    "updated_at": "2021-05-20T15:53:22.173259Z",
    "id": "affa597b-84fd-4481-a6c0-d3c30c43155e",
    "biometric_consent_required": true
}
{% /tab %}
{% /code %}

{% table %}
| Field | Value | Description | 
| ---- | ---- | ---- | 
| sdk_id | uuid | SDK ID for a given session. | 
| callback_url | string | Configured callback_url property in session creation. | 
| notification_url | string | Configured notification_url property in session creation. | 
| type | AGE, \n\nOVER,\n\nUNDER | Configured type property in session creation. | 
| age_estimation | object | Configured age_estimation properties in session creation. | 
| digital_id | object | Configured digital_id properties in session creation. | 
| doc_scan | object | Configured doc_scan properties in session creation. | 
| age | integer | Returns the actual age if type AGE. Otherwise returns the threshold value. | 
| status | PENDING\n\n\n\nIN_PROGRESS\n\n\n\nFAIL\n\n\n\nCOMPLETE\n\n\n\nERROR | PENDING - User has not started any checks.\n\n\nIN_PROGRESS - Checks have begun on the session, awaiting result to be returned.\n\n\nFAIL - The session has been completed, however the user has failed to meet the age threshold. FAIL will be returned only for 'OVER' and 'UNDER' attempts.\n\n\nCOMPLETE - The session has been completed, the user has passed the required threshold or an age has been returned.\n\n\nERROR - We could not provide an age result or calculate the threshold. This may be because the face was not recognised during age estimation or the ID document could not be processed through Doc Scan.\n\n\nAdditional states may be added in future releases and therefore mapping methods should contain default values. | 
| method | string | The AV method used to complete the session. | 
| reference_id | string | Configured reference_id property in session creation. | 
| created_at | timestamp | Timestamp of session creation. | 
| expires_at | timestamp | Timestamp of session expiry. | 
| updated_at | timestamp | Timestamp of last session update. | 
| id | uuid | ID of session. | 
| evidence_id | uuid | An ID relating to a specific Age verification attempt. | 
| biometric_consent_required | boolean | Configured biometric_consent_required properties in session creation. | 
{% /table %}

## Notifications

Each session has a configured 'time to live' (TTL) which must be above 60 seconds (1 minute). When a session is created, it remains active until it's time to live is reached.

To receive the result of an age verification, a HTTP endpoint (notification URL) needs to be listening for a JSON payload in the format of the below through a POST method. 

Notifications require HTTPS and will be reattempt if a 200 status code is not received. It is important to acknowledge the notification with a 200 status code to avoid receiving repeat notifications.

Below is an example payload:

{% code %}
{% tab language="json" %}
{
  "method": "AGE_ESTIMATION",
  "result": false,
  "age": 30,
  "session_key": "69db8ad4-c983-40b3-b95a-a8fa576e70a6",
  "reference_id": "some_reference_id",
  "id": "2480375e-ddc0-4832-9b82-b1d14af5cf75",
  "timestamp": 1613482863,
  "notification_url": "https://mynotification.example.com",
  "evidence_id": "da4070de-3d34-44d7-86d4-7d6fdf547740",
  "state": "FAIL",
  "check_type": "NONE",
  "sequence_number": 1,
  "signature": "some_signature"
}
{% /tab %}
{% /code %}

{% table %}
| Field | Value | Description | 
| ---- | ---- | ---- | 
| method | AGE_ESTIMATION\n\n\n\nDOC_SCAN\n\n\n\nDIGITAL_ID | The method used to complete the Age verification session. | 
| result | true\n\n\n\nfalse | The result is true if the user met the OVER or UNDER criteria, false if not. The result is always true for type of AGE when an age is returned. | 
| age | integer | Returns the actual age if type AGE. Otherwise returns the threshold value. | 
| session_key | uuid | The Age verification session ID. | 
| reference_id | string | The reference_id submitted to the session create endpoint is returned in this field. | 
| id | uuid | Notification ID. | 
| timestamp | epoch timestamp | Timestamp for when the notification was sent. | 
| notification_url | string | The notification_url submitted to the session create endpoint is returned in this field. | 
| evidence_id | uuid | An ID relating to a specific Age verification attempt. | 
| state | FAIL\n\n\n\nCOMPLETE\n\n\n\nERROR | FAIL - The session has been completed, however the user has failed to meet the age threshold. FAIL will be returned only for 'OVER' and 'UNDER' attempts.\n\n\nCOMPLETE - The session has been completed, the user has passed the required threshold or an age has been returned.\n\n\nERROR - We could not provide an age result or calculate the threshold. This may be because the face was not recognised during age estimation or the ID document could not be processed through Doc Scan.\n\n\nAdditional states may be added in future releases and therefore mapping methods should contain default values. | 
| check_type | NONE\n\n\n\nACTIVE\n\n\n\nPASSIVE | Returns the type of liveness check that was performed in the Age verification session. This is specified as the 'level' at session creation. | 
| sequence_number | integer | The attempt number for the current notification. Starts at 1. | 
| signature | string | Signed notification payload which can be verified using the Age verification public key. | 
{% /table %}