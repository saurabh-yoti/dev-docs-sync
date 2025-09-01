---
type: page
title: Social security number
listed: true
slug: social-security-number
description: 
index_title: Social security number
hidden: 
keywords: 
tags: 
---

Yoti offers the additional method of using a social security number to verify a users age. This check is only available to individuals from the USA that have a social security number.

The Social security number method checks that the basic identity details of a user can be matched to an known social security number in order to verify a user’s age. Yoti will send the user’s details including their social security number to one of our data providers. Once the check is complete, the provider confirms the social security number can be linked to the validation identity which is then used to determine if the user is over the age threshold.

We never store or share the user’s details with anyone other than the provider.

{% badge type="error" text="Important:" /%} Please contact Yoti before enabling this method.

{% callout type="info" title="Info" %}
The social security number check requires provisioning through Yoti. Please get in touch through [support.yoti.com](https://support.yoti.com/yotisupport/s/contactsupport) if interested in using this solution
{% /callout %}

## Endpoint

The API endpoint to request the SSN check for age:

{% code %}
{% tab language="http" %}
POST https://age.yoti.com/api/v1/social-security-number/check
{% /tab %}
{% /code %}

## Authentication & Headers

The HTTP headers for the API request:

{% table widths="" %}
| Header | Description | 
| ---- | ---- | 
| Authorization | API Key to call the Yoti Age API. Should be sent as a 'Bearer {{API_TOKEN}}'. | 
| Content-Type | application/json | 
| Yoti-Sdk-Id | Your unique Yoti-Sdk-Id (uuid) | 
{% /table %}

## Request Payload

{% callout type="info" title="Info" %}
You should inform the user of this check in advance
{% /callout %}

The Social Security number can either be the full SSN or the last four digits. Both examples are shown below.

{% badge type="error" text="Scope:" /%} A scope of **address** is required to use this check. This can be enabled through the Yoti Hub in the services section under your API key.

The JSON structure for the API request (payload):

{% code %}
{% tab language="json" title="Full SSN" %}
{
  "type": "OVER", // optional
  "threshold": 18, // optional -> defaults to 18
  "first_name": "John",
  "last_name": "Doe",
  "zip_code": "123456",
  "social_security_number": "333-33-3333",
  "date_of_birth": "05/25/1984",
  "phone_number": "phone number",
  "street": "street name"
}
{% /tab %}
{% tab language="json" title="Last 4 Digits" %}
{
  "type": "OVER", // optional
  "threshold": 18, // optional -> defaults to 18
  "first_name": "John",
  "last_name": "Doe",
  "zip_code": "123456",
  "social_security_number": "3333",
  "date_of_birth": "05/25/1984",
  "phone_number": "phone number",
  "street": "street name"
}
{% /tab %}
{% /code %}

{% table widths="" %}
| Field | Value | Description | 
| ---- | ---- | ---- | 
| type | OVER | Only 'OVER' is supported | 
| threshold | number | Defaults to 18 | 
| first_name | string | The first name of the user | 
| last_name | string | The last name of the user | 
| zip_code | string | User zip code | 
| social_security_number | string | User SSN | 
| date_of_birth | string (dob) | User DOB | 
| phone_number | string | The user phone number | 
| street | string | The user street name | 
{% /table %}

## Example Response

The JSON structure for the API response:

{% code %}
{% tab language="json" %}
{
  "transaction_id": "<some uuid>",
  "status": "<COMPLETE|ERROR|INSUFFICIENT_DATA>",
  "result": false|true, // <- deprecated
  "age": 0|18,
  "method": "SOCIAL_SECURITY_NUMBER",
  "type": "OVER"
}
{% /tab %}
{% /code %}

{% table widths="" %}
| Field | Description | 
| ---- | ---- | 
| transaction_id | Unique ID related to the request check being performed. | 
| type | The condition for the age check (Over threshold) | 
| status | COMPLETE - The SSN was verified to be over the threshold\n\n\nERROR - No match found for the check\n\n\nINSUFFICIENT_DATA - No match found for the check (this will eventually replace the ERROR state) | 
| result | Returns true if the threshold (18) has been met. Returns false if not met, or on error. The result flag will eventually be deprecated so we recommend looking at the Status to determine the outcome. | 
| age | The threshold of the check (18) | 
| method | The method used. This should return as Social Security Number | 
{% /table %}