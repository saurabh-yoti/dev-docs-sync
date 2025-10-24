---
type: page
title: Mobile
listed: true
slug: mobile
description: 
index_title: Mobile
hidden: 
keywords: 
tags: 
---

## Overview

{% synced id="mobile-avs-overview" %}
{% /synced %}

## Mobile - Headless check

## Send mobile OTP

When verifying someones age via the mobile method, you can optionally send a one time password (OTP) to the phone number that the user provides, to ensure they have access to this mobile phone. If the phone number has already been verified (i.e. through a pre-existing OTP), this step may be skipped.

{% code %}
{% tab language="http" %}
POST https://age.yoti.com/api/v1/mobile/otp
{% /tab %}
{% /code %}

{% table widths="" %}
| Header | Description | 
| ---- | ---- | 
| Authorization | API Key to call the Yoti Age API. Should be sent as a Bearer token. | 
| Content-Type | application/json | 
| Yoti-SDK-Id | Your unique Yoti-Sdk-Id (uuid) | 
{% /table %}

#### Request body

{% code %}
{% tab language="json" %}
{
   "phone_number": "phoneNumber",
   "consent_id": "Unique_ID"
}
{% /tab %}
{% /code %}

{% table widths="" %}
| Parameter | Types | Description | 
| ---- | ---- | ---- | 
| phone_number | String | This should be the target phone number to receive an OTP, including the country prefix. | 
| consent_id | String | Reference stored by the telco for each check. | 
{% /table %}

#### Example response

{% code %}
{% tab language="json" title="Success" %}
{
    "success": true
}
{% /tab %}
{% tab language="json" title="Failure" %}
{
    "message": "Unauthorised",
    "error_code": "E200008"
}
{% /tab %}
{% /code %}

## Mobile check

{% code %}
{% tab language="http" %}
POST https://age.yoti.com/api/v1/mobile/check
{% /tab %}
{% /code %}

{% table widths="" %}
| Header | Description | 
| ---- | ---- | 
| Authorization | API Key to call the Yoti Age API. Should be sent as a Bearer token. | 
| Content-Type | application/json | 
| Yoti-SDK-Id | Your unique Yoti-Sdk-Id (uuid) | 
{% /table %}

#### Request body

{% code %}
{% tab language="json" %}
{
   "phone_number": "phoneNumber",
   "consent_id": "Unique_ID",
   "otp": "OTP_Code" //optional
}
{% /tab %}
{% /code %}

{% table widths="212,0" %}
| Parameter | Types | Description | 
| ---- | ---- | ---- | 
| phone_number | String | The phone number to verify. This must include the country code prefix. | 
| consent_id | String | Reference stored by the telco for each check. | 
| otp* | String | Optional, if an OTP was requested, this can be sent to verify the recipient has received the OTP.\n\n\n\nIf the phone number is already verified, an OTP may not be required. | 
{% /table %}

#### Example response

{% code %}
{% tab language="json" title="Success" %}
{
    "method": "MOBILE",
    "type": "OVER",
    "threshold": 18,
    "age": 18,
    "result": true,
    "status": "COMPLETE",
    "evidence_id": "ef4846dd-10fa-4c1b-ba81-f9046c698c8a"
}
{% /tab %}
{% tab language="json" title="Error" %}
{
    "method": "MOBILE",
    "type": "OVER",
    "threshold": 18,
    "age": 0,
    "result": false,
    "status": "ERROR",
    "evidence_id": "26102c13-3612-4c01-bf88-43c4fd434e97"
}
{% /tab %}
{% /code %}

{% table widths="234" %}
| Field | Description | 
| ---- | ---- | 
| method | The AV method used. MOBILE is returned for mobile checks | 
| type | Dictates the threshold type. For mobile checks only OVER is returned | 
| threshold | The age threshold that has been met | 
| age | The age threshold that has been met | 
| result | Returns true if the threshold (18) has been met. Returns false if not met, or on error | 
| status | COMPLETE - The phone number has been associated with an Over 18 individual\n\n\nERROR - We could not provide an age result, because we didn't have enough info associated with that phone number\n\n\nFAIL - The phone number has been associated with an Under 18 individual | 
| evidence_id | The Evidence ID can be re-shared with Yoti to provide evidence that a check of a mobile phone number was performed. The mobile phone number  or associated personal information is not stored by Yoti, this can never be retrieved. Yoti will be able to confirm that a check took place at a specific time, the processing steps and result of the check | 
{% /table %}

## Error codes

{% table widths="" %}
| Error Code | Description | 
| ---- | ---- | 
| E200001 | Internal server error | 
| E200003 | Unable to get a response from requesting OTP | 
| E200006 | Invalid country code | 
| E200007 | Bad request | 
| E200008 | Unauthorised | 
| E200009 | Not allowed | 
| E200010 | Not found | 
| E200011 | Invalid message template | 
| E200012 | Phone number not whitelisted | 
| E200013 | Error received from supplier | 
{% /table %}