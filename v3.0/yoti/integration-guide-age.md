---
type: page
title: Integration guide
listed: true
slug: integration-guide-age
description: 
index_title: Integration guide
hidden: 
keywords: 
tags: 
---

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
This product is in the BETA stage. Any feedback on the product would be much appreciated.    </div>
    <div class="alert-links"> 
       <a href="mailto:sdksupport@yoti.com">SDK Support contact</a>

    </div>
</div>
{% /html %}

The below will guide you through the implementation steps for our age verification service API on mobile or web.  The options for age verification are:

- [Yoti App](https://www.yoti.com/business/digital-id/)
- [Yoti Age Scan](https://www.yoti.com/business/age-verification/)
- [Yoti Doc Scan ](https://www.yoti.com/business/doc-scan/)- Coming soon.

You can pick and choose which products you would like to display to the user to perform an age check.

The integrations steps are as follows:

1. [Create a session](https://developers.yoti.com/yoti/integration-guide-age#create-a-session)
2. [Launch the user view](https://developers.yoti.com/yoti/integration-guide-age#launch-the-user-view)
3. [Receive the result](https://developers.yoti.com/yoti/integration-guide-age#receiving-an-age-result)

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      You will need to download the Yoti app on your phone and register your business with Yoti.
   </div>
   <div class="alert-links"> 
      <a  target="_self" href="https://developers.yoti.com/yoti/getting-started-hub"> Onboarding with Yoti </a>
   </div>
</div>
{% /html %}

After you have created an organisation with us please [contact us](mailto:sdksupport@yoti.com) for API keys including your organisation name. We aim to get you api keys within 1-2 working days.

Yoti will provide:

- API Key
- SDK ID

---

## Technical Overview

This section describes the API interactions for a web and mobile web integration. Data is exchanged securely between the relying party (your backend), Yoti and the client (the end user’s browser or mobile device).

{% image url="https://image-archive.developerhub.io/image/upload/71150/ee3ofsbgr3brehh4zzm1/1603120413.png" caption="Yoti Age Flow" mode="responsive" height="814" width="2086" %}
{% /image %}

A **session** represents one end-to-end request of the age verification service. Each time the age verification service is initiated a unique session identifier is assigned from Yoti's backend. Every time a user elects a method of age verification on your relying business app or website, you will need to create a session with Yoti to perform the checks.

Once the Yoti Client has launched it will take the end user through the appropriate age capture flow. Once this flow is completed the end user is redirected back to the relying business client so that they may continue their journey. These redirects are defined when generating the session.

The session can be retrieved using the session ID. The response from this endpoint contains information on the age of the user, result and method.

---

## Create a session

To begin the age verification service start by informing Yoti of your intent. This is done by making a post request to the session create endpoint.

{% code %}
{% tab language="http" %}
POST https://age.yoti.com/sessions/create
{% /tab %}
{% /code %}

{% table %}
| Header | Description | 
| ---- | ---- | 
| Authorization | API Key to call the Yoti Age API. This should be sent as a bearer token. | 
| Content-Type | application/json | 
{% /table %}

Yoti Age uses an HTTP authentication scheme called ‘bearer authentication’. This involves security tokens called ‘bearer tokens’. They are the predominant type of access token used with [OAuth 2.0](https://oauth.net/2/). A resource should interpret a bearer token as "Give the bearer of this token access". The client must send this token in the Authorization header when making requests to protected resources.

It is important that your API Key remains strictly confidential. It must be stored securely. We advise that you never commit any code containing your API Key, and never share it beyond the authorised party.

If you believe your API key has been compromised, please contact us as soon as possible. This can be done through your account manager or via our support desk by emailing [sdksupport@yoti.com](mailto:sdksupport@yoti.com).

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
    "reference_id": "123123",
    "ttl": 300000000,
    "callback_url": "https://yourdomain.example",
    "notification_url": "https://yourdomain.example/updates"
}
{% /tab %}
{% /code %}

{% table %}
| Parameter | Types | Description | 
| ---- | ---- | ---- | 
| Type | OVER, UNDER, AGE | This is where you define what preference you want to set for the age of the user.\n\nIf the user is OVER an age threshold e.g. over 21 \n\n\n\nIf the user is UNDER an age threshold e.g. under 30\n\n\n\nIf the user is the AGE e.g if the user is 25. | 
| digital_id | digital_id | If you wish to enable the Yoti app as an option to perform an age age verification service. | 
| age_estimation | age_estimation | If you wish to enable the Yoti Age Scan as an option to perform an age age verification service. | 
| allowed | True / False | Whether you want the verification method to be available for the user to use. | 
| threshold | Integer e.g. 30 | Age threshold for under/over age limits | 
| level | NONE | What level of security for anti-spoofing on age-estimation. Currently we do not support anti-spoofing. Stay tuned on our [release pages ](https://developers.yoti.com/releases)to see when we do. | 
| reference id | 123 | Unique ID for each session. | 
| ttl | seconds (60) | How long the session is valid for, the user will need to complete this before the ttl expires. This must be at least 60 seconds (1 minute). | 
| callback URL | [https://yourdomain.example](https://yourdomain.example) | Where to send your user after they have finished age verification. | 
| notification URL | [https://yourdomain.example/updates](https://yourdomain.example/updates) | To state where the results of an age verification should be sent. | 
{% /table %}

### Example response

If the request is successful and a session is generated the API will send a response in the form:

{% code %}
{% tab language="json" %}
{
  "id": "uuid",
  "expires_at": "2020-10-19T16:06:25.080Z"
}
{% /tab %}
{% /code %}

**Error codes**

{% table %}
| Error code | Description | 
| ---- | ---- | 
| 201 | Success | 
| 400 | Missing field in post body | 
| 401 | Missing or unknown SDK ID | 
| 403 | Incorrect API key | 
{% /table %}

---

## Launch the user view

In the previous section we saw how to create a session request, which returns:

- Session ID

We then use these to construct a URL which loads the Yoti Client. The URL can be used in the following ways:

- Within an iFrame on your webpage
- As a link on your webpage
- As a link shared securely with a user

{% code %}
{% tab language="http" %}
https://age.yoti.com?sessionId=<sessionId>&sdkId=<sdkId>
{% /tab %}
{% /code %}

{% table %}
| URL component | Description | 
| ---- | ---- | 
| sessionId | The session ID from the Yoti response. | 
| sdkID | This is your SDK ID provided to you by Yoti. | 
{% /table %}

Once the Yoti Client has launched it will take the user through the age verification flow. The user will be redirected to the specified call back URL. 

{% image url="https://image-archive.developerhub.io/image/upload/71150/ord8w3bdsg5o83vmtios/1603185729.png" caption="User View" mode="responsive" height="671" width="1064" %}
{% /image %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
        While it is possible to use this solution in an iframe, using a new browser window will guarantee an optimal user experience.
    </div>
    <div class="alert-links"> 

   </div>
</div>
{% /html %}

---

## Receiving an age result

Each session has a configured 'time to live' (TTL) which must be above 60 seconds (1 minute). When a session is created, it remains active until it's time to live is reached. For any active session, you can use the retrieve a result on the session.

To receive the result of an age verification, a HTTP endpoint (notification URL) needs to be listening for a JSON payload in the format of the below:

{% code %}
{% tab language="json" %}
{
    "method": "AGE_ESTIMATION",
    "status": "COMPLETE",
    "result": <value based on the session configuration>, // AGE, OVER, UNDER
    "age": <actual age of the person>,
    "sdk_id": <your sdk id>,
    "session_id": <the session id for this check>,
    "reference_id": <reference_id provided when you created your session>,
    "created_at": <time the session was completed>
}
{% /tab %}
{% /code %}

---

## Examples

Please see examples for different scenarios.

{% code %}
{% tab language="json" %}
//OVER 18

{
  "type": "OVER",
  "age_estimation": {
    "allowed": true,
    "threshold": 18,
    "liveness_level": "NONE"
  },
  "digital_id": {
    "allowed": true,
    "threshold": 18,
    "level": "NONE"
  },
  "ttl": 900,
  "reference_id": "over_18_example",
  "callback_url": "https://www.yourdomain.example/account/profile",
  "notification_url": "https://yourdomain.example/webhook"
}
{% /tab %}
{% tab language="json" %}
//OVER 16

{
  "type": "OVER",
  "age_estimation": {
    "allowed": true,
    "threshold": 16,
    "liveness_level": "ACTIVE"
  },
  "digital_id": {
    "allowed": false,
    "threshold": 18,
    "level": "NONE"
  },
  "ttl": 900,
  "reference_id": "over_18_example",
  "callback_url": "https://www.yourdomain.example/account/profile",
  "notification_url": "https://yourdomain.example/webhook"
}
{% /tab %}
{% tab language="json" %}
//EXACT AGE

{
  "type": "AGE",
  "age_estimation": {
    "allowed": true,
    "threshold": 13,
    "liveness_level": "NONE"
  },
  "digital_id": {
    "allowed": true,
    "threshold": 13,
    "level": "NONE"
  },
  "ttl": 900,
  "reference_id": "string",
  "callback_url": "https://www.yourdomain.example/account/profile",
  "notification_url": "https://yourdomain.example/webhook"
}
{% /tab %}
{% /code %}