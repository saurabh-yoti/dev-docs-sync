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

{% code %}
{% tab language="http" %}
https://age.yoti.com?sessionId=<sessionId>&sdkId=<sdkId>
{% /tab %}
{% /code %}

{% table %}
| URL component | Description | 
| ---- | ---- | 
| sessionId | The session ID from the Yoti session create response. | 
| sdkID | This is your SDK ID provided to you by Yoti. | 
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

---

## Theming

The user interface may be themed to make the UI appear closer to your own web page. Theming allows your user to have a consistent experience navigating through your website and into the age verification flow.

The following items can be customised:

- Background colour
- Body font colour
- Body buttons
- Card buttons

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1623857266/v2_2762/n5wifwictftx0oe3axro.png" caption="Theming" mode="responsive" height="1278" width="2846" %}
{% /image %}

Themes are assigned per SDK ID and cannot be dynamically changed at session creation.

For further details on theming, or to create a theme request please contact [clientsupport@yoti.com](mailto:clientsupport@yoti.com).