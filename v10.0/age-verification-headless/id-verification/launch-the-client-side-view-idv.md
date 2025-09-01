---
type: page
title: Launch the client side view
listed: true
slug: launch-the-client-side-view-idv
description: 
index_title: Launch the client side view
hidden: 
keywords: 
tags: 
---

The next step is to load the Yoti client SDK. Here we describe how to:

- Launch the web client
- Or launch the mobile client

## Get Session Details

Firstly you will need to make an additional API call to retrieve session details, which will allow you to launch the client side view. The "{session-id}" would have been generated from the create session API call.

{% code %}
{% tab language="http" %}
GET https://age.yoti.com/api/v1/sessions/<session-id>/doc-scan
{% /tab %}
{% /code %}

{% table %}
| Header | Description | 
| ---- | ---- | 
| Yoti-SDK-Id | Your Yoti SDK ID | 
{% /table %}

---

#### Response Body

{% code %}
{% tab language="json" %}
{
  "token": "string",
  "session_id": "string"
}
{% /tab %}
{% /code %}

The token and session_id that are returned can be used to launch the client side view.

---

## [Web client](https://developers.yoti.com/identity-verification/render-the-user-view#web-client)

In the previous section we saw how to create a request, which returns:

- Session ID
- Session Token

We then use these to construct a URL which loads the Yoti Client SDK. The URL can be used in the following ways:

- Within an iframe on your webpage
- As a link on your webpage
- As a link shared securely with a user

{% code %}
{% tab language="http" %}
https://api.yoti.com/idverify/v1/web/index.html?sessionID=<inputsessionID>&sessionToken=<yoursessionToken>
{% /tab %}
{% /code %}

The example below demonstrates the use of an iframe:

{% code %}
{% tab language="markdown" %}
<iframe src="<https://api.yoti.com/idverify/v1/web/index.html?sessionID=<inputsessionID>&sessionToken=<yoursessionTokenID>" style="height:605px; width:100%; border:none;" allow="camera"></iframe>
{% /tab %}
{% /code %}

Once the Yoti Client SDK has launched it will take the user through the ID document capture flow.

Please note: `allow="camera"` is required when using ID verification on mobiles (web or native), and is serving the website over HTTPS.

### [Event notifications](https://developers.yoti.com/identity-verification/render-the-user-view#event-notifications)

Yoti recommend using POST messaging if you would like to be notified for one of the following situations :

- When the iFrame flow has **successfully** completed
- If an error occurs during the flow. See below for full error list.

A POST message for either of these events is structured as follows:

{% code %}
{% tab language="javascript" %}
{
  eventType: string, // "SUCCESS” or “ERROR”,
  eventCode: number // See 'Error codes' for possible error codes. This will be undefined in the event of a success
}
{% /tab %}
{% /code %}

Below is a javascript example that can be used to listen to these messages.

{% code %}
{% tab language="javascript" %}
window.addEventListener(
    'message',
    function(event) {
      console.log('Message received', event.data);

      if (event.data.eventType === 'SUCCESS') {
        // Act upon success
      } else if (event.data.eventType === ‘ERROR’) {
        // Act upon error
       const errorCode = event.data.eventCode;
      }
    }
  );
{% /tab %}
{% /code %}

**Please note** if a success URL or error URL is supplied as part of the session preferences then the iFrame will redirect after button click at the end of the flow. To utilise POST messaging, a success URL and error URL should be omitted.

### [iFrame launch - Post method](https://developers.yoti.com/identity-verification/render-the-user-view#iframe-launch---post-method)

Step 1: Render the iFrame with just the base Yoti URL, without the URL parameters:

`https://api.yoti.com/idverify/v1/web/index.html`

Step 2: Using the postMessage JavaScript functionality the session will be launched with the correct configuration, posting the following

{% code %}
{% tab language="json" %}
{
  eventType: 'INIT_SESSION',
	sessionID: '<Obtained from the get session API call>',
	sessionToken: '<Obtained from the get session API call>',
}
{% /tab %}
{% /code %}

Step 3: User proceeds as normal. No other implementation changes are required to enable this functionality

{% code %}
{% tab language="html" %}
<iframe src="https://api.yoti.com/idverify/v1/web/index.html" allow=”camera” width="100%" height="100%" id="iframeId"></iframe> 

<script> 
   const iframe = document.getElementById('iframeId').contentWindow;
   const origin = 'https://api.yoti.com';
   window.addEventListener(
       'message',
       event => {
          if (event.data.eventType === 'STARTED' && event.origin === origin) {
               iframe.postMessage({
                       eventType: 'INIT_SESSION',
                       sessionID: 'someSessionId',
                       sessionToken: 'someSessionToken',
                   },
                   origin
               );
           }
       }
   );
</script>
{% /tab %}
{% /code %}

## Native SDK

The mobile integration provides a native version of IDV which can be integrated into your own Mobile App, as opposed to being rendered through a webpage.

The mobile integrations that we currently support are listed below for the IDV integration. Please select your preferred language to continue.

- [iOS](https://github.com/getyoti/yoti-doc-scan-ios)
- [Android](https://github.com/getyoti/yoti-doc-scan-android)
- [React native](https://github.com/getyoti/yoti-doc-scan-react-native)