---
type: page
title: Image requirements
listed: true
slug: image-requirements
description: 
index_title: Image requirements
hidden: 
keywords: 
tags: 
---

{% callout type="info" title="Face capture" %}
Get better results by using our native Face capture module(s).

[auto$](/ai-services-terminals/face-capture-module-fcm)
{% /callout %}

This page is only relevant if you are not able to use our native Face capture module for any reason. In that case, you must ensure your image captures fulfil the following requirements to use our services:

{% synced id="age-estimation-image-requirements" %}
{% /synced %}

There is also a tradeoff between estimation accuracy and camera quality / light conditions, false-negative errors such as face not detected or spoofing attempt detected may be higher than expected due to one or more of the following factors:

{% table %}
| Condition | Description | 
| ---- | ---- | 
| Lighting | Provide UX and guidance to the user. Jump to [auto$](/ai-services-terminals/user-experience) for more information. | 
| Face positioning | Guide the users to place their face in the middle of the photo you are capturing. A near frontal pose with no obstruction to the facial features. The minimum inter ocular distance is 120 pixels. | 
| Camera angle | Please try to get a face-on photo of the user to get the best result. The camera’s field of view is too small to provide suitable context around the facial image captured. | 
| Camera type | The API does not work on infrared cameras. To ensure the best performance we are happy to support your testing when evaluating camera options. | 
| Image cropping | Further image cropping can also reduce the context around the facial image captured. This can negatively impact the ability of the algorithm to compare to other ‘normal’ images in its learned model. | 
| Glare / Blur | Insufficient anti-glare capabilities of either the lens or the glass will make it harder for the anti-spoofing to accurately detect edges around faces. This can negatively impact the ability of the algorithm to compare to other ‘normal’ images in its learned model. | 
| Zoom | Optical zoom effects can reduce the context around the facial image captured. This can negatively impact the ability of the algorithm to compare to other ‘normal’ images in its learned model. A distorted lens structure, such as a ‘fish-eye’ lens which is not how the AI model has been trained. | 
| Image compression | Too much image compression is applied to the captured image which creates ‘artefacts’ and inaccuracies in the image (ideally no more than 90% compression). This can negatively impact the ability of the algorithm to compare to other ‘normal’ images in its learned model. | 
{% /table %}