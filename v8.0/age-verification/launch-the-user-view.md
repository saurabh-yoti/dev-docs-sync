---
type: page
title: Launch the user view
listed: true
slug: launch-the-user-view
description: 
index_title: Launch the user view
hidden: 
keywords: 
tags: 
---

In the previous section we saw how to create a session request, which returns:

- Session ID

We then use these to construct a URL which loads the Yoti Client. The URL can be used in the following ways:

- Within an iFrame on your webpage
- As a link on your webpage
- As a link shared securely with a user

{% badge type="info" text="Hint" /%} This is only for sessions where the UI needs to be launched 

{% code %}
{% tab language="http" %}
https://age.yoti.com?sessionId=<sessionId>&sdkId=<sdkId>
{% /tab %}
{% /code %}

{% table %}
| URL component | Description | 
| ---- | ---- | 
| sessionId | The session ID from the Yoti session create response. | 
| sdkId | This is your SDK ID provided to you by Yoti. | 
{% /table %}

Once the Yoti Client has launched it will take the user through the age verification flow. The user will be redirected to the specified call back URL on completion of one of the age verification methods.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1603979234/72728/pbpim3nnb57jegewbhno.png" caption="user view" mode="responsive" height="664" width="1060" %}
{% /image %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
        While it is possible to use this solution in an iFrame, using a new browser window will guarantee an optimal user experience.
    </div>
    <div class="alert-links"> 

   </div>
</div>
{% /html %}

## Preferred method

If you wish to encourage a particular age verification method to be used first, you can launch the user directly into your specified method. Doing so will mandate the option, but still allow any other enable methods to be retried in case a user does not meet the desired threshold.

{% table %}
| Method | URL | 
| ---- | ---- | 
| Age estimation | [https://age.yoti.com/age-estimation?sessionId=&lt;sessionId&gt;&sdkId=&lt;sdkId](https://age.yoti.com/age-estimation?sessionId=%3CsessionId%3E&amp;sdkId=%3CsdkId)&gt; | 
| IDV | [https://age.yoti.com/doc-scan?sessionId=&lt;sessionId&gt;&sdkId=&lt;sdkId](https://age.yoti.com/doc-scan?sessionId=%3CsessionId%3E&amp;sdkId=%3CsdkId)&gt; | 
| Digital id | [https://age.yoti.com/yoti?sessionId=&lt;sessionId&gt;&sdkId=&lt;sdkId](https://age.yoti.com/yoti?sessionId=%3CsessionId%3E&amp;sdkId=%3CsdkId)&gt; | 
{% /table %}

---

The user interface may be themed to make the UI appear closer to your own web page. Theming allows your user to have a consistent experience navigating through your website and into the age verification flow.

The following items can be customised:

- Background colour
- Body font colour
- Body buttons
- Card buttons

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1623857266/v2_2762/n5wifwictftx0oe3axro.png" caption="Theming" mode="responsive" height="1278" width="2846" %}
{% /image %}

{% badge type="info" text="Hint" /%} Themes are assigned per SDK ID and cannot be dynamically changed at session creation.