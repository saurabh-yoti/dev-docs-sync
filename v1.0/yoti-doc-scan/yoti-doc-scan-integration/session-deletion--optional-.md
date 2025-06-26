---
type: page
title: Session deletion (Optional)
listed: true
slug: session-deletion--optional-
description: 
index_title: Session deletion (Optional)
hidden: 
keywords: 
tags: 
---

The session, which includes  all associated resources and media, can be deleted from the Yoti system, before the retention period is reached. The endpoint and parameters required are described below.

Please note the session along with all associated resources and media will be automatically deleted once the retention period (defined in the session creation) is reached. 

**Base URL**: Please contact Yoti for this on [sdksupport@yoti.com](mailto:sdksupport@yoti.com)

Request authentication will be required. Full details for the required authorisation headers can be found [here](/yoti-doc-scan/authentication-and-headers).

{% table %}
| Endpoint | 
| ---- | 
| DELETE /idverify/v1/sessions/{session_id}?sdkId={sdkId}&amp;nonce={nonce}&amp;timestamp={timestamp} | 
{% /table %}

{% table %}
| Parameter | Description | Example | 
| ---- | ---- | ---- | 
| session_id | The session id obtained from the generate session request | 9d539c59-1cd0-4e2c-bed8-eb525248aa84 | 
| sdkId | The SDK ID from your Yoti Hub | b3c6bed3-8f17-46b1-a008-3aebc2da0b79 | 
| nonce | Unique ID for this request transaction. This should be in GUID form and should be uniquely generated for each request&nbsp; | 24487c75-0d20-457f-918a-c0abe5b1473b | 
| timestamp | A timestamp in milliseconds for the request&nbsp; | 1540457718692 | 
{% /table %}

### Response code

{% table %}
| Response Code | Description | 
| ---- | ---- | 
| 204 | No content | 
| 400 | Bad request | 
| 401 | Unauthorised request (wrong key or signature) | 
| 404 | Session not found | 
{% /table %}