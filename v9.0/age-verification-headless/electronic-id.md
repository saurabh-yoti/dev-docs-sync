---
type: page
title: Electronic ID
listed: true
slug: electronic-id
description: 
index_title: Electronic ID
hidden: 
keywords: 
tags: 
---

The Electronic ID method allows you to use various electronic ID's in order to verify a user's age.  If you are looking to perform age checks in any of the countries that we support eIDs we recommend offering these methods as an option to users. These eID schemes are widely adopted and regularly used, and therefore should lead to high success rates.

To integrate the electronic ID methods without using our UI you must go through the 3 step process detailed below:

1. Request a session
2. Launch URL
3. Retrieve Results

## Request a session

The first step is to request a session for a specific electronic ID method.

{% code %}
{% tab language="http" %}
POST https://age.yoti.com/api/v1/electronic-id/start-session
{% /tab %}
{% /code %}

{% table %}
| Header | Description | 
| ---- | ---- | 
| Authorization | API Key to call the Yoti Age API. Should be sent as a Bearer token | 
| Content-Type | application/json | 
| Yoti-SDK-Id | Your unique Yoti-Sdk-Id (uuid) | 
{% /table %}

#### Request Body

{% code %}
{% tab language="json" %}
{
  "method": "CZECH_BANK_ID",
  "return_url": "https://<YourDomain>/return",
  "enhanced_checks": true
}
{% /tab %}
{% /code %}

{% table widths="179,143" %}
| Parameter | Types | Description | 
| ---- | ---- | ---- | 
| method | String | electronic Id method:\n\n\n\n- `CZECH_BANK_ID`\n- `CZECH_MOJE_ID`\n- `POLISH_EDO_APP` | 
| return_url | String | Url that the user will be redirected towards after they complete the verification process | 
| enhanced_checks | boolean | Toggle for enhanced checks, must be set to true | 
{% /table %}

#### Example Response

{% code %}
{% tab language="json" %}
{
  "url": "string",
  "conversation_id": "string"
}
{% /tab %}
{% /code %}

{% table widths="166" %}
| Parameter | Description | 
| ---- | ---- | 
| url | The url that the user needs to be directed towards to complete the verification | 
| conversion_id | Unique Id needed to retrieve results | 
{% /table %}

---

## Launch URL

The second step in the integration process is to simply launch the url that is retrieved in the API call detailed above. The user will be directed to the relevant electronic Id method, where they will be able to complete the verification process. On completion, the user will be redirected to the "return_url" that was configured in the API call detailed above.

---

#### Retrieve Results

The final step in the integration would be to retrieve the results of the age verification. To do this a final call to our API will need to be made.

{% code %}
{% tab language="http" %}
GET https://age.yoti.com/api/v1/electronic-id/status/{conversationId}
{% /tab %}
{% /code %}

{% table %}
| Header | Description | 
| ---- | ---- | 
| Authorization | API Key to call the Yoti Age API. Should be sent as a Bearer token | 
| Content-Type | application/json | 
| Yoti-SDK-Id | Your unique Yoti-Sdk-Id (uuid) | 
{% /table %}

The conversion Id that is returned in the API call to request a session must also be used as a query parameter in this API call.

#### Example Response

{% code %}
{% tab language="json" %}
{
  "status": "COMPLETE",
  "data": {
    "fullname": "string",
    "address": "string",
    "date_of_birth": "string"
  }
}
{% /tab %}
{% /code %}

{% table widths="167" %}
| Parameter | Description | 
| ---- | ---- | 
| status | IN_PROGRESS - User has not yet completed the process.\n\n\nCOMPLETE - The session has been completed, data has successfully been returned.\n\n\nERROR - We could not provide any Data or an error occurred.\n\n\nFAIL - We have only received a partial result. | 
| data | The data of the individual who underwent the verification, including the date of birth. | 
{% /table %}