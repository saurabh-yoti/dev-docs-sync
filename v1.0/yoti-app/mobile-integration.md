---
type: page
title: Mobile Integration
listed: true
slug: mobile-integration
description: 
index_title: Mobile Integration
hidden: 
keywords: 
tags: 
---

Please view the [auto$](/yoti-app/web-integration) documentation first. The mobile SDKs purpose is to provide 3rd party applications the ability to request attributes from a Yoti profile whilst leveraging the Yoti mobile app.

The image below describes the login process and how your back-end integrates with the Yoti architecture.

{% image url="https://image-archive.developerhub.io/image/upload/12871/arruzqv0xbmsm5y76hah/1562781975.png" mode="600" height="1718" width="1312" %}
{% /image %}

For a detailed explanation please visit our GitHub pages. The SDKs we support for mobile are:

- iOS (Swift and Objective C): [https://github.com/getyoti/ios-sdk-button](https://github.com/getyoti/ios-sdk-button)_(You will need to ensure the minimum version of the deployment target is 9.0 or above.)_
- Android: [https://github.com/getyoti/android-sdk-button](https://github.com/getyoti/android-sdk-button)_(You will need to ensure the minimum version of your Android app is 4.0.3 or above)_

**Note:** If you want to use Yoti with other mobile application development frameworks, you have to make sure they support receiving a broadcast message from an external native app. The Cordova/Ionic platforms currently don’t have official support for it.