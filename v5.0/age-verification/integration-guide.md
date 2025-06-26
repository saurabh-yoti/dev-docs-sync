---
type: page
title: Integration guide
listed: true
slug: integration-guide
description: 
index_title: Integration guide
hidden: 
keywords: 
tags: 
---

Welcome to the developer documentation for integrating with Age verification. The integrations steps are as follows:

1. Create a session
2. Launch the user view
3. Retrieve results

---

## Create a session

To begin using the age verification service a session must first be created. This is done by making a post request to the sessions endpoint.

{% code %}
{% tab language="http" %}
POST https://age.yoti.com/api/v1/sessions
{% /tab %}
{% /code %}

{% table %}
| Header | Description | 
| ---- | ---- | 
| Authorization | API Key to call the Yoti Age API. This must be sent as a bearer token | 
| Content-Type | application/json | 
| Yoti-SDK-Id | Your unique Yoti-Sdk-Id (uuid) | 
{% /table %}

The age verification API uses an HTTP authentication scheme called ‘bearer authentication’. This involves security tokens called ‘bearer tokens’. They are the predominant type of access token used with [OAuth 2.0](https://oauth.net/2/). A resource should interpret a bearer token as "Give the bearer of this token access". The client must send this token in the Authorization header when making requests to protected resources.

It is important that your API Key remains strictly confidential. It must be stored securely. We advise that you never commit any code containing your API Key, and never share it beyond the authorised party.

If you believe your API key has been compromised, please contact us as soon as possible. This can be done through your account manager or via our support desk by emailing[ clientsupport@yoti.com.](mailto:clientsupport@yoti.com)

Here you will provide which authentication method you would like, the allowed age threshold and your client preferences.

{% code %}
{% tab language="json" %}
{
    "type": "OVER",
    "digital_id": {
        "allowed": true,
        "threshold": 19,
        "level": "NONE"
    },
    "age_estimation": {
        "allowed": true,
        "threshold": 30,
        "level": "NONE"
    },
    "doc_scan": {
        "allowed": true,
        "threshold": 25,
        "level": "NONE"
    },
    "reference_id": "123123",
    "ttl": 300000000,
    "callback_url": "https://yourdomain.example",
    "notification_url": "https://yourdomain.example/updates"
}
{% /tab %}
{% /code %}

{% table widths="0,251" %}
| Parameter | Types | Description | 
| ---- | ---- | ---- | 
| Type | OVER / UNDER / AGE | This is where you define what preference you want to set for the age of the user. \n\n\n\nIf the user is OVER an age threshold e.g. over 21.\n\n\nIf the user is UNDER an age threshold e.g. under 30.\n\n\nIf the user is the AGE e.g if the user is 25. | 
| digital_id | digital_id | If you wish to enable the Digital ID as an option to perform an age verification service. | 
| age_estimation | age_estimation | If you wish to enable the Age estimation service as an option to perform an age verification service. | 
| doc_scan | doc_scan | If you wish to enable the Identity verification service as an option to perform an age verification service. This solution may take longer to verify your users. | 
| allowed | true / false | Whether you want the verification method to be available for the user to use. | 
| threshold | Integer e.g. 30 | Age threshold for under/over age limits. | 
| level | NONE / ACTIVE / MY_FACE | The level of anti-spoofing for each age verification method.\n\n\nACTIVE enables an active liveness test and face match for doc scan. \n\nEnables an active liveness test for age estimation.\n\n\n\nMY_FACE enables a passive liveness test for age estimation. | 
| reference id | 123 | Unique ID for each session. This is returned in the results webhook. | 
| ttl | seconds (60) | How long the session is valid for, the user will need to complete this before the ttl expires. This must be at least 60 seconds (1 minute). | 
| callback URL | [https://yourdomain.example](https://yourdomain.example/) | Where to send your user after they have finished age verification. Redirects appending the sessionId as a query parameter. | 
| notification URL | [https://yourdomain.example/updates](https://yourdomain.example/updates) | To state where the results of an age verification should be sent. This endpoint must be HTTPS and must accept a POST notification. | 
| block_biometric_consent | true / false | For several American states (Texas, Illinois and Washington US states) , Yoti will need the user’s consent to collect their biometric details for our liveness feature to be compliant with legislations in the US. We have implemented a toggle on / off box for users to give biometric consent before starting the age verification process. | 
{% /table %}

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

## Error Codes

{% table %}
| Error code | Description | 
| ---- | ---- | 
| 201 | Success | 
| 400 | Missing field in post body | 
| 401 | Missing or unknown SDK ID | 
| 403 | Incorrect API key | 
{% /table %}

## Examples

Please see examples for different scenarios.

{% code %}
{% tab language="json" title="Over 18" %}
{
  "type": "OVER",
  "age_estimation": {
    "allowed": true,
    "threshold": 18,
    "level": "MY_FACE"
  },
  "digital_id": {
    "allowed": true,
    "threshold": 18,
    "level": "NONE"
  },
  "doc_scan": {
    "allowed": true,
    "threshold": 18,
    "level": "ACTIVE"
  },
  "ttl": 900,
  "reference_id": "over_18_example",
  "callback_url": "https://yourdomain.example/account/profile",
  "notification_url": "https://yourdomain.example/webhook"
}
{% /tab %}
{% tab language="json" title="Over 16" %}
{
  "type": "OVER",
  "age_estimation": {
    "allowed": true,
    "threshold": 16,
    "level": "MY_FACE"
  },
  "digital_id": {
    "allowed": false,
    "threshold": 16,
    "level": "NONE"
  },
  "doc_scan": {
    "allowed": true,
    "threshold": 16,
    "level": "ACTIVE"
  },
  "ttl": 900,
  "reference_id": "over_16_example",
  "callback_url": "https://yourdomain.example/account/profile",
  "notification_url": "https://yourdomain.example/webhook"
}
{% /tab %}
{% tab language="json" title="Exact Age" %}
{
  "type": "AGE",
  "age_estimation": {
    "allowed": true,
    "threshold": 13,
    "level": "MY_FACE"
  },
  "digital_id": {
    "allowed": true,
    "threshold": 13,
    "level": "NONE"
  },
  "doc_scan": {
    "allowed": true,
    "threshold": 13,
    "level": "ACTIVE"
  },
  "ttl": 900,
  "reference_id": "exact_age_example",
  "callback_url": "https://yourdomain.example/account/profile",
  "notification_url": "https://yourdomain.example/webhook"
}
{% /tab %}
{% /code %}