---
type: page
title: Reusable Digital ID
listed: true
slug: reusable-digital-id
description: 
index_title: Reusable Digital ID
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
         <a href="https://developers.yoti.com/digital-id/overview">Full integration guide</a>
      <a target="_self" href="https://forms.gle/aRPdfj7FQav8jycq7">Feedback form</a> 
   </div>
</div>
{% /html %}

---

## Request endpoint

{% code %}
{% tab language="http" %}
POST /api/v1/qrcodes/apps/:appId
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
--url https://www.example.com//api/v1/qrcodes/apps/:appId?sdkId={sdkId}&nonce={nonce}&timestamp={timestamp} \
--header "X-Yoti-SDK: {X-Yoti-SDK}" \
--header "X-Yoti-SDK-Version: {X-Yoti-SDK-Version}" \
--header "X-Yoti-Auth-Token: {X-Yoti-Auth-Token}" \
--data '{
"callback_endpoint": "{string}",
"subject":{
 "subject_id":"{string}"
}
"policy":{
 "identity_profile_requirements":{
   "trust_framework":"UK_TFIDA",
   "scheme":{
     "type":"DBS",
     "objective":"STANDARD"
  }
 }
 "wanted_remember_me":true
}
}'
{% /tab %}
{% /code %}

{% table %}
| Parameter | Type | Description | Mandatary | 
| ---- | ---- | ---- | ---- | 
| DynamicScenarioPayload | Object | Payload to create a Yoti share token \n\n(QR code or URL/button) | Required | 
| callback_endpoint | String | Callback endpoint to return the result. Must be a valid URI path that starts with / and has less than 255 chars. | Required | 
| subject | Object | Allows to provide information \n\non the subject. _Only taken into account if policy.identity_profile_requirements defined._ | Optional | 
| subject_id | String | Allows the relying party to provide a \n\nsubject_id that will be returned in the verification report. Should not contain any personal identifiable information. | Optional | 
| policy | Object | Allows to define what is required from the \n\nuser and what is provided back to the user | Required | 
| wanted | []Object | Allows to define a list of attributes requested from the user. \n\n**_Not required_**_if identity_profile_requirements__\n\n**is specified as the system will automatically populate which identity attributes are**\n\n__required for the specific identity profile._ | Optional | 
| wanted_remember_me | Boolean | Allows to define if a unique identifier for the user is required. This is a Yoti generated random unique identifier that the user \n\n\n\nconsents to provide and is returned in the sharing receipt. It is going to be the same across all interactions between the organisation and the same user. | Optional | 
| wanted_auth_types | []Integer | Allows to define additional authentication requirements for the user at share time.\n\n**_Not required_**_if identity_profile_requirements__\n\n**is specified as the system will automatically**\n\n__determine if additional auth is required._ | Optional | 
| identity_profile_requirements | Object | Defines a required identity profile within the scope of a trust framework and scheme. | Required | 
| trust_framework | String | Defines under which trust framework\n\nthis identity profile should be verified.\n\nEnum: UK_TFIDA | Required | 
| scheme | Object | Defines which scheme this identity profile should satisfy. The scheme must be \n\nsupported by the specified trust framework otherwise the request is considered invalid. | Required | 
| type | String | Defines which scheme this identity profile should satisfy.\n\nEnum: DBS, RTW, RTR, DBS_RTW | Required | 
| objective | String | Defines the objective to be achieved for \n\n\n\nthe particular scheme.\n\nIt must be provided for those schemes where it is mandatory. Example, this is mandatory for DBS and the possible values are: ”BASIC”, “STANDARD”, “ENHANCED”. | Optional | 
{% /table %}

### Response

{% code %}
{% tab language="http" %}
{
 "qrcode": "https://code.yoti.com/forfhq3peurij4ihroiehg4jgiej",
 "ref_id": "01aa2dea-d28b-11e6-bf26-cec0c932ce01"
}
{% /tab %}
{% /code %}

{% table %}
| Parameter | Type | Mandatory | 
| ---- | ---- | ---- | 
| qrcode | String | Required | 
| ref_id | String | Required | 
{% /table %}

### Error codes

{% table %}
| Code | Description | 
| ---- | ---- | 
| 200 | Success | 
| 400 | Payload validation error or malformed request | 
| 401 | Unauthorised request (wrong key or signature) | 
| 403 | Unauthorised request (app is disabled or has no associated organisation_id) | 
| 404 | The application for provided sdk id does not exist | 
| 503 | The service is unavailable | 
{% /table %}

---

## Using Yoti SDK's

The description on how to use the above endpoint from the SDK can be found here:

- [Create button](https://developers.yoti.com/digital-id/createbutton#dynamic-qr)
- [Retrieve the profile](https://developers.yoti.com/digital-id/retrieve-the-profile)

Please read the above for a full description and understanding, below we’ll provide examples on how those requests will expose the new functionality.

{% code %}
{% tab language="javascript" %}
const dynamicPolicy = new Yoti.DynamicPolicyBuilder()
     //identityProfileRequirements is the JSON as defined in the API above
    .withIdentityProfile(identityProfileRequirements)
    .build();
{% /tab %}
{% /code %}

The policy can now be used to create a dynamic scenario:

{% code %}
{% tab language="javascript" %}
const dynamicScenario = new Yoti.DynamicScenarioBuilder()
      .withCallbackEndpoint("/your-callback")
      .withPolicy(dynamicPolicy)
      //subject is the JSON as defined in the API above
      .withSubject(subject)
      .build();
{% /tab %}
{% /code %}

The dynamicScenario can be used to get a shareURL which will be used by the Yoti scripts to generate a Yoti QR code.

{% code %}
{% tab language="javascript" %}
yotiClient.createShareUrl(dynamicScenario)
    .then((shareUrlResult) => {
     const shareURL =  shareUrlResult.getShareUrl(),
    }).catch((error) => {
      console.error(error.message);
    });
{% /tab %}
{% /code %}

---

## Response

The description on how to use the above endpoint from the SDK can be found here:

- [Retrieve the profile](https://developers.yoti.com/digital-id/retrieve-the-profile)

In case of a successful transaction, once the profile is retrieved, the identity profile report can be accessed.

{% code %}
{% tab language="javascript" %}
yotiClient.getActivityDetails(oneTimeUseToken)
  .then((activityDetails) => {
    const rememberMeId = activityDetails.getRememberMeId();
    const parentRememberMeId = activityDetails.getParentRememberMeId();
    const receiptId = activityDetails.getReceiptId();
    const timestamp = activityDetails.getTimestamp();
 
    const profile = activityDetails.getProfile();
 
    const selfieImageData = profile.getSelfie().getValue();
    
    // identityProfileReport is the JSON object containing identity assertion and
    // verification report. See API definition for field names and description.
    const identityProfileReport = profile.getIdentityProfileReport().getValue(); 
    
 
 })
{% /tab %}
{% /code %}

The identity profile report contains the verified identity details and the verification report that certifies how the identity was verified and how the verification level was achieved.

---

## User experience

There will be instances where we have exhausted all available ‘routes’ to help a user achieve compliance with the requested scheme and not been successful.  In these cases the user will not be able to complete the ‘share’, and will be shown a screen which informs them that they cannot continue with the journey in our app, and to return to the relying party to understand next steps.

We recommend that all relying parties provide some way for applicants to return to the point at which they initiated the digital ID journey and ‘flag’ that they cannot get verified with digital ID.  (It is recommended that users can only flag they have been unsuccessful after they have launched the webshare ‘start share’ QR / button at least once.)