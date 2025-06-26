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
{% tab language="json" title="Completed" %}
{
  "status": "COMPLETED"
}
{% /tab %}
{% tab language="json" title="Archived" %}
{
  "status":"ARCHIVED"
}
{% /tab %}
{% tab language="json" title="Active" %}
{
  "status": "ACTIVE"
}
{% /tab %}
{% tab language="json" title="Error" %}
{
  "envelope_id": "<envelopeId>",
  "status": "ERRORED",
  "details": {
    "errors": [
      {
        "file_name": "sample.pdf",
        "code": "<ERROR MESSAGE>"
      }
    ]
  }
}
{% /tab %}
{% /code %}

---

### Error response

If the request is unsuccessful a response code and a message will be sent:

{% table widths="" %}
| Response | Description | 
| ---- | ---- | 
| 400 | Bad Request, example: id provided not a UUID | 
| 401 | Unauthorised request, example: requesting the status on an envelope you are not authorized to view | 
| 403 | Forbidden, requesting user did not create the envelope | 
| 404 | The envelope ID couldn’t be found | 
{% /table %}