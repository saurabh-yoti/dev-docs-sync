---
type: page
title: Knowledge base
listed: true
slug: knowledge-base-app
description: 
index_title: Knowledge base
hidden: 
keywords: 
tags: 
---

This is your online library of information about the Yoti App.

## FAQs

Some of our most asked questions from integrators and businesses.

**[View Developer FAQs](https://yoti.zendesk.com/hc/en-us/sections/360000034333-Yoti-App)**

---

## Query parameters

You can append query params to the landing page URL that displays the Yoti button. These will be added to the callback URL.

For example if you load the landing page containing the Yoti button as follows:

[https://example.com/?iso=test&user_id=6667](https://example.com/?iso=test&amp;user_id=6667)

The query parameters (iso=test&user_id=6667) will be returned in the callback URL.

---

## Non-browser client

{% html %}
<div class="alert-BYS">

   <div class="alert-title" id="BYS">

      Before you start

   </div>

   <div class="alert-text" >

   Have a read of our web integration guide and ensure you have onboarded with Yoti. 

   </div>

   <div class="alert-links"> 

         <a href="https://developers.yoti.com/yoti/web-integration">Web integration</a>
  <a href="https://developers.yoti.com/yoti/getting-started-hub">Onboarding with Yoti</a>


   </div>

</div>
{% /html %}

This section below describes the process of creating a personalised client which triggers the Yoti QR flow. Yoti recommend You will need to have registered an Organisation and created a Yoti Application before continuing.

Our Web Integration packages the process together of retrieving a Yoti QR code and forwarding the token to your own server. However it is possible to manually construct this QR code as this can be necessary in cases where you do not have access to a Web server on your front end, for example using a kiosk of GUI.

Requesting a QR code is broken down into the following steps:

1. [Requesting a QR code from Yoti Servers](https://developers.yoti.com/yoti/knowledge-base-digitalid#requesting-a-qr-code-from-yoti-servers)
2. [Decoding and resolving the QR code metadata](https://developers.yoti.com/yoti/knowledge-base-digitalid#decoding-and-resolving-the-qr-code-metadata)
3. [Opening a web socket channel to Yoti using the resolved metadata](https://developers.yoti.com/yoti/knowledge-base-digitalid#opening-a-web-socket-channel)
4. [Receiving a Yoti token over the web socket channel or handling a session error](https://developers.yoti.com/yoti/knowledge-base-digitalid#receiving-a-token)
5. [Passing the received token to the callback url that has been specified in Yoti Hub](https://developers.yoti.com/yoti/knowledge-base-digitalid#passing-the-token-to-the-callback-url)

### Requesting a QR code from Yoti Servers

In order to request a QR code from Yoti Servers the client must create a `GET HTTPS` request to the following endpoint:

**Endpoint 1: Retrieve a QR code**

{% code %}
{% tab language="markup" %}
https://api.yoti.com/api/v1.1/sessions/apps/<sdkId>/scenarios/<scenarioId>
{% /tab %}
{% /code %}

{% table %}
| Parameter | Description | 
| ---- | ---- | 
| sdkId | sdkId is the SDK_ID found with your Yoti Hub Application | 
| scenarioId | scenarioId is  the Scenario ID found within your Yoti Hub Application that relates to a specific scenario | 
{% /table %}

A Yoti QR code contains a URL and is returned in full from the `Retrieve a QR code` endpoint.

An example of how a URL in a QR code should look is as follows:

**Yoti QR code content**

{% code %}
{% tab language="markup" %}
https://code.yoti.com/CAEaJDlhMzg5MTRiLTg0ZDAtNGI3Zi05NDNiLWQzNzBmNmM3YTVlYzAA
{% /tab %}
{% /code %}

{% html %}
<div class="alert-GTK">

    <div class="alert-title" id="GTK">

        Good to know... 

    </div>

    <div class="alert-text">

The important section of the URL is the string that follows https://code.yoti.com/. This is a base 64 url encoded Protocol Buffer.

    </div>

</div>
{% /html %}

### Decoding and resolving the QR code metadata

In order to decode and resolve the URL returned by Endpoint 1 and retrieve the QR code metadata, it is necessary to:

1. Split the URL by `https://code.yoti.com/` keeping the QR code data, i.e. `CAEaJDlhMzg5MTRiLTg0ZDAtNGI3Zi05NDNiLWQzNzBmNmM3YTVlYzAA`
2. Base 64 url decode the obtained string.

{% code %}
{% tab language="java" %}
byte[] bytes = Base64.getUrlDecoder().decode(str);
{% /tab %}
{% /code %}

Unmarshal the protocol buffer data structure using the following proto definition:

{% code %}
{% tab language="java" %}
syntax = "proto2";
package qrpubapi_v1;
option java_package = "com.yoti.qrpubapi_v1";
option java_outer_classname = "QrCodeMsgProto";
enum Issuer {
    CONNECT = 1;
}
enum Transport {
    UNDEFINED = 0;
    URI = 1;
    QR_CODE = 2;
}
message QrCodeMsg{
    optional Issuer issuer = 1;
    optional bytes sharing_token = 2;
    optional bytes ref_id = 3;
    optional bytes  policy = 4;
    optional Transport transport = 6;
}
{% /tab %}
{% /code %}

Major languages provide protobuf compilers to generate code that automatically handles protocol buffers marshalling/unmarshalling.

If you are using the java protobuf compiler and you have [`generated your proto stubs`](https://developers.google.com/protocol-buffers/docs/proto#generating), un marshalling the described protocol buffer is very simple.

{% code %}
{% tab language="java" %}
QrCodeMsg qrCodeMsg = QrCodeMsg.parseFrom(bytes);
{% /tab %}
{% /code %}

Although there are few fields in the described data structure, we are only interested in the field named "ref_id", since the others are used by the Yoti app, in order to properly handle the scanned code.

The ref_id field must be interpreted as a UTF-8 string (default encoding for the Java language when creating a String object) and used to retrieve the QR code meta data. This can be achieved by invoking the following endpoint:

**Endpoint 2: retrieving QR code metadata**

{% code %}
{% tab language="markup" %}
https://api.yoti.com/api/v1.1/qrcodes/refs/<ref_id>
{% /tab %}
{% /code %}

{% table %}
| Parameter | Description | 
| ---- | ---- | 
| ref_id | This is the UTF-8 string representation of the ref_id field obtained from the proto buffer data structure. | 
{% /table %}

The result of this invocation is a JSON payload that looks like the following:

{% code %}
{% tab language="json" %}
{

  "name": "App name",
  "policy": "CggKBnNlbGZpZQoOCgxwaG9uZV9udW1iZXISEgoQYXBwbGljYXRpb25fbG9nbxIRCg9hcHBsaWNhdGlvbl91cmwSEgoQYXBwbGljYXRpb25fbmFtZRIdChthcHBsaWNhdGlvbl9yZWNlaXB0X2JnY29sb3IYASAA",
  "application_id": "a9c4a5ad-d9e5-4fc8-a561-6eedbc882691",
  "application_name": "Yoti App",
  "receipt_bg_color": "#2D9FFF",
  "callback_endpoint": "https://yoti.com/app",
  "sharing_token": "2z94Ix7B7t6B+C3aUSy/6bBuMzQJYZqEBbQa9fp3O6r0bqRgpp0VveojLu8FxdLT",
  "session_data": "0LBGRyLy-422ef9b5-871f-4fba-8bed-e70bc4a1e650"
}
{% /tab %}
{% /code %}

The field we are interested in is the one named "session_data" and it will be used to establish a web socket channel through which our client will get notified about a successful/failed interaction.

Attribute "callback_endpoint" will be used in the last step of this guide.

### Opening a web socket channel

Opening a web socket channel to Yoti using the resolved metadata

To create a web socket channel to Yoti servers, it is necessary to hit the following endpoint using a web socket client:

**Endpoint 3: creating a web socket channel**

{% code %}
{% tab language="markup" %}
wss://api.yoti.com/api/v1.1/connect-sessions/<session_data>
{% /tab %}
{% /code %}

{% table %}
| Parameter | Description | 
| ---- | ---- | 
| session_data | The session_data obtained from the call to endpoint 2 | 
{% /table %}

It is important to know that different clients connect using different schemes: some use the WSS protocol, while others make an https request and expect the server to do the upgrade to WSS (this is the standard approach).

Once the connection is established, you will need to send an initial subscription message, the value of this is the session_data used to create the channel. An example of this is shown below.

{% code %}
{% tab language="json" %}
{
	"subscription": <session_data>
}
{% /tab %}
{% /code %}

{% code %}
{% tab language="javascript" %}
var socket = new WebSocket(socketAddress + '/connect-sessions/' + session_data)
socket.onopen = function() {
  socket.send(JSON.stringify({subscription: session_data}))
}
{% /tab %}
{% /code %}

If successful the server will send the following message back over the channel:

{% code %}
{% tab language="json" %}
{
  "status" : "ACCEPTED",
  "subscription" : "0LBGRyLy-422ef9b5-871f-4fba-8bed-e70bc4a1e650"
}
{% /tab %}
{% /code %}

If an invalid session_data value has been provided, the server will send the following message:

{% code %}
{% tab language="json" %}
{
  "status" : "REJECTED",
  "subscription" : "0LBGRyLy-422ef9b5-871f-4fba-8bed-e70bc4a1e650"
}
{% /tab %}
{% /code %}

### Receiving a token

Receiving a Yoti token over the web socket channel or handling a session error.

Assuming the connection was successfully established, the you must now wait for a further message that signals the completion of the transaction.

If the transaction fails, the server will send the following message:

{% code %}
{% tab language="json" %}
{
  "status" : "FAILED",
  "subscription" : "0LBGRyLy-422ef9b5-871f-4fba-8bed-e70bc4a1e650"
}
{% /tab %}
{% /code %}

If the transaction times out, the server will send the following message:

{% code %}
{% tab language="json" %}
{
  "status" : "TIMED_OUT",
  "subscription" : "0LBGRyLy-422ef9b5-871f-4fba-8bed-e70bc4a1e650"
}
{% /tab %}
{% /code %}

If any of the last two messages occur, you should restart the process by requesting a new QR code.

Let's finally see what happens when a transaction is successfully completed. In this case the server will send the following message:

{% code %}
{% tab language="json" %}
{
  "status" : "COMPLETED",
  "subscription" : "0LBGRyLy-422ef9b5-871f-4fba-8bed-e70bc4a1e650",
  "token" : "egouerghwl4itjxpri4oty5ihfli4yg7tgbnkrliu"
}
{% /tab %}
{% /code %}

The token here is the Yoti token that must be passed to your application back-end, in order to retrieve the user shared profile using the Yoti SDKs.

Below is a javascript example that shows how to implement the logic that is necessary to correctly handle the channel communication.

{% code %}
{% tab language="javascript" %}
var socket = new WebSocket(socketAddress + '/connect-sessions/' + connection)
socket.onopen = function() {
  socket.send(JSON.stringify({subscription: connection}))
}
socket.onmessage = function(e) {
  var message = JSON.parse(e.data)
  switch(message.status) {
    case 'COMPLETED':
      var token = message.token
      // send token to backend here
      break;
    case 'ACCEPTED':                   
      break;
    case 'TIMED_OUT':
      // restart process
      break;
    case 'REJECTED':
      // restart process
      break;
  }
}
{% /tab %}
{% /code %}

### Passing the token to the callback URL

Passing the received token to the callback url that has been specified in Yoti Hub.

Finally, the received token must be forwarded to your back-end, which should be listening for GET requests at the address specified by the attribute named "callback_endpoint" that has been returned as a response to the request to endpoint 2.

The token should be provided as a query string parameter, so, in this example, the client should send a GET request to the follow URL:

{% code %}
{% tab language="markup" %}
https://yoti.com/app?token=egouerghwl4itjxpri4oty5ihfli4yg7tgbnkrliu
{% /tab %}
{% /code %}

It is worth noticing that, in case you are deploying your client in different physical locations, this would be the best point to provide some metadata by personalising your request to your own back-end.

The example above could be extended by providing more parameters:

{% code %}
{% tab language="markup" %}
https://yoti.com/app?token=egouerghwl4itjxpri4oty5ihfli4yg7tgbnkrliu&lane=2&location=WC2N4JH
{% /tab %}
{% /code %}

From here on, it is only a matter of using the Yoti SDK for your favourite language as described in [Web Integration](https://developers.yoti.com/yoti/web-integration).

Your endpoint can return any value in any format, since your client will handle it. Our suggestion is at least to capture the result of the interaction with the Yoti SDK and tell the client whether the interaction succeeded or not.

---

## Rendering a Yoti QR Code

If you're looking at integrating Yoti with a 'Non-browser' client, one of the tasks you will need to do is request a Yoti QR code from Yoti's servers. This URL must be transformed into a QR code before it can be scanned with the Yoti app. Yoti provides a simple API to transform this URL into an official Yoti QR.

By using an official Yoti QR Code you will establish a sense of trust with your user base.

{% image url="https://image-archive.developerhub.io/image/upload/23781/wlkyqqdl11rxjctvfjqo/1591286248.jpg" caption="Example QR code" mode="300" height="502" width="502" %}
{% /image %}

**Endpoint**

{% code %}
{% tab language="markup" %}
POST https://api.yoti.com/api/v1/qrcodes/image
{% /tab %}
{% /code %}

The following headers are required to use the image service:

{% table %}
| Header | Value | Description | 
| ---- | ---- | ---- | 
| Accept | The follow Accept values can be provided in the header\n\n\n\n- image/svg+xml\n- image/png | Returns a formatted QR code as an svg or png | 
{% /table %}

The request body should be formed as JSON, specifying a URL (mandatory) and an image size (option).

**Request body**

{% table %}
| Field | Value | 
| ---- | ---- | 
| url | This is the URL returned from requesting a Yoti QR | 
{% /table %}

{% code %}
{% tab language="json" %}
{
	"url": "https://code.yoti.com/<YotiCode>"
}
{% /tab %}
{% /code %}

**Possible Errors**

{% table %}
| Code | Description | Resolution | 
| ---- | ---- | ---- | 
| 400 | Missing url field in the request body | Ensure to POST a JSON body containing a url | 
| 406 | Empty Accept header | Send a request Accept header with the required image return type | 
| 406 | An Accept header was sent with an invalid return type | Ensure the Accept header is one of\n\n\n\n- image/svg+xml\n- image/png | 
{% /table %}