---
type: page
title: Handle the image
listed: true
slug: handle-the-image
description: 
index_title: Handle the image
hidden: 
keywords: 
tags: 
---

After capturing the image with the face capture module, you can make a request to our Age estimation endpoint to verify an individuals age. A base64 image will need to be sent in the request body to the following endpoint:

{% code %}
{% tab language="http" %}
POST https://age.yoti.com/api/v1/age-estimation
{% /tab %}
{% /code %}

### Headers explained

{% table %}
| Header | Description | 
| ---- | ---- | 
| Yoti-Sdk-Id | Your unique Sdk id | 
| Authorization | Your API key (bearer token) | 
{% /table %}

### Request Body

{% code %}
{% tab language="json" %}
{
    "image": "<base64 encoded image>",
    "type": "OVER | UNDER | AGE",
    "level": "PASSIVE | NONE"
}
{% /tab %}
{% /code %}

{% table %}
| Parameter | Types | Description | 
| ---- | ---- | ---- | 
| image | Base64 encoded image | Image of the user that the age estimation is performed on. | 
| type | OVER / UNDER / AGE | This is where you define what preference you want to set for the age of the user. | 
| threshold | Integer e.g 25 | Age threshold for under/over age limits. We recommend this to be the exact age of the threshold you want to cover. | 
| level | PASSIVE / NONE | Whether an Anti Spoofing test is applied to the image. | 
{% /table %}

### Successful Response Example

{% code %}
{% tab language="json" %}
{
    "type": "OVER",
    "method": "AGE_ESTIMATION",
    "threshold": 18,
    "age": 18,
    "result": true,
    "status": "COMPLETE",
    "evidence_id": "1cc829d7-6cba-420e-aec9-3a45d051a58b"
}
{% /tab %}
{% /code %}

### Error Response Example

{% code %}
{% tab language="json" %}
{
    "message": "<Message>",
    "error_code": "<Error_Code>"
}
{% /tab %}
{% /code %}

{% table %}
| Error Code | Message | 
| ---- | ---- | 
| E600408 | Spoofing attempt detected | 
| PAYLOAD_TOO_LARGE | Payload too large. | 
| IMAGE_NOT_PROVIDED | Image has not been provided. | 
| INVALID_B64_IMAGE | - Base64 image is incorrectly padded.\n- Cannot create image from base64 decoded bytes | 
| UNSUPPORTED_IMAGE_FORMAT | Image format not supported. Please use JPEGs (95 to 100 quality) and PNGs. | 
| IMAGE_SIZE_TOO_BIG | Image size too big, the maximum size is 1.5MB. | 
| IMAGE_SIZE_TOO_SMALL | Image size too small, the minimum size is 50KB. | 
| MIN_HEIGHT | The image height is incorrect. Image minimum height required is 300 pixels. | 
| MAX_HEIGHT | The image height is incorrect. Image maximum height required is 2000 pixels. | 
| MIN_WIDTH | The image width is incorrect. Image minimum width required is 300 pixels. | 
| MAX_WIDTH | The image width is incorrect. Image maximum width required is 2000 pixels. | 
| MIN_PIXELS | To process the image the minimum number of pixels required is 90,000 pixels. | 
| MAX_PIXELS | To process the image the maximum number of pixels required is 2,100,000 pixels. | 
| IMAGE_WRONG_CHANNELS | Missing colour channel, the input image must be RGB or RGBA. | 
| IMAGE_GRAYSCALE_NOT_SUPPORTED | Grayscale images not supported. | 
| FACE_NOT_FOUND | Face not found. | 
| MULTIPLE_FACES | Multiple faces in the image provided. | 
| FACE_BOX_TOO_SMALL | The face in the image provided is too small. | 
| FACE_TO_IMAGE_RATIO_TOO_LOW | Face ratio is lower than the minimum ratio. | 
| FACE_TO_IMAGE_RATIO_TOO_HIGH | Face ratio is bigger than the maximum ratio. | 
| INSUFFICIENT_AREA_AROUND_THE_FACE | Insufficient area around the face in the image provided. | 
| IMAGE_TOO_BRIGHT | Image too bright. | 
| IMAGE_TOO_DARK | Image too dark. | 
| INVALID_REQUEST_BODY | Request body is invalid, '-' field is invalid. | 
| UNSPECIFIED_ERROR | An internal server error occurred. | 
{% /table %}