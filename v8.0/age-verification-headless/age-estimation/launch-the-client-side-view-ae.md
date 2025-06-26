---
type: page
title: Launch the client side view
listed: true
slug: launch-the-client-side-view-ae
description: 
index_title: Launch the client side view
hidden: 
keywords: 
tags: 
---

## Overview

We have developed a Face capture module for both Web and Native integrations to aid in capturing images that closely meet the age estimation and anti-spoofing API requirements.

The Face capture module provides a simplified way to capture a face and provides an image output. However, it does not handle transactions with the age estimation API; these calls should be made separately and are documented in the next section.

---

## Native SDK

The native clients are on our Github, with platform-specific instructions for launching the module.

These native clients offer no UI but instead emit a series of callbacks around the state of the capture, which we suggest using to present real-time feedback to the end user.

[Android](https://github.com/getyoti/yoti-face-capture-android)

[iOS](https://github.com/getyoti/yoti-face-capture-ios)

[React Native](https://github.com/getyoti/react-native-yoti-face-capture)

---

## Web SDK

Our web component for the face capture module is available as a React and Vanilla JS library.

[NPM Package](https://www.npmjs.com/package/@getyoti/react-face-capture)