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
| Authorization | API Key to call the Yoti Age API. | 
| Content-Type | application/json | 
| Yoti-SDK-Id | Your unique Yoti-Sdk-Id (uuid) | 
{% /table %}

The age verification API uses an HTTP authentication scheme called ‘bearer authentication’. This involves security tokens called ‘bearer tokens’. They are the predominant type of access token used with [OAuth 2.0](https://oauth.net/2/). A resource should interpret a bearer token as "Give the bearer of this token access". The client must send this token in the Authorization header when making requests to protected resources.

It is important that your API Key remains strictly confidential. It must be stored securely. We advise that you never commit any code containing your API Key, and never share it beyond the authorised party.

If you believe your API key has been compromised, please generate new API keys in the hub asap. 

Here you will provide which authentication method you would like, the allowed age threshold and your client preferences.

{% code %}
{% tab language="json" %}
{
    "type": "OVER",
    "age_estimation": {
        "allowed": true,
        "threshold": 20,
        "level": "PASSIVE"

    },
    "digital_id": {
        "allowed": true,
        "threshold": 18,
        "level": "NONE"
    },
    "doc_scan": {
        "allowed": true,
        "threshold": 24,
        "authenticity": "OFF",
        "level": "NONE"
    },
    "credit_card": {
        "allowed": true,
        "threshold": 24,
        "level": "NONE"
    },

    "mobile": {
        "allowed": true,
        "threshold": 24,
        "level": "NONE"
    },

    "ttl": 900,
    "reference_id": "over_18_example",
    "callback_url": "https://yoti.com",
    "notification_url": "https://yourdomain.example/webhook",
    "block_biometric_consent": true

}
{% /tab %}
{% /code %}

### Type parameter

This is where you define what preference you want to set for the age of the user.

{% table %}
| Type parameter | Description | 
| ---- | ---- | 
| OVER | If the user is OVER an age threshold e.g. over 21. | 
| UNDER | If the user is UNDER an age threshold e.g. under 30. | 
| AGE | If the user is the AGE e.g if the user is 25. | 
{% /table %}

### Age estimation parameter

If you wish to enable the Age estimation service as an option to perform an age verification service.

{% table %}
| Parameter | Types | Description | 
| ---- | ---- | ---- | 
| allowed | true / false | Enable the verification method to be available for the user to use. | 
| threshold | Integer e.g. 30 | Age threshold for under/over age limits. We recommend for this threshold to be more than the age you want to set as your barrier to entry. | 
| level | NONE PASSIVE ACTIVE | The level of anti-spoofing for each age verification method.\n\n\nPASSIVE enables a passive liveness test for age estimation. Passive liveness looks at the texture, depth and edges of a person’s face and their surroundings for signs of spoofing and requires no movement from the user.\n\n\n\nACTIVE enables an active liveness test for age estimation. Active anti-spoofing requires the user to simply move their phone towards their face – our technology works in the background to scan their face and determine whether they’re a real person. | 
{% /table %}

### Digital ID parameter

To enable the Digital ID as an option to perform an age verification service.

{% table %}
| Parameter | Types | Description | 
| ---- | ---- | ---- | 
| allowed | true / false | Enable the verification method to be available for the user to use. | 
| threshold | Integer e.g. 30 | Age threshold for under/over age limits. We recommend this to be the exact age of the threshold you want to cover. | 
| level | NONE | The level of anti-spoofing for each age verification method. Yoti app currently strong levels of anti-spoofing, the user must either use Face ID / a PIN to get into the Yoti app. | 
{% /table %}

### Doc scan parameter

If you wish to enable the Identity verification service as an option to perform an age verification service. This solution may take longer to verify your users. Yoti extracts the date of birth from the ID document. 

{% table widths="107,0" %}
| Parameter | Types | Description | 
| ---- | ---- | ---- | 
| allowed | true / false | Enable the verification method to be available for the user to use. | 
| threshold | Integer e.g. 30 | Age threshold for under/over age limits. We recommend this to be the exact age of the threshold you want to cover. | 
| authenticity | OFF / ON | If you would like to enable this ON, Yoti will perform an identity verification check on the document.  For more information on the types of checks please head [here](/identity-verification/document). | 
| level | NONE / ACTIVE | The level of anti-spoofing for each age verification method.\n\n\nACTIVE enables an active liveness test and face match for doc scan. | 
{% /table %}

### Credit card parameter

If you wish to enable the Credit card service as an option to perform an age verification service.

{% table %}
| Parameter | Types | Description | 
| ---- | ---- | ---- | 
| allowed | true / false | Enable the verification method to be available for the user to use. | 
| threshold | Integer e.g. 30 | Age threshold for under/over age limits. We recommend this to be the exact age of the threshold you want to cover. | 
| level | NONE | The level of anti-spoofing for each age verification method. | 
{% /table %}

### Mobile parameter

If you wish to enable the mobile service as an option to perform an age verification service.

{% table %}
| Parameter | Types | Description | 
| ---- | ---- | ---- | 
| allowed | true / false | Enable the verification method to be available for the user to use. | 
| threshold | Integer e.g. 30 | Age threshold for under/over age limits. We recommend this to be the exact age of the threshold you want to cover. | 
| level | NONE | The level of anti-spoofing for each age verification method. | 
{% /table %}

### Configuration parameter

{% table widths="0,251" %}
| Parameter | Types | Description | 
| ---- | ---- | ---- | 
| reference id | 123 | Unique ID for each session. This is returned in the results webhook. | 
| ttl | seconds (60) | How long the session is valid for, the user will need to complete this before the ttl expires. This must be at least 60 seconds (1 minute). | 
| callback URL | [https://yourdomain.example](https://yourdomain.example/) | Where to send your user after they have finished age verification. Redirects appending the sessionId as a query parameter. | 
| notification URL | [https://yourdomain.example/updates](https://yourdomain.example/updates) | To state where the results of an age verification should be sent. This endpoint must be HTTPS and must accept a POST notification. | 
| block_biometric_consent | true / false | For several American states (Texas, Illinois and Washington US states) , Yoti will need the user’s consent to collect their biometric details for our liveness feature to be compliant with legislations in the US. We have implemented a toggle on / off box for users to give biometric consent before starting the age verification process. | 
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