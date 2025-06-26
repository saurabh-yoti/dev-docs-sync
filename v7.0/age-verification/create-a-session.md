---
type: page
title: Create a session
listed: true
slug: create-a-session
description: 
index_title: Create a session
hidden: 
keywords: 
tags: 
---

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      You will need to have completed Onboarding and generated API keys. 
   </div>
   <div class="alert-links"> 
      <a href="https://developers.yoti.com/age-verification/getting-started"> Onboarding </a>
   </div>
</div>
{% /html %}

Welcome to the developer documentation for integrating with Age verification. The integrations steps are as follows:

1. Create a session
2. Launch the user view
3. Retrieve results

To begin using the age verification service a session must first be created. This is done by making a post request to the sessions endpoint.

{% code %}
{% tab language="http" %}
POST https://age.yoti.com/api/v1/sessions
{% /tab %}
{% /code %}

{% table %}
| Header | Description | 
| ---- | ---- | 
| Authorization | API Key to call the Yoti Age API. Should be sent as a Bearer token. | 
| Content-Type | application/json | 
| Yoti-SDK-Id | Your unique Yoti-Sdk-Id (uuid) | 
{% /table %}

The age verification API uses an HTTP authentication scheme called ‘bearer authentication’. This involves security tokens called ‘bearer tokens’. They are the predominant type of access token used with [OAuth 2.0](https://oauth.net/2/). A resource should interpret a bearer token as "Give the bearer of this token access". The client must send this token in the Authorization header when making requests to protected resources.

It is important that your API Key remains strictly confidential. It must be stored securely. We advise that you never commit any code containing your API Key, and never share it beyond the authorised party.

If you believe your API key has been compromised, please generate new API keys in the hub asap. 

Here you will provide which authentication method you would like, the allowed age threshold and your client preferences.

### Full example

{% code %}
{% tab language="json" %}
{
    "type": "OVER",
    "age_estimation": {
        "allowed": true,
        "threshold": 25,
        "level": "PASSIVE"
    },
    "digital_id": {
        "allowed": true,
        "threshold": 18,
        "level": "NONE"
    },
    "doc_scan": {
        "allowed": true,
        "threshold": 18,
        "authenticity": "MANUAL",
        "level": "ACTIVE"
    },
    "credit_card": {
        "allowed": false,
        "threshold": 18,
        "level": "NONE"
    },
    "mobile": {
        "allowed": false,
        "threshold": 18,
        "level": "NONE"
    },
    "ttl": 900,
    "reference_id": "over_18_example",
    "callback": {
       "auto": true,
       "url": "https://www.yoti.com"
    },
    "notification_url": "https://yourdomain.example/webhook",
    "block_biometric_consent": false,
    "cancel_url": "https://www.yoti.com"
}
{% /tab %}
{% /code %}

### Type parameter

This is where you define what preference you want to set for the age of the user.

{% table %}
| Parameter | Description | 
| ---- | ---- | 
| OVER | If the user is OVER an age threshold e.g. over 21. | 
| UNDER | If the user is UNDER an age threshold e.g. under 30. | 
| AGE | This will return the estimated AGE of the user e.g if the user is estimated to be 25, we will return 25. | 
{% /table %}

### Configuration parameter

{% table widths="0,251" %}
| Parameter | Types | Description | 
| ---- | ---- | ---- | 
| reference_id | 123 | Unique ID for each session. This is returned in the results webhook. | 
| ttl | seconds (60) | How long the session is valid for, the user will need to complete this before the ttl expires. This must be at least 60 seconds (1 minute). | 
| callback_url | [https://yourdomain.example](https://yourdomain.example/) | Where to send your user after they have finished age verification. Redirects appending the sessionId as a query parameter.\n\nYou can enable this by, `auto: true` | 
| notification_url | [https://yourdomain.example/updates](https://yourdomain.example/updates) | To state where the results of an age verification should be sent. This endpoint must be HTTPS and must accept a POST notification. | 
| block_biometric_consent | true / false | For several American states (Texas, Illinois and Washington US states) , Yoti will need the user’s consent to collect their biometric details for our liveness feature to be compliant with legislations in the US. We have implemented a toggle on / off box for users to give biometric consent before starting the age verification process. | 
| cancel_url | [https://yourdomain.example](https://yourdomain.example/) | You can specify a cancel URL, if the user opens AVS and decides that they don't want to continue then they can be taken to a specific place rather than going back in the browser.\n\nIf you would like to see how this looks please head over [here.](https://developers.yoti.com/age-verification/customisation#cancel-url) | 
{% /table %}

---

## Example response

If the request is successful and a session is generated the API will send a response in the form:

{% code %}
{% tab language="json" %}
{
  "id": "uuid",
  "expires_at": "2020-10-19T16:06:25.080Z"
}
{% /tab %}
{% /code %}

---

## Error Codes

{% table %}
| Error code | Description | 
| ---- | ---- | 
| 201 | Success | 
| 400 | Missing field in post body | 
| 401 | Missing or unknown SDK ID | 
| 403 | Incorrect API key | 
{% /table %}