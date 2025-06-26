---
type: page
title: Get IDV Session PDF
listed: true
slug: get-idv-session-pdf
description: 
index_title: Get IDV Session PDF
hidden: 
keywords: 
tags: 
---

This endpoint will return the result of the Identity verification session within a pdf.

{% code %}
{% tab language="http" %}
GET https://api.yotisign.com/v2/idv/recipients/:recipientID/sessions/signed/pdf
{% /tab %}
{% /code %}

---

### Headers Explained

The following elements are needed:

{% table widths="208" %}
| Header | Description | 
| ---- | ---- | 
| Authorisation (header) | API Key to call the Yoti Sign API. This should be sent as a bearer token. | 
{% /table %}

---

### Response

On success, we return a 200 with a .zip file as an attachment containing the pdf report.

{% badge type="error" text="Important" /%} if a recipient successfully signed but was unable to complete a session due to a technical error the session status will be ONGOING, and we will be unable to create a session PDF so will respond with a 409.