---
type: page
title: Applicants
listed: true
slug: create-applicant
description: 
index_title: Applicants
hidden: 
keywords: 
tags: 
---

## Create Applicant

The first step in the process is to create an applicant. An applicant will be a person whose face you want to search against. You can create multiple applicants, with each having one facial image added to it. 

{% code %}
{% tab language="http" %}
POST https://api.yoti.com/idverify/v1/applicants
{% /tab %}
{% /code %}

### Headers

{% table widths="" %}
| Headers | Value | 
| ---- | ---- | 
| Content-Type | application/json | 
| Accept | application/json | 
{% /table %}

### Request body

Adding a payload is **optional** in this request. But if you do opt to send a payload, you can directly add a face to the applicant upon creation of the applicant.

{% code %}
{% tab language="json" %}
{
  "face": {
    "data": "base64 encoded image",
  }
}
{% /tab %}
{% /code %}

### Response

The response generates an applicant id and will include the face if added in the request:

{% code %}
{% tab language="json" %}
{
    "id": 'eaa08767-2a59-47a7-9804-aa9f99ac9d93',
    "created_at": '2025-05-29T11:15:03Z',
    "last_updated": '2025-05-29T11:15:03Z',
    "faces": { "faces": [] },
    "pools": []
}
{% /tab %}
{% /code %}

---

## Add Face

Once an applicant has been created, you can then add a face of an individual to the applicant.

{% code %}
{% tab language="http" %}
POST https://api.yoti.com/idverify/v1/applicants/{applicantId}/faces
{% /tab %}
{% /code %}

### Request body

When adding a face to the applicant, you can either use an image that you already possess of an individual, or you can use an image that Yoti captured of an individual in a previous Yoti identity verification session.

{% code %}
{% tab language="json" %}
{
  "face": {
    "data": "base64 encoded image",
  }
}
{% /tab %}
{% /code %}

When using an image from a previous identity verification session, you need to supply the session id and media id that is linked to that image.

{% code %}
{% tab language="json" %}
{
  "face": {
    "source": {
      "session_id": "string",
      "media_id": "string"
    }
  }
}
{% /tab %}
{% /code %}

### Response

You will receive a unique id for the face upon a successful request:

{% code %}
{% tab language="json" %}
{
    "id": "<uuid>"
}
{% /tab %}
{% /code %}

---

## Error Responses

{% table widths="" %}
| Error code | Description | 
| ---- | ---- | 
| 400 | Bad request - there was an error when validating the request payload | 
| 401 | Unauthorised - the request to the endpoint is not authorised for the API keys use | 
| 403 | Insufficient permission - the sdk id does not have permission to use this service | 
| 422 | Unprocessable entity - cannot handle the content of the payload | 
| 404 | Not found - applicant can't be found linked to the supplied id | 
| 503 | Service unavailable - Yoti services are temporarily unavailable | 
{% /table %}