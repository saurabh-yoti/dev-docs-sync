---
type: page
title: Notifications
listed: true
slug: notifications
description: 
index_title: Notifications
hidden: 
keywords: 
tags: 
---

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