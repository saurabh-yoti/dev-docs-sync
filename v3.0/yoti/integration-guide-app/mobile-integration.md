---
type: page
title: Mobile integration
listed: true
slug: mobile-integration
description: 
index_title: Mobile integration
hidden: 
keywords: 
tags: 
---

Once you've set up your organisation account on the Yoti Hub, you’re ready to start integrating with Yoti. This section explains how to complete a basic mobile integration.

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      You need to have a completed web integration setup before you're able to complete a mobile integration.
   </div>
   <div class="alert-links"> 
         <a  target="_self" href="https://developers.yoti.com/yoti/getting-started-app">See web integration</a>
   </div>
</div>
{% /html %}

## Technical overview

The diagram below describes the mobile process and how your backend integrates with the Yoti architecture.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1575301553/23576/akys1ikcxqqtt2q0saoq.jpg" caption="Mobile integration process diagram" mode="600" height="1360" width="1106" %}
{% /image %}

---

## Mobile examples

The mobile integrations that we currently support are listed below for the Yoti App integration. Please select your preferred language to continue.

- [iOS (Swift & Objective C) ](https://github.com/getyoti/ios-sdk-button)- Minimum deployment target version 9.0 or above
- [Android](https://github.com/getyoti/android-sdk-button) - Min Android version 4.0.3 or above
- [React native](https://github.com/getyoti/react-native-sdk-button)

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
If you want to use Yoti with other mobile application development frameworks, you have to make sure they support receiving a broadcast message from an external native app. The Cordova / Ionic platforms currently don’t have official support for it.
    </div>
</div>
{% /html %}