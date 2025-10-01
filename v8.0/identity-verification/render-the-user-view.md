---
type: page
title: Client side user view
listed: true
slug: render-the-user-view
description: 
index_title: Client side user view
hidden: 
keywords: 
tags: 
---

The next step is to load the Yoti client SDK. Here we describe how to:

- Launch the web client
- Or launch the mobile client

## Web client

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

{% html %}
<div style="padding:56.25% 0 0 0;position:relative;"><iframe src="https://player.vimeo.com/video/647392006?h=6c95831bb6&amp;badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=58479&dnt=1" frameborder="0" allow="autoplay; fullscreen; picture-in-picture" allowfullscreen style="position:absolute;top:0;left:0;width:100%;height:100%;" title="Seamless identity verification directly on your website or app"></iframe></div><script src="https://player.vimeo.com/api/player.js"></script>
{% /html %}

### Event notifications

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

### iFrame launch - Post method

Step 1: Render the Iframe with just the base Yoti URL, without the URL parameters:

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

Step 3: User proceeds as normal. No other implementation changes are required to enable this  functionality.

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

---

## In-session feedback

OCR failure on the document is a good sign that there’s something wrong with the submission.

Yoti will process the image and provide feedback to the user based on the result of the image capture. In unsuccessful prompting the user to try to upload once again and why if unsuccessful.

In session feedback should help:

- Notify the user something is wrong with the submission
- Provide the user with a chance to re-upload the document within the same session
- Increase number of successful checks

By default Yoti will allow 1 extra attempt. The screen that will be shown to the user on unsuccessful attempts is:

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/jdrxfixfuvrgtskhd5h3/1623415101.png" caption="In session feedback example screen" mode="600" height="1142" width="1802" %}
{% /image %}

The user flow is as follows:

1. The user will select document type and country.
2. The user will upload / take a photo of the document.
3. If the document can be OCR’d it will go through.
4. If it cannot due to user error, they will be asked to retry or change their document type.

If the user has reached their maximum attempts the session will end there.

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/ztxrkzwhyxxv3qsepktv/1623414895.png" caption="End of in-session feedback" mode="600" height="1714" width="2374" %}
{% /image %}

Coming soon: Ability to configure the retry attempts in the server side integration. This is already live in the API. 

---

Reclassification

If the wrong document is uploaded Yoti will attempt to reclassify the document. That means, that if the submitted document type or / and country would be different from the ones user selected Yoti will save it under the detected one if the data is extracted successfully.

---

## Translation

Yoti Identity verification has configuration settings to change the language of the information displayed to the client.

Supported languages are:

{% synced id="idv-web-localisation" %}
{% /synced %}

For information on how to do this please go to [auto$](/identity-verification/client-preferences).

{% html %}
<div class="alert-know">

    <div class="alert-title" id="know">

Jump to
    </div>

    <div class="alert-text">

        Please head over to our document settings section where you can remove documents / countries in the user view.

    </div>

    <div class="alert-links"> 

  <a href="https://developers.yoti.com/identity-verification/document-checking#document-settings">Document settings</a>

    </div>

</div>
{% /html %}

{% badge type="info" text="Hint" /%} See the next page for information on integrating our native SDK's.

---

## Error codes

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
| 4001 | Web | The user has submitted a document that does not match the selection, or the user has exceed attempts to submit an in date document. | Yes, a new session is required. | 
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
| 5011 | Web | The camera does not meet the minimum required resolution | No | 
| 6000 | Mobile | Document Capture dependency not found error | No | 
| 6001 | Mobile | Liveness dependency not found error | No | 
| 6002 | Mobile | Supplementary Document capture dependency not found error | No | 
| 6003 | Mobile | Face capture dependency could not be found. Only applicable to Native SDK | Yes, with dependency installed | 
| 7000 | Web | The user did not have the required documents | No | 
{% /table %}