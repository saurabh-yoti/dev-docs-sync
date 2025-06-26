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

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
     Webhook notifications should be subscribed to for the ID AV method as this may not always return an immediate result.
    </div>
</div>
{% /html %}

{% code %}
{% tab language="http" %}
GET https://age.yoti.com/api/v1/sessions/<session-id>/result
{% /tab %}
{% /code %}

{% table %}
| Header | Description | 
| ---- | ---- | 
| Authorization | API Key to call the Yoti Age Verification API. This must be sent as a bearer token | 
| Content-Type | application/json | 
| Yoti-SDK-Id | Your unique SDK ID (uuid) | 
{% /table %}

## Example response

{% code %}
{% tab language="json" title="Complete" %}
{
    "sdk_id": "<uuid>",
    "callback_url": "https://your.callback.url",
    "callback":{
      "url":"https://your.callback.url",
      "auto":false
   },
    "notification_url": "https://your.webhook.url",
    "cancel_url":"https://your.cancel.url",
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
    "credit_card":{
      "threshold":18,
      "allowed":true,
      "level":"",
      "authenticity":""
   },
   "mobile":{
      "threshold":18,
      "allowed":true,
      "level":"",
      "authenticity":""
   },
   "login":{
      "threshold":0,
      "allowed":false,
      "level":"",
      "authenticity":""
   },
    "age": 18,
    "status": "COMPLETE",
    "method": "DOC_SCAN",
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
| notification_url | string | Configured notification_url property in session creation. | 
| type | AGE, \n\nOVER,\n\nUNDER | Configured type property in session creation. | 
| doc_scan | object | Configured doc_scan properties in session creation. | 
| age | integer | Returns the actual age if type AGE. Otherwise returns the threshold value. | 
| status | PENDING\n\n\n\nIN_PROGRESS\n\n\n\nFAIL\n\n\n\nCOMPLETE\n\n\n\nERROR\n\n\n\nCANCELLED | PENDING - User has not started any checks.\n\n\nIN_PROGRESS - Checks have begun on the session, awaiting result to be returned.\n\n\nFAIL - The session has been completed, however the user has failed to meet the age threshold. FAIL will be returned only for 'OVER' and 'UNDER' attempts.\n\n\nCOMPLETE - The session has been completed, the user has passed the required threshold or an age has been returned.\n\n\nERROR - We could not provide an age result or calculate the threshold. This may be because the face was not recognised during age estimation or if the ID document was processed via Doc Scan, but we do not believe that it is a genuine document.\n\n\nCANCELLED - The user no longer wishes to prove their age, and aborts the session.\n\n\nAdditional states may be added in future releases and therefore mapping methods should contain default values. | 
| method | string | The AV method used to complete the session. | 
| reference_id | string | Configured reference_id property in session creation. | 
| created_at | timestamp | Timestamp of session creation. | 
| expires_at | timestamp | Timestamp of session expiry. | 
| updated_at | timestamp | Timestamp of last session update. | 
| id | uuid | ID of session. | 
| evidence_id | uuid | An ID relating to a specific Age verification attempt. | 
| biometric_consent_required | boolean | Configured biometric_consent_required properties in session creation. | 
{% /table %}