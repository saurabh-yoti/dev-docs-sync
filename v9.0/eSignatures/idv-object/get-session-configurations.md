---
type: page
title: Get Session Configurations
listed: true
slug: get-session-configurations
description: 
index_title: Get Session Configurations
hidden: 
keywords: 
tags: 
---

This API endpoint will allow you to see the prebuilt Yoti identity verification configurations, as well as any custom configurations that have been created.

{% code %}
{% tab language="http" %}
GET https://api.yotisign.com/v2/idv/sessions/configs
{% /tab %}
{% /code %}

---

### Headers Explained

The following elements are needed:

{% table %}
| Headers | Description | 
| ---- | ---- | 
| Authorization (header) | API Key to call the Yoti Sign API. This should be sent as a bearer token. | 
| Content-Type (header) | application/json | 
{% /table %}

---

### Request Body

In this request you have the ability to view the identity verification session configuration payloads in their entirety, to understand what you are requesting.

{% code %}
{% tab language="json" %}
{
  "detailed_session_configs": false
}
{% /tab %}
{% /code %}

{% table widths="214" %}
| Value | Description | 
| ---- | ---- | 
| detailed_session_configs | If set to true the JSON session configuration payloads for each result will also be included in the response, resulting in a very large payload. | 
{% /table %}

---

### Response

On success, we return a 200 with a JSON body matching the following schema:

{% code %}
{% tab language="json" %}
{
    "session_configs":
    [
        {
            "name": "Real Estate",
            "is_custom": false,
            "is_private": false
        },
        {
            "name": "HR",
            "is_custom": false,
            "is_private": false
        },
        {
            "name": "Finance",
            "is_custom": false,
            "is_private": false
        }
    ]
}
{% /tab %}
{% /code %}

---

## Error codes

If the request is unsuccessful we will respond with an appropriate HTTP code, and a message will be detailed in the response body.