---
type: page
title: Launch the web view
listed: true
slug: render-the-user-view
description: 
index_title: Launch the web view
hidden: 
keywords: 
tags: 
---

The next step is to load the Yoti client view. Here we describe how to:

- Launch the web client
- Or launch the mobile client

In the previous section we saw how to create a request, which returns:

- Session ID
- Session Token

We then use these to construct a URL which loads the Yoti Client view. The URL can be used in the following ways:

- Within an iframe on your webpage
- As a link on your webpage
- As a link shared securely with a user

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
<iframe src="<https://api.yoti.com/idverify/v1/web/index.html?sessionID=<inputsessionID>&sessionToken=<yoursessionTokenID>" style="height:605px; width:100%; border:none;" allow="camera"></iframe>
{% /tab %}
{% /code %}

Once the Yoti Client SDK has launched it will take the user through the ID document capture flow.

Please note: `allow="camera"` is required when using Yoti Identity verification on mobiles (web or native), and is serving the website over HTTPS.

---

### Error codes

{% table %}
| Error Codes | Platform - Mobile or Web | Description | Retry Possible | 
| ---- | ---- | ---- | ---- | 
| 1000 | Mobile | No error occurred – the end-user cancelled the session for an unknown reason. | Yes | 
| 2000 | Mobile/Web | Unauthorised request (wrong or expired session token). | Yes, a new session is required. | 
| 2001 | Mobile/Web | Session not found. | Yes, a new session is required. | 
| 2002 | Mobile/Web | Session expired. | Yes, a new session is required. | 
| 2003 | Mobile/Web | SDK launched without session Token. | Yes, a new session is required. | 
| 2004 | Mobile/Web | SDK launched without session ID. | Yes, a new session is required. | 
| 3000 | Mobile/Web | Yoti's services are down or unable to process the request. | Yes | 
| 3001 | Mobile | An error occurred during a network request. | Yes | 
| 3002 | Mobile/Web | User has no network. | Yes | 
| 4000 | Mobile/Web | The user did not grant permissions to the camera. | Yes\n\nThe end-user will be asked again to grant permissions to the camera. | 
| 4001 | Web | The user has submitted a document that does not match the selection. | Yes, a new session is required. | 
| 5000 | Mobile/Web | No camera.\n\n(When user's camera was not found and file upload is not allowed) | No | 
| 5001 | Web | Unsupported browser/platform by the liveness flow. | No | 
| 5002 | Mobile/Web | No more local tries for the liveness flow. | Yes | 
| 5003 | Mobile | SDK is out-of-date - please update the SDK to the latest version - (see [github](https://github.com/getyoti/) pages). | No | 
| 5004 | Mobile/Web | Unexpected internal error. | No | 
| 5005 | Mobile | Unexpected document scanning error. | No | 
| 5006 | Mobile/Web | Unexpected liveness error. | No | 
| 5007 | Web | iOS browser in use other than Safari. Only Safari on iOS may access camera. | No | 
| 5008 | Web | Unsupported configuration | No | 
| 5009 | Mobile | There was not enough storage available to write to the device | No | 
| 5010 | Web | Camera access failed and no alternative capture method available | No | 
| 6000 | Mobile | Document Capture dependency not found error | No | 
| 6001 | Mobile | Liveness dependency not found error | No | 
| 6002 | Mobile | Supplementary Document capture dependency not found error | No | 
{% /table %}