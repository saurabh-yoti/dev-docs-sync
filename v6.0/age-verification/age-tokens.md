---
type: page
title: Age Tokens
listed: true
slug: age-tokens
description: 
index_title: Age Tokens
hidden: 
keywords: 
tags: 
---

When someone uses the portal to prove their age, an age token is added to their browser. 

This acts as a digital proof that they’ve been age checked by Yoti, and lets them freely access your site without having to prove their age every time.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1632336765/v2_2762/fgpmytyncxtc12vgeofj.png" caption="Age token" mode="responsive" height="414" width="1226" %}
{% /image %}

Tokens are flexible and are accepted entirely at the discretion of the integrating party. You can define your own criteria for what type of age tokens you accept, depending on your regulatory requirements.

When the user lands on your site there will be a token request, a check is performed to see if the user has an age claim that matches your requirements.

If a user doesn’t have a token that meets the requirements, they’ll be sent to your age portal to prove their age again. If a claim is present a record of the claim's use is made and both the claim and receipt is sent to you. You can then:

- Verify a signature in the claim, proving it was issued by a legitimate Age Provider.
- Confirm that the receipt is unique and that the claim is not being re-used.

An age token will open the ability to:

{% table %}
| Feature | Description | 
| ---- | ---- | 
| Seamless access to participating websites | When the user visits another site that’s integrated with this service, that site will check for an age token to make sure they’re old enough to enter. \n\n\n\nIf the token meets the requirements of the website, they can enter without having to prove their age again | 
| Authenticate new browsers and devices | To access your site on another device, users can create an age account and pass their tokens across to a new browser. | 
{% /table %}

Integrating age tokens into the Age verification flow can be broken down into the following steps:

1. Create an Age Token rule.
2. Request a Client Key
3. Request Token Check

{% badge type="info" text="Hint" /%} An Age Token will only be issued if a user successfully passes an AV flow.

---

## Create an Age Token rule

By creating an age token rule, you define the exact AV requirements the user should meet from an existing flow.

{% code %}
{% tab language="http" %}
POST https://age.yoti.com/api/v1/rules
{% /tab %}
{% /code %}

{% table %}
| Header | Description | 
| ---- | ---- | 
| Authorization | API Key to call the Yoti Age API. This must be sent as a Bearer token | 
| Yoti-Sdk-Id | Your unique Yoti-Sdk-Id (UUID) | 
{% /table %}

The rule body is a mirror of the payload to [Create an AV session](/age-verification/integration-guide). The rule is granular and will only be fulfilled if the AV method, threshold and anti spoofing levels are all met.

{% badge type="info" text="Hint" /%} It's advised to match your Age Token rule to your create session payload to ensure the user has met your own requirements.

{% code %}
{% tab language="json" %}
{
  "ttl": 31540000, // value is in seconds, 31540000 = 1 year,
  "type": "OVER",
  "age_estimation": {
    "allowed": true,
    "threshold": 22,
    "level": "MY_FACE"
  },
  "doc_scan": {
    "allowed": true,
    "threshold": 18,
    "authenticity": "AUTO",
    "level": "ACTIVE"
  },
  "digital_id": {
    "allowed": true,
    "threshold": 18
  }
}
{% /tab %}
{% /code %}

The returned Rule ID must be retained as it will be used for all future checks.

#### Responses

{% code %}
{% tab language="http" title="Success" %}
Success responses
statusCode: 201
body: { "id": "<rule id>" }
{% /tab %}
{% /code %}

{% code %}
{% tab language="http" title="Error" %}
Error responses
statusCode: 4xx - 5xx
body: { "error_message": "<string>", "error_code": "<string>"}
{% /tab %}
{% /code %}

---

## Request a Client Key

For each new user session, a client key must be requested prior to performing an age token check. This prevents un-registered sites requesting age tokens from users.

{% code %}
{% tab language="http" %}
POST https://age.yoti.com/api/v1/client-key
{% /tab %}
{% /code %}

{% table %}
| Header | Description | 
| ---- | ---- | 
| Authorization | API Key to call the Yoti Age API. This must be sent as a Bearer token | 
| Yoti-Sdk-Id | Your unique Yoti-Sdk-Id (UUID) | 
{% /table %}

#### Body

{% code %}
{% tab language="json" %}
{
  "redirect_url": "https://someurl.com/"
}
{% /tab %}
{% /code %}

#### Responses

{% code %}
{% tab language="http" title="Success" %}
Success response
statusCode: 200
body: { "id": "<string>", "client_key": "<string>" }
{% /tab %}
{% /code %}

{% code %}
{% tab language="http" title="Error" %}
Error responses
statusCode: 4xx - 5xx
body: { "error_message": "<string>", "error_code": "<string>"}
{% /tab %}
{% /code %}

---

## Request Token Check

The client’s device (browser) requests Yoti provides proof of an age token check.

{% code %}
{% tab language="http" %}
GET https://age.yoti.com/api/v1/credentials?sdkId=<sdkId>&ruleId=<ruleId>&clientId=<id>&clientKey=<client_key>&referenceId=<somereferenceid>&returnUrl=<encodedUriComponent_of_where_the_user_should_be returned>
{% /tab %}
{% /code %}

{% table %}
| Parameter | Description | 
| ---- | ---- | 
| sdkId | Your Yoti SdkId | 
| ruleId | The rule ID returned from creating an age token rule | 
| clientId | The id returned from requesting a client key | 
| clientKey | The client_key returned from requesting a client key | 
| referenceId | A reference Id, can be any string | 
| returnUrl | This should be a page within your control. The user will be redirected with a query parameter of either **error** or **claim**, depending on the result of the Age Token check. | 
{% /table %}

### Return URL states explained.

The two states are described below:

{% table %}
| State | Description | 
| ---- | ---- | 
| Error | This means the user does not have an age token. The value is base64 encoded. Decoding the value will provide an error code and context to explain why no age token was found. | 
| Claim | This means the user does have an age token. The value is base64 encoded. Decoding the value will provide a json object of the claim, including a signature in the proof segment, the original reference id and the rule id used. | 
{% /table %}

---

## Verify a claim

If the user does have an age token complete the following: 

1. Make sure the referenceId has not been returned by a different user.
2. Validate the `credentialProof.signature` has been generated using Yoti Age’s public key.
    1. Base64 decode the signature to bytes
    2. Create msg that consists of 
        1. `claim.reference_id|id|issuance_date|claim.rule_id|claim.evidence_id|claim.method`

    3. Convert the msg to bytes
    4. Hash the message using SHA256
    5. Use the public key of [age.yoti.com](http://age.yoti.com/) to compare the message hash to the decoded signature
        1. If the values are equal, this is a valid response

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
        The client’s device needs to have a session with Yoti Age. If no session is present the subsequent request will return a E400003 error.

To obtain a session with Yoti Age complete an age verification, in the response to any age verification there will be two ‘Set-Cookie’ headers. The values of these headers must be included in requests to /api/v1/credentials. Typically this happens when you navigate to the url in a browser.
    </div>
    <div class="alert-links"> 

   </div>
</div>
{% /html %}

---

## Token Error Codes

{% table %}
| Error Code | Description | Resolution | 
| ---- | ---- | ---- | 
| E400002 | The current user does not have any valid tokens | User will have to verify their age using an appropriate method | 
| E400003 | No cookie found to determine whether user has an age token | User needs to verify their age, using an appropriate method and then request their token in the same browser session. | 
| E400004 | The origin header is missing from the request to token-api | Use the browser to request the token include the origin header in your http client’s request | 
| E400005 | Bad request | A missing or malformed request was sent. Check the context field in the error response for details. | 
| E800002 | Bad request | A missing or malformed request was sent. Check the context field in the error response for details. | 
| E800003 | The credentials provided have not been verified | Check your header or query parameters to ensure your id and key are correct. Perhaps you are missing or have an extra character. | 
{% /table %}

---

### Privacy

To minimise the data collected about a user’s browsing behaviour, we only use first-party cookies.

As browser vendors move away from third-party cookies, Yoti is ahead of the changing technological landscape. An age token isn’t a cookie, but it does rely on a first-party cookie being dropped in the browser. This allows us to understand if a visitor’s device has previously been used to verify an age without collecting more identifiable data through third-party cookies.

Third-party cookies are used by multiple websites to ascertain information about user behaviour or age without their knowledge or consent. By choosing to only use first party cookies, we don’t share information unless there is a direct interaction with the portal that can be observed by the user.

Age tokens are stored inside our infrastructure and do not get passed on to any relying parties or consumer.