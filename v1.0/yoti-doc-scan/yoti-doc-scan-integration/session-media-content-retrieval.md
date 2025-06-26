---
type: page
title: Session media content retrieval
listed: true
slug: session-media-content-retrieval
description: 
index_title: Session media content retrieval
hidden: 
keywords: 
tags: 
---

The session will detail the tasks and checks completed along with the results, the associated media (e.g. a passport image) can now be retrieved. 

 The media_id value can be obtained from the session retrieval request . There will be a media ID associated with each media resource, for example the front and back images for a Driving Licence would each have a media ID.

**Base URL**: Please contact Yoti for this on [sdksupport@yoti.com](mailto:sdksupport@yoti.com)

Request authentication will be required. Full details for the required authorisation headers can be found [here](/yoti-doc-scan/authentication-and-headers).

{% table %}
| Endpoint | 
| ---- | 
| GET /idverify/v1/sessions/{session_id}/media/{media_id}/content?sdkId={sdkId}&amp;nonce={nonce}&amp;timestamp={timestamp} | 
{% /table %}

{% table %}
| Parameters | Description | Example | 
| ---- | ---- | ---- | 
| session_id | The session id obtained from the generate session request | 9d539c59-1cd0-4e2c-bed8-eb525248aa84 | 
| media_id | The media id, obtained from the retrieve session request | e43815b4-f0ea-4961-9033-2a9b98549c6c | 
| sdkId | The SDK ID from your Yoti Hub | b3c6bed3-8f17-46b1-a008-3aebc2da0b79 | 
| nonce | Unique ID for this request transaction. This should be in GUID form and should be uniquely generated for each request | 24487c75-0d20-457f-918a-c0abe5b1473b | 
| timestamp | A timestamp in milliseconds for the request&nbsp; | 1540457718692 | 
{% /table %}

### Response

The response will depend on Content-Type, this is defined in the media section in the session retrieve response.

### Response code

{% table %}
| Response Code | Description | 
| ---- | ---- | 
| 200 | OK | 
| 400 | Bad Request | 
| 401 | Unauthorised request (wrong, missing or expired token) | 
| 404 | Media not found | 
{% /table %}