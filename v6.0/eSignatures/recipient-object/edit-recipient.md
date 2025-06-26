---
type: page
title: Edit recipient
listed: true
slug: edit-recipient
description: 
index_title: Edit recipient
hidden: 
keywords: 
tags: 
---

Yoti gives you the ability to edit recipient information after sending the envelope so that if there is an error you are able to rectify it with out having to archive and then send a new envelope.

{% code %}
{% tab language="http" %}
PATCH https://api.yotisign.com/v2/envelopes/{envelope_id}/recipients/{recipient_id}
{% /tab %}
{% /code %}

---

## Header explained

The following elements are required in the header:

{% table %}
| Header | Description | 
| ---- | ---- | 
| Authorization | API Key to call the Yoti Sign API. This should be sent as a bearer token. | 
| Content-Type | application/json | 
{% /table %}

---

## Example body

{% code %}
{% tab language="http" %}
{
   "name": "foobar", // Optional
   "email": "test@example.com", // Optional
   "iso_country_code": "US", // Optional - If OTP is enabled
   "mobile_number": "2136210002", // Optional - If OTP is enabled
}
{% /tab %}
{% /code %}

Attributes within the payload body are all optional, however at least one property must be specified to make a change to the recipient within an envelope.

Both iso_country_code and mobile_number must be specified if at least one of these fields is included in the request.