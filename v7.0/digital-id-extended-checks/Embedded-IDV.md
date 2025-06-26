---
type: page
title: Embedded IDV
listed: true
slug: Embedded-IDV
description: 
index_title: Embedded IDV
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
       For the purposes of explaining the request and response format, the below details the API and provides SDK examples in Javascript.
   </div>
   <div class="alert-links"> 
         <a href="https://developers.yoti.com/identity-verification/overview">Full integration guide</a>
      <a target="_self" href="https://forms.gle/aRPdfj7FQav8jycq7">Feedback form</a> 
   </div>
</div>
{% /html %}

---

## Request endpoint

{% code %}
{% tab language="http" %}
POST /identity-profile/sessions
{% /tab %}
{% /code %}

### Header

{% table %}
| Key | Description | 
| ---- | ---- | 
| Authentication | Yoti-Auth-Token | 
{% /table %}

### Query string

{% table %}
| Query | Type | Mandatory | 
| ---- | ---- | ---- | 
| sdkID | string | Required | 
| nonce | string | Required | 
| timestamp | string | Required | 
{% /table %}

## Request body

{% code %}
{% tab language="http" %}
curl --request POST \
--url https://www.example.com//identity-profile/sessions?sdkId={sdkId}&nonce={nonce}&timestamp={timestamp} \
--header "X-Yoti-SDK: {X-Yoti-SDK}" \
--header "X-Yoti-SDK-Version: {X-Yoti-SDK-Version}" \
--header "X-Yoti-Auth-Token: {X-Yoti-Auth-Token}" \
--data '{
"client_session_token_ttl": 600,
"resources_ttl": 87000,
"subject":{
 "subject_id":"{string}"
}
"identity_profile_requirements":{
 "trust_framework":"UK_TFIDA",
 "scheme":{
    "type":"DBS",
    "objective":"STANDARD"
 }
}
"block_biometric_consent": true,
"notifications": {
 "endpoint": "{string}",
 "topics": [
  "SESSION_COMPLETION",
 ],
 "auth_token": "{string}",
 "auth_type": "{string}"
},
"sdk_config": {
 "primary_colour": "#2d9fff",
 "secondary_colour": "#FFFFFF",
 "font_colour": "#FFFFFF",
 "locale": "en-GB",
 "preset_issuing_country": "GBR",
 "success_url": "{string}",
 "error_url": "{string}",
 "privacy_policy_url": "{string}"
 },
}
}'
{% /tab %}
{% /code %}

{% table %}
| Parameter | Type | Description | Mandatary | 
| ---- | ---- | ---- | ---- | 
| CreateSessionPayload | Object | Create Session Payload |  | 
| client_session_token_ttl | Integer | Number of seconds for the user to complete the whole flow.\n\n\n\nDefault: 600 | Optional | 
| resources_ttl | Integer | Retention period for uploaded documents/images in number of seconds.\n\n\n\nminimum: 86700\n\n\n\nDefault: 87000 | Optional | 
| subject | Object | Allows to provide information \n\non the subject. | Optional | 
| subject_id | String | Allows to track the same user across multiple sessions. Should not contain any personal identifiable information. | Optional | 
| policy | Object | Allows to define what is required from the \n\nuser and what is provided back to the user | Required | 
| identity_profile_requirements | Object | Defines a required identity profile within the scope of a trust framework and scheme. | Required | 
| trust_framework | String | Defines under which trust framework\n\nthis identity profile should be verified.\n\nEnum: UK_TFIDA | Required | 
| scheme | Object | Defines which scheme this identity profile should satisfy. The scheme must be \n\nsupported by the specified trust framework otherwise the request is considered invalid. | Required | 
| type | String | Defines which scheme this identity profile should satisfy.\n\nEnum: DBS, RTW, RTR, DBS_RTW | Required | 
| objective | String | Defines the objective to be achieved for \n\n\n\nthe particular scheme.\n\nIt must be provided for those schemes where it is mandatory. Example, this is mandatory for DBS and the possible values are: ”BASIC”, “STANDARD”, “ENHANCED”. | Optional | 
| block_biometric_consent | Boolean | Allows the relying business to block the collection of biometric consent. | Optional | 
| notifications | Object |  | Optional | 
| endpoint | String | POST endpoint required. Update notifications are sent to this endpoint based on the selected subscription topics\n\npattern: ^https://.+$ | Optional | 
| topics | []string |  | Optional | 
| auth_token | String | If provided, Yoti will send this as a base64 encoded value for the Authorization header in the notifications | Optional | 
| auth_type | String | Determines the type of auth header to include in outbound notifications. Defaults to BASIC\n\nEnum: BASIC,BEARER | Optional | 
| sdk_config | Object |  | Optional | 
| primary_colour | String | pattern: ^#([A-Fa-f0-9]{6}&#124;[A-Fa-f0-9]{3})$ | Optional | 
| secondary_colour | String | pattern: ^#([A-Fa-f0-9]{6}&#124;[A-Fa-f0-9]{3})$ | Optional | 
| font_colour | String | pattern: ^#([A-Fa-f0-9]{6}&#124;[A-Fa-f0-9]{3})$ | Optional | 
| locale | String | pattern: ^(?!\s*$).+ | Optional | 
| preset_issuing_country | String |  | Optional | 
| success_url | String |  | Optional | 
| error_url | String |  | Optional | 
| privacy_policy_url | String |  | Optional | 
{% /table %}

### Response

{% code %}
{% tab language="http" %}
{
 "client_session_token_ttl": 599,
 "client_session_token": "{string}",
 "session_id": "{string}"
}
{% /tab %}
{% /code %}

{% table widths="0,151,0" %}
| Parameter | Type | Description | Mandatory | 
| ---- | ---- | ---- | ---- | 
| client_session_token_ttl | Integer | Remaining time the user has to complete the session | Required | 
| client_session_token | String | Client token to be used for auth of any calls made by client for this session | Required | 
| session_id | String | Identifier for the session | Required | 
{% /table %}

### Error codes

{% table %}
| Code | Description | 
| ---- | ---- | 
| 200 | Success | 
| 400 | Payload validation error or malformed request | 
| 401 | Unauthorised request (wrong key or signature) | 
| 403 | Unauthorised request (app is disabled or has no associated organisation_id) | 
| 404 | The application for provided SDK ID does not exist | 
| 503 | The service is unavailable | 
{% /table %}

---

## Retrieve the profile

Retrieve the identity profile session

{% code %}
{% tab language="http" %}
GET /identity-profile/sessions/{sessionId}
{% /tab %}
{% /code %}

{% table %}
| Key | Description | 
| ---- | ---- | 
| Authentication | Yoti-Auth-Token | 
{% /table %}

{% table %}
| Path | Type | Mandatory | 
| ---- | ---- | ---- | 
| sessionID | String | Required | 
{% /table %}

{% table %}
| Query | Type | Mandatory | 
| ---- | ---- | ---- | 
| sdkID | string | Required | 
| nonce | string | Required | 
| timestamp | string | Required | 
{% /table %}

{% code %}
{% tab language="http" %}
curl --request GET \
--url https://www.example.com//sessions/{sessionId}?sdkId={sdkId}&timestamp={timestamp}&nonce={nonce} \
--header "X-Yoti-Auth-Token: {X-Yoti-Auth-Token}"
{% /tab %}
{% /code %}

{% table %}
| Code | Description | 
| ---- | ---- | 
| 200 | Success | 
| 400 | Payload validation error or malformed request | 
| 401 | Unauthorised request (wrong key or signature) | 
| 404 | Session or App not found | 
{% /table %}

### Response

In case of a successful transaction, once the profile is retrieved, the identity profile report can be accessed.

The identity profile report contains the verified identity details and the verification report that certifies how the identity was verified and how the verification level was achieved.

{% table widths="0,108,552" %}
| Parameter | Type | Description | Mandatary | 
| ---- | ---- | ---- | ---- | 
| IdentityProfileSessionResponse | Object | Create Session Payload | Required | 
| session_id | String |  | Required | 
| client_session_token_ttl | Integer | Remaining time the user has to complete the session. | Optional | 
| biometric_consent | String | Collected biometric consent. | Optional | 
| state | String | The current state of the session\n\nEnum: ONGOING,COMPLETED,EXPIRED | Required | 
| client_session_token | String | Client token to be used for auth of any calls made by client for this session. | Optional | 
| resources | Object | Collection of all resources created.\n\n_For full description please refer to__\n\n_[_https://developers.yoti.com/identity-verification/results_](https://developers.yoti.com/identity-verification/results)_and_[_https://developers.yoti.com/yoti-identity-verification-public-api/ref#retrievetheentiresession_](https://developers.yoti.com/yoti-identity-verification-public-api/ref#retrievetheentiresession)_._ | Required | 
| checks | []Object | List of all checks performed.\n\n_For full description please refer to__\n\n_[_https://developers.yoti.com/identity-verification/results_](https://developers.yoti.com/identity-verification/results)_and_[_https://developers.yoti.com/yoti-identity-verification-public-api/ref#retrievetheentiresession_](https://developers.yoti.com/yoti-identity-verification-public-api/ref#retrievetheentiresession)_._ | Required | 
| identity_profile | Object | Identity profile will be available when the session is completed | Optional | 
| subject_id | String | Subject identifier provided by the RP at\n\nsession creation time. | Optional | 
| result | String | Done means the identity could be verified and the identity profile report provided.\n\nAborted means the user could not be verified and no identity profile report was\n\n\n\nproduced, all the resources and checks\n\n\n\nwill still be available.\n\nEnum: DONE, ABORTED | Required | 
| failure_reason | Object | In case of _result:__ABORTED,_ failure_reason will provide the reason why. | Optional | 
| reason_code | String | Reason code. \n\nSome examples are: MANDATORY_DOCUMENT_COULD_NOT_BE_PROVIDED, FRAUD_DETECTED, COULD_NOT_VERIFY_ADDRESS,\n\n\n\nUNABLE_TO_VALIDATE_DOCUMENT. | Required | 
| identity_profile_report | Object | The identity profile report media contains the identity attributes and the verification \n\nreport that certifies the achieved verification level. | Optional | 
| trust_framework | String | Defines under which trust framework\n\nthis identity was verified.\n\n\n\nAs defined at session creation time.\n\nEnum: UK_TFIDA | Required | 
| schemes_compliance | []Object | Defines which schemes (of the requested ones) this identity profile satisfies. | Required | 
| scheme | Object | Scheme defines the identity scheme. | Required | 
| requirements_met | Boolean | Asserts whether the identity scheme requirements were met or not. | Required | 
| requirements_not_met_info | String | Provides info on why the scheme requirements were not met. | Required | 
| media | Object | Full identity profile report provided \n\nas a JSON media. | Required | 
| created | String | Uses the ISO8601 standard representation of date times | Required | 
| last_updated | String | Uses the ISO8601 standard representation of date times | Required | 
| id | String | Identifier to be used to fetch this media. | Required | 
| type | String | JSON\n\nEnum: IMAGE,JSON,BINARY | Required | 
{% /table %}

---

Given the identity_profile_report.media  the relying party can now proceed with retrieving it.

Example of retrieving a JSON media using the Yoti SDKs can be found [here](https://developers.yoti.com/identity-verification/results#retrieve-supplementary-documents.).

Definition of the GET media endpoint can be found [here](https://developers.yoti.com/yoti-identity-verification-public-api/ref#retrievemediacontent.).

##