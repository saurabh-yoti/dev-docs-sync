---
type: page
title: API reference
listed: true
slug: api-reference
description: 
index_title: API reference
hidden: 
keywords: 
tags: 
---

The following provides information about API endpoints, response and error codes.

## Endpoints

You can create the age estimation and anti-spoofing request using the API:

{% table widths="470" %}
| Endpoint | Description | 
| ---- | ---- | 
| {% badge type="success" text="POST" /%} [https://api.yoti.com/ai/v1/self-checkout/age-antispoofing](https://api.yoti.com/ai/v1/self-checkout/age-antispoofing) | Use Yoti's Age estimation service and the Anti-spoofing check. | 
{% /table %}

## Headers

The API supports the following headers:

{% table widths="217" %}
| Header | Description | 
| ---- | ---- | 
| X-Yoti-Auth-Id | SDK ID for the Yoti Hub application. | 
| Terminal-Id | Unique ID per machine. Mandatory for non-browser integrations. | 
| Session-Id | May be provided to demonstrate multiple attempts are from a single user transaction. Optional. | 
{% /table %}

## Request

The JSON object body for the API request has the following structure:

{% code %}
{% tab language="json" %}
{
    "img": "base64encoded_image"
}
{% /tab %}
{% /code %}

### Example request

A typical API request will have a JSON body similar to the following:

{% code %}
{% tab language="json" %}
{
    "img": "/9j/4AAQSkZJRgABAgAAAQABAAD/2wAcHNXCKigjEaYH51Me1Zy1Za0P/Z...."
}
{% /tab %}
{% /code %}

## Response

The JSON object body returned from the API has the following structure:

{% code %}
{% tab language="json" %}
{
   "antispoofing": {
       "prediction": "real | fake"
   },
   "age": {
       "age": float,
     	 "st_dev": float
   }
}
{% /tab %}
{% /code %}

{% table widths="225" %}
| Response | Explained | 
| ---- | ---- | 
| Prediction - real | Yoti has detected a real user. | 
| Prediction - fake | Yoti has detected a spoof attempt. | 
| Age - age | The age estimation of the user. | 
| Age - st_dev | The st_dev value is an uncertainly value. Yoti recommends rejecting any response with an uncertainty greater than 6.0. Typically this indicates a problem with image capture. This should **only** be treated as a quality score. | 
{% /table %}

### Example response

The response received from the API will be similar to the following:

{% code %}
{% tab language="json" title="/self-checkout/age-antispoofing" %}
{
    "antispoofing": {
        "prediction": "real"
    },
    "age": {
        "age": 25.1,
        "st_dev": 3.5
    }
}
{% /tab %}
{% /code %}

{% synced id="ae-error-codes" %}
{% /synced %}