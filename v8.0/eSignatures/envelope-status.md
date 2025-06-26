---
type: page
title: Envelope status
listed: true
slug: envelope-status
description: 
index_title: Envelope status
hidden: 
keywords: 
tags: 
---

Get envelope status

This endpoint allows you to query the Yoti Sign API for the current status of an envelope:

{% code %}
{% tab language="http" %}
Sandbox:
GET https://demo.api.yotisign.com/v2/envelopes/<envelopeId>/status
{% /tab %}
{% /code %}

{% code %}
{% tab language="http" %}
Production:
GET https://api.yotisign.com/v2/envelopes/<envelopeId>/status
{% /tab %}
{% /code %}

The same headers are required as for the endpoint above.

---

### Response

On success, we return a 200 with a JSON body matching the following schema:

{% code %}
{% tab language="json" %}
{
  "status": <COMPLETED/ARCHIVED/ACTIVE/ERRORED>
}
{% /tab %}
{% /code %}

---

### Error response

The same error codes will be provided as the endpoint above. An example of an error response:

{% code %}
{% tab language="json" %}
{
  "message" : "envelope not found"
}
{% /tab %}
{% /code %}