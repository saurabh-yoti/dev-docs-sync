---
type: page
title: Launching the Yoti client SDK
listed: true
slug: launching-the-yoti-client-sdk
description: 
index_title: Launching the Yoti client SDK
hidden: 
keywords: 
tags: 
---

The next step is to load the Yoti client SDK. Yoti will send a response back with the following from the create session request:

- Session ID
- Session Token

These values can now be used to create a URL.

{% table %}
| Example | 
| ---- | 
| &lt;hostname&gt;/idverify/v1/web/index.html?sessionID=&lt;inputsessionID&gt;&amp;sessionToken=&lt;yoursessionTokenID&gt;&lt;br&gt; | 
{% /table %}

{% table %}
| URL Component | Description | 
| ---- | ---- | 
| Base URL | Please contact Yoti for this on sdksupport@yoti.com | 
| Path | /idverify/v1/web/index.html | 
| sessionID | ?sessionID=&lt;yoursessionID&gt; | 
| sessionToken | &amp;sessionToken=&lt;yoursessionTokenID&gt; | 
{% /table %}

The constructed url​ (using the session Id and session token), which loads the customised Yoti Client SDK, can be used in several ways:

- Within an iframe on your webpage
- As a link on your webpage
- As a link shared securely with a user 

The example below demonstrates how an iframe can be used. 

{% code %}
{% tab language="javascript" %}
<html>
	<iframe src="<hostname>/idverify/v1/web/index.html?sessionID=<inputsessionID>&sessionToken=<inputsessionID>"width="930"height"750" allow="camera"></iframe>
</html>
{% /tab %}
{% /code %}

Once the Yoti Client SDK has launched it will take the user through the ID document capture flow.

In all of the above configurations the Yoti Client SDK will fetch the verification session configuration. This will provide configuration for the captures to be performed and which methods are allowed.

Having received the session configuration, the Yoti Client SDK will handle the capture of all resources necessary to process the requested tasks and checks, and submit them to the server.

Once the required resources (and their associated media) have been captured and uploaded, the end user is redirected back to the relying business client so that they may continue their journey via the success or error URLs. The tasks and checks are performed in the background, and any updates are sent to the updates URL (if subscribed) or can be found by calling the session retrieval endpoint. Please see the next step for more information.