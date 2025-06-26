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

You can create two types of requests using the API:

{% table widths="470" %}
| Endpoint | Description | 
| ---- | ---- | 
| {% badge type="success" text="POST" /%} [https://api.yoti.com/ai/v1/age-verify](https://api.yoti.com/ai/v1/age-verify) | Use Yoti's Age estimation verify service. | 
| {% badge type="success" text="POST " /%} [https://api.yoti.com/ai/v1/age-antispoofing-verify](https://api.yoti.com/ai/v1/age-antispoofing-verify) | Use Yoti's Age estimation verify service and the Anti-spoofing check. | 
{% /table %}

## Request

The JSON object body for the API request has the following structure:

{% code %}
{% tab language="json" %}
{
    "img": "base64_image",
    "threshold": "age_threshold",
    "operator": "OVER" | "UNDER",
    "metadata": (Optional) {        
        "device": "mobile", "laptop", "unknown"
    },
}
{% /tab %}
{% /code %}

### Example request

A typical API request would have the following JSON body:

{% code %}
{% tab language="json" %}
{
    "img": "/9j/4AAQSkZJRgABAgAAAQABAAD/2wAcHNXCKigjEaYH51Me1Zy1Za0P/Z....",
    "threshold": 25,
    "operator": "OVER",
    "metadata": {        
        "device": "mobile"
    }
}
{% /tab %}
{% /code %}

### Relaxed image requirements

When using the Age only endpoint, it is possible to lower the threshold for face detection and image validation. A reason for this might be that images are not being captured live through Yoti's Face Capture module, or you may want to estimate age for images without needing to perform a liveness check.

{% code %}
{% tab language="json" %}
{
    "img": "/9j/4AAQSkZJRgABAgAAAQABAAD/2wAcHNXCKigjEaYH51Me1Zy1Za0P/Z....",
    "img_validation_level": "low"
}
{% /tab %}
{% /code %}

{% badge type="warning" text="Note:" /%} This may only be used with the age endpoint.

## Response

The JSON object body returned from the API has the following structure:

{% code %}
{% tab language="json" %}
{
    "age": {
				"age_check": "pass | fail" (string)     
		},
  	"antispoofing": {
				"prediction": "real | fake" 
		}
}
{% /tab %}
{% /code %}

{% table widths="225" %}
| Response | Explained | 
| ---- | ---- | 
| Prediction - real | Yoti has detected a real user. | 
| Prediction - fake | Yoti has detected a spoof attempt. | 
| Age - pass | The estimation age of the user has passed the age threshold. | 
| Age - fail | The estimation age of the user has failed the age threshold. | 
{% /table %}

### Example response

The response received from the API will be below, depending on the endpoint used.

{% code %}
{% tab language="json" title="/age-verify" %}
{
    "age_check": "pass"
}
{% /tab %}
{% /code %}

{% code %}
{% tab language="json" title="/age-antispoofing-verify" %}
{
    "age": {
        "age_check": "pass"
    },
    "antispoofing": {
        "prediction": "real"
    }
}
{% /tab %}
{% /code %}

{% synced id="ae-error-codes" %}
{% /synced %}