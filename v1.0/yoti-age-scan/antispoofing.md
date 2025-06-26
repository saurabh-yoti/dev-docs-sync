---
type: page
title: AntiSpoofing
listed: true
slug: antispoofing
description: 
index_title: AntiSpoofing
hidden: 
keywords: 
tags: 
---

Anti-spoofing is achieved by capturing the background image that does not contain any human faces. This background image is then compared to all future age estimation requests and ensures that the photo cannot be taken at another location. 

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1564055807/17672/xpwsr88cxkvw7eebgozl.png" mode="responsive" height="1200" width="1600" %}
{% /image %}

This functionality will require two invocations of the API:

1. Submit a background image, this will be used in each age estimation request to ensure the background match
2. Submit the photo for age estimation, with the associated background Id.

The Background setup (Anti-Spoofing mechanism) URI will take the form:

{% code %}
{% tab language="http" %}
POST /api/v1/age-verification/backgrounds?nonce=(…)&timestamp=(…)
{% /tab %}
{% /code %}

{% table %}
| Parameter | Description | Example | 
| ---- | ---- | ---- | 
| nonce | Unique ID for this request transaction. This should be in GUID form and should be uniquely generated for each request.&nbsp;&lt;br&gt; | 23487c75-0d20-457f-918a-c0abe5b1473b | 
| timestamp | A timestamp in milliseconds for the request&lt;br&gt; | 1540457718692 | 
{% /table %}

## Authorisation and Headers

All requests to a Yoti API require a form of authorisation. This API requires the following headers. These headers should be the same for both the setup of the Anti-spoofing background and the age estimation request.

{% table %}
| Header | Purpose | 
| ---- | ---- | 
| X-Yoti-Auth-Digest | Base64 encoded signed hash of the request, signed using the Key file pair associated with your Yoti Application. Steps to generate are described below | 
| X-Yoti-Auth-Id&lt;br&gt; | The SDK ID associated with the Yoti Application. | 
| ContentType&lt;br&gt; | The body content type – this will be application/json | 
{% /table %}

The X-Yoti-Auth-Digest should be composed from the following

- HTTP method, i.e. POST
- URI Path (from /backgrounds or /checks onwards)
- Request Body – Encoded representation of the image

These should be appended with an ‘&’.

### Post Background

{% code %}
{% tab language="http" %}
POST&/backgrounds?nonce=b98a5ac6-5336-4594-8690-68a4e8223b0c&timestamp=1541694094210&<Body Omitted>
{% /tab %}
{% /code %}

### Post Age estimation check

{% code %}
{% tab language="http" %}
POST&/checks?nonce=b98a5ac6-5336-4594-8690-68a4e8223b0c&timestamp=1541694094210&<Body Omitted>
{% /tab %}
{% /code %}

This should then be signed using the Yoti Application PEM file, and the resulting signature encoded in Base64.

### Request Body - Setup background

{% table %}
| Element | Description | 
| ---- | ---- | 
| data | A&nbsp;base64 encoded representation of the background image to set | 
{% /table %}

{% code %}
{% tab language="json" %}
{
  "data": "<Base64 Encoded Image>"
}
{% /tab %}
{% /code %}

### Example request - Setup background

**Hostname**: Available upon request

{% code %}
{% tab language="http" %}
POST https://<HOSTNAME>:<PORT>/api/v1/age-verification/backgrounds?nonce=99fbfdb2-b18d-413d-8bdb-9df0b7bbd541&timestamp=1541697968659&<Body Omitted>
{% /tab %}
{% /code %}

**Headers**

{% code %}
{% tab language="http" %}
X-Yoti-Auth-Id: a1c06cbb-e810-4150-bf7a-67073b659f8d

X-Yoti-Auth-Digest: qoMA1Pb8IaC4vv7DzgkZY5tD0hkHT+bV1rnFX3EDMfr3lHilbdZakE....

ContentType: application/json
{% /tab %}
{% /code %}

**Body**

{% code %}
{% tab language="json" %}
{
  "data": " /9j/4AAQSkZJRgABAgAAAQABAAD/2wBDAAgGBgcGBQgHBw……"
}
{% /tab %}
{% /code %}

### Example Request – Check Age (With Anti Spoofing)

**Hostname**: Available upon request from [sdksupport@yoti.com](mailto:sdksupport@yoti.com)

{% code %}
{% tab language="http" %}
POST https://<HOSTNAME>:<PORT>/api/v1/age-verification/checks?nonce=99fbfdb2-b18d-413d-8bdb-9df0b7bbd541&timestamp=1541697968659&<Body Omitted>
{% /tab %}
{% /code %}

**Headers**

{% code %}
{% tab language="http" %}
X-Yoti-Auth-Id: a1c06cbb-e810-4150-bf7a-67073b659f8d
X-Yoti-Auth-Digest: qoMA1Pb8IaC4vv7DzgkZY5tD0hkHT+bV1rnFX3EDMfr3lHilbdZakE....
ContentType: application/json
{% /tab %}
{% /code %}

**Body**

{% code %}
{% tab language="json" %}
{
  "data": "/9j/4AAQSkZJRgABAgAAAQABAAD/2wAcHNXCKigjEaYH51Me1Zy1Za0P/Z",
  "background_id": "4e08364e-a55a-4794-a93b-8f4d70d432ba"
}
{% /tab %}
{% /code %}

### Example Response – Check Age (With Anti Spoofing)

This request will return a HTTP 200 OK if the age can be estimated.

{% code %}
{% tab language="json" %}
{
  "pred_age": 29.7475,
  "uncertainty": 2.04677
}
{% /tab %}
{% /code %}

{% table %}
| Element | Description | 
| ---- | ---- | 
| pred_age | The predicted age in years | 
| uncertainty | The uncertainty value in years | 
{% /table %}

### Error codes

{% table %}
| Code | Description | 
| ---- | ---- | 
| 401 | There is an error in the X-Yoti-Auth-Digest signature or SDK ID.&nbsp; | 
| 400 | Bad request - details provided in response body | 
| 404 | Background image not found | 
| 500 | Internal server error | 
{% /table %}

{% table %}
| Code | Description | 
| ---- | ---- | 
| 1 | Image too big | 
| 2 | Unable to decode image (not a jpeg or wrong base64 string) | 
| 3 | No face detected | 
| 4 | Spoofing attempt detected | 
{% /table %}