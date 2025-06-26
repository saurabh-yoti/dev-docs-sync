---
type: page
title: Media content deletion (Optional)
listed: true
slug: media-content-deletion--optional-
description: 
index_title: Media content deletion (Optional)
hidden: 
keywords: 
tags: 
---

Specific media can be deleted from the session by using a session and a media id. This can be requested before the defined retention period is up.

Please note that the session along with all associated resources and media will be automatically deleted once the retention period (defined in the session creation) is reached.

**Base URL**: Please contact Yoti for this on [sdksupport@yoti.com](mailto:sdksupport@yoti.com)

Request authentication will be required. Full details for the required authorisation headers can be found [here](/yoti-doc-scan/authentication-and-headers).

{% table %}
| Endpoint | 
| ---- | 
| DELETE /idverify/v1/sessions/{session_id}/media/{media_id}/content?sdkId={sdkId}&amp;nonce={nonce}&amp;timestamp={timestamp} | 
{% /table %}

{% table %}
| Parameter | Description | Example | 
| ---- | ---- | ---- | 
| session_id | The session id obtained from the generate session request | 9d539c59-1cd0-4e2c-bed8-eb525248aa84 | 
| media_id | The media id, obtained from the retrieve session request | e43815b4-f0ea-4961-9033-2a9b98549c6c | 
| sdkId | The SDK ID from your Yoti Hub | b3c6bed3-8f17-46b1-a008-3aebc2da0b79 | 
| nonce | Unique ID for this request transaction. This should be in GUID form and should be uniquely generated for each request&nbsp; | 24487c75-0d20-457f-918a-c0abe5b1473b | 
| timestamp | A timestamp in milliseconds for the request&nbsp; | 1540457718692 | 
{% /table %}

### Response Codes

{% table %}
| Response Code | Description | 
| ---- | ---- | 
| 204 | No Content | 
| 400 | Bad Request | 
| 401 | Unauthorised request (wrong key or signature)&lt;br&gt; | 
| 409 | Resource is locked | 
{% /table %}