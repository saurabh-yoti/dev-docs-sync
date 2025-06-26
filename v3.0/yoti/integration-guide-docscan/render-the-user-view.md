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

In the previous section we saw how to create a session [request](/yoti/generating-a-session), which returns: 

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

Please note:`allow="camera"` is required when using Yoti Doc Scan on mobiles (web or native), and is serving the website over HTTPS.

{% video %}
{% /video %}

### Event notifications

Yoti recommend using POST messaging if you would like to be notified for one of the following situations :

- When the iFrame flow has **successfully** completed
- If an [error](https://developers.yoti.com/yoti/render-the-user-view#error-codes) occurs during the flow. See below for full error list.

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

**Please note** that, if a success URL or error URL is supplied as part of the [session preferences](/yoti/generating-a-session#preferences), then the iFrame will always automatically redirect. To utilise POST messaging, a success URL and error URL should be omitted.

### Translation

Yoti Doc scan has configuration settings to change the language of the information displayed to the client.

Supported languages are:

- French (Français)
- Spanish (Español)
- Thai (ภาษาไทย)
- Russian (русский)
- Brazilian Portuguese (português brasileiro)
- Turkish (Türkçe)
- Vietnamese (Tiếng Việt)
- Czech (čeština)
- German (Deutsch)
- Canadian 

For information on how to do this please go [here](https://developers.yoti.com/yoti/generating-a-session#preferences).

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

{% table %}
| Error Codes | Platform - Mobile or Web | Description | Retry Possible | 
| ---- | ---- | ---- | ---- | 
| 1000 | Mobile | No error occurred – the end-user cancelled the session for an unknown reason. | Yes | 
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
| 5003 | Mobile | SDK is out-of-date - please update the SDK to the latest version - (see [github](https://github.com/getyoti/) pages). | No | 
| 5004 | Mobile/Web | Unexpected internal error. | No | 
| 5005 | Mobile | Unexpected document scanning error. | No | 
| 5006 | Mobile/Web | Unexpected liveness error. | No | 
| 5007 | Web | iOS browser in use other than Safari. Only Safari on iOS may access camera. | No | 
{% /table %}