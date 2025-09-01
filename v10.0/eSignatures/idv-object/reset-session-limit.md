---
type: page
title: Reset Session Limit
listed: true
slug: reset-session-limit
description: 
index_title: Reset Session Limit
hidden: 
keywords: 
tags: 
---

This endpoint will allow the session limit to be reset. resets are allowed until the max number of permitted sessions is 50 and when this endpoint is called it will simply double the amount of attempts that were originally configured.

{% code %}
{% tab language="http" %}
GET https://api.yotisign.com/v2/idv/recipients/:recipientID/sessions/reset-limit
{% /tab %}
{% /code %}

---

### Headers Explained

The following elements are needed:

{% table %}
| Headers | Description | 
| ---- | ---- | 
| Authorization (header) | API Key to call the Yoti Sign API. This should be sent as a bearer token. | 
{% /table %}

---

### Response

On success, we return a 200 and the previous session limit will have been doubled.