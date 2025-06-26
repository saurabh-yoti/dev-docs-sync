---
type: page
title: Launch the user view
listed: true
slug: render-the-user-view
description: 
index_title: Launch the user view
hidden: 
keywords: 
tags: 
---

## Web client

The next step is to load the Yoti client SDK. 

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
     Please have a look at our best practices for a better performance of the SDK.
   </div>
   <div class="alert-links"> 
         <a href="https://developers.yoti.com/yoti/user-experience-docscan">User experience</a>
   </div>
</div>
{% /html %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know... 
    </div>
    <div class="alert-text">
       This section refers to the implementation on web clients, please see the 'mobile integration' section for details of our 
       native Android and iOS SDKs.
    </div>
    <div class="alert-links"> 
        <a href="https://developers.yoti.com/yoti/docscan-mobile">Moblie integrations</a>
   </div>
</div>
{% /html %}

### How it works

The constructed URL​ (using the sessionId and session token), which loads the customised Yoti Client SDK, can be used in several ways:

- Within an iframe on your webpage
- As a link on your webpage
- As a link shared securely with a user

{% video %}
{% /video %}

In the response to your create session [request](/yoti/generating-a-session), you will have received:

- Session ID
- Session Token

These values can now be used to create a URL.

{% code %}
{% tab language="http" %}
https://api.yoti.com/idverify/v1/web/index.html?sessionID=<inputsessionID>&sessionToken=<yoursessionToken>
{% /tab %}
{% /code %}

{% table %}
| URL Component | Description | 
| ---- | ---- | 
| sessionId | The session ID from the Yoti response. | 
| sessionToken | The session token from the Yoti response. | 
{% /table %}

The example below demonstrates the use of an iframe:

{% code %}
{% tab language="markdown" %}
<iframe src="<https://api.yoti.com/idverify/v1/web/index.html?sessionID=<inputsessionID>&sessionToken=<yoursessionTokenID>" style="height:600px; width:100%; border:none;" allow="camera"></iframe>
{% /tab %}
{% /code %}

Once the Yoti Client SDK has launched it will take the user through the ID document capture flow.

The Yoti Client SDK will fetch the verification session configuration that was defined on session creation. This will provide configuration for the captures to be performed, and which methods are allowed.

Having received the session configuration, the Yoti Client SDK will handle the capture of all resources necessary to process the requested tasks and checks, and submit them to the server.

Once the required resources (and their associated media) have been captured and uploaded, the end user is redirected back to the relying business client so that they may continue their journey via the success or error URLs. The tasks and checks are performed in the background, and any updates are sent to the updates URL (if subscribed) or can be found by calling the session retrieval endpoint.

{% html %}
<div class="alert-know">

    <div class="alert-title" id="know">

        Knowledge base

    </div>

    <div class="alert-text">

        Please head over to our knowledge base on selecting multiple documents / countries in the user view.

    </div>

    <div class="alert-links"> 

  <a href="https://developers.yoti.com/yoti/knowledge-base-docscan#document--country-selection">Document / Country selection</a>

    </div>

</div>
{% /html %}

---

## Mobile client

The mobile integration provides a native version of Yoti Doc Scan which can be integrated into your own Mobile App, as opposed to being rendered through a webpage.

The mobile integrations that we currently support are listed below for the Yoti Doc Scan integration. Please select your preferred language to continue.

- [iOS](https://github.com/getyoti/yoti-doc-scan-ios)
- [Android](https://github.com/getyoti/yoti-doc-scan-android)
- [React native](https://github.com/getyoti/yoti-doc-scan-react-native)

---

## Error codes

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
     Please have a look at our best practices for a handing errors.
   </div>
   <div class="alert-links"> 
         <a href="https://developers.yoti.com/yoti/user-experience-docscan#error-handling">User experience</a>
   </div>
</div>
{% /html %}

{% table %}
| Error Codes | Platform - Mobile or Web | Description | Retry Possible | 
| ---- | ---- | ---- | ---- | 
| 1000 | Mobile | No error occurred - the end-user cancelled the session for an unknown reason. | Yes | 
| 2000 | Mobile/Web | Unauthorised request (wrong or expired session token). | Yes\n\nNew session required. | 
| 2001 | Mobile/Web | Session not found. | Yes\n\nNew session required. | 
| 2002 | Mobile/Web | Session expired. | Yes\n\nNew session required | 
| 2003 | Mobile/Web | SDK launched without session Token. | -- | 
| 2004 | Mobile/Web | SDK launched without session ID. | -- | 
| 3000 | Mobile/Web | Yoti's services are down or unable to process the request. | Yes | 
| 3001 | Mobile | An error occurred during a network request. | Yes | 
| 3002 | Mobile/Web | User has no network. | Yes | 
| 4000 | Mobile/Web | The user did not grant permissions to the camera. | Yes\n\nThe end-user will be asked again to grant permissions to the camera | 
| 5000 | Mobile/Web | No camera.\n\n(When user's camera was not found and file upload is not allowed) | No | 
| 5001 | Web | Unsupported browser/platform by the liveness flow. | No | 
| 5002 | Mobile/Web | No more local tries for the liveness flow. | Yes | 
| 5003 | Mobile | SDK is out-of-date - please update the SDK to the latest version. (see github pages) | No | 
| 5004 | Mobile/Web | Unexpected internal error. | No | 
| 5005 | Mobile | Unexpected document scanning error. | No | 
| 5006 | Mobile/Web | Unexpected liveness error. | No | 
| 5007 | Web | iOS browser in use other than Safari. Only Safari on iOS may access camera. | No | 
{% /table %}