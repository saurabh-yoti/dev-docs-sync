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
POST https://age.yoti.com/api/v1/sessions/<sessionId>/age-estimation
{% /tab %}
{% /code %}

### Headers explained

{% table widths="" %}
| Header | Description | 
| ---- | ---- | 
| Yoti-Sdk-Id | Your unique Sdk id | 
| Content-Type | multipart/form-data; boundary | 
{% /table %}

### Request Body

The request body must be sent as multipart form-data along with the relevant boundary. 

{% code %}
{% tab language="json" title="form-data" %}
{
    "image": "<base64 encoded image>",
    "biometric_consent": "<biometric_timestamp>",
    "secure_token": "<fcm_secure_object>"
}
{% /tab %}
{% /code %}

{% table widths="" %}
| Parameter | Content-Type | Type | Description | 
| ---- | ---- | ---- | ---- | 
| image | application/octet-stream | Base64 encoded image | Image of the user that the age estimation is performed on. | 
| biometric_consent | text/plain | Biometric timestamp string | Timestamp in UTC when the image of the user is captured. | 
| secure_token | text/plain | Secure Token | Payload from FCM capture returned in the `secure` field. | 
{% /table %}

### Response Body

The response body is returned with the content type of `application/json`.

#### Successful (Complete) Response

{% code %}
{% tab language="json" %}
{
  	"status": "COMPLETE"
}
{% /tab %}
{% /code %}

#### Successful (Fail) Response

{% code %}
{% tab language="json" %}
{
    "status": "FAIL"
    "attempts_remaining":5,
    "retries_depleted": false
}
{% /tab %}
{% /code %}

#### Error Response

{% code %}
{% tab language="json" %}
{
		"context": "<Context_Message>",
		"error_code": "<Error_Code>",
  	"attempts_remaining":6, // optional
    "retries_depleted": false // optional
}
{% /tab %}
{% /code %}

{% table widths="" %}
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

### Retries

It's possible to trigger a check again when a success (fail) or an error response is returned  with the same session  The pre-requisite is that the value of `attempts_remaining` is greater than zero and `retries_depleted` is not true.

To trigger the retry check, you have to make the API call again with the same request body as mentioned at the top.