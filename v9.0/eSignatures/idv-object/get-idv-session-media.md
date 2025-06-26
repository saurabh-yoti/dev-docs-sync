---
type: page
title: Get IDV session media
listed: true
slug: get-idv-session-media
description: 
index_title: Get IDV session media
hidden: 
keywords: 
tags: 
---

This endpoint will allow you to obtain the individual media generated in the identity verification session submitted in signing e.g the image of a document.

{% code %}
{% tab language="http" %}
GET https://api.yotisign.com/v2/idv/recipients/:recipientID/sessions/signed/media/:mediaID
{% /tab %}
{% /code %}

---

### Headers Explained

The following elements are needed:

{% table widths="242" %}
| Headers | Description | 
| ---- | ---- | 
| Authorization (header) | API Key to call the Yoti Sign API. This should be sent as a bearer token. | 
{% /table %}

---

### Response

On success, we return a 200 with the specified media. The content-type will be different depending on what is being received, e.g it will be JSON for the data extraction media but will be buffer for the image media.