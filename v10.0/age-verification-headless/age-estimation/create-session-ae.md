---
type: page
title: Create session
listed: true
slug: create-session-ae
description: 
index_title: Create session
hidden: 
keywords: 
tags: 
---

To use Age estimation with Headless Age verification service (AVS), you will first need to create a session with `age_estimation` method enabled.

{% code %}
{% tab language="http" %}
POST https://age.yoti.com/api/v1/sessions
{% /tab %}
{% /code %}

{% table %}
| Header | Description | 
| ---- | ---- | 
| Authorization | API Key for the Yoti Age Verification API. Should be sent as 'Bearer {{API_TOKEN}}'. | 
| Content-Type | application/json | 
| Yoti-SDK-Id | Your unique Yoti-Sdk-Id (uuid) | 
{% /table %}

The age verification API uses an HTTP authentication scheme called ‘bearer authentication’. This involves security tokens called ‘bearer tokens’. They are the predominant type of access token used with [OAuth 2.0](https://oauth.net/2/). A resource should interpret a bearer token as "Give the bearer of this token access". The client must send this token in the Authorization header when making requests to protected resources.

It is important that your API Key remains strictly confidential. It must be stored securely. We advise that you never commit any code containing your API Key, and never share it beyond the authorised party.

If you believe your API key has been compromised, please generate new API keys in the hub asap.

### Request Body

{% code %}
{% tab language="json" %}
{
    "type": "OVER",
    "age_estimation": {
        "allowed": true,
        "threshold": 21,
        "level": "PASSIVE"
    },
    "ttl": 900,
    "reference_id": "over_21_example",
  	"notification_url": "https://yourdomain.example/webhook",
    "callback": {
      	"auto": false,
      	"url": "https://www.example.com"
    }
}
{% /tab %}
{% /code %}

{% table %}
| Parameter | Type | Description | 
| ---- | ---- | ---- | 
| allowed | true / false | Enable the verification method to be available for the user to use. | 
| threshold | Integer e.g. 30 | Age threshold for under/over age limits. We recommend for this threshold to be more than the age you want to set as your barrier to entry. | 
| level | NONE / PASSIVE | The level of anti-spoofing for each age verification method.\n\n\nPASSIVE enables a passive liveness test for age estimation. | 
| type | OVER / UNDER / AGE | This is where you define what preference you want to set for the age of the user. | 
| ttl | seconds (60) | How long the session is valid for, the user will need to complete this before the ttl expires. This must be at least 60 seconds (1 minute). And can't be longer than 1 month. | 
{% /table %}

---

### [Example response](https://developers.yoti.com/age-verification/create-a-session#example-response)

If the request is successful and a session is generated the API will send a response in the form:

{% code %}
{% tab language="json" %}
{
  "id": "uuid",
  "expires_at": "2020-10-19T16:06:25.080Z"
}
{% /tab %}
{% /code %}

### Error codes

{% table %}
| Error code | Description | 
| ---- | ---- | 
| 201 | Success | 
| 400 | Missing field in post body | 
| 401 | Missing or unknown SDK ID | 
| 403 | Incorrect API key | 
{% /table %}