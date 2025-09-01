---
type: page
title: Age Estimation
listed: true
slug: age-estimation
description: 
index_title: Age Estimation
hidden: 
keywords: 
tags: 
---

With this method, the users will simply be asked to look at the camera and have their selfie taken to estimate their age.

{% callout type="info" title="Good to know" %}
This option should be configured with a threshold higher than your age of interest.

Yoti details true positive rates for different ages in the Facial Age Estimation whitepaper which can be found [here](https://www.yoti.com/blog/yoti-age-estimation-white-paper/).
{% /callout %}

The image is analysed by an algorithm that has been trained to determine age by analysing facial features. A robust facial age estimation process should also include liveness detection technology to ensure it’s a real person in front of the camera.

Good for:

- People without ID documents
- Global coverage
- Low friction

## Liveness explained

Our liveness technology looks at the texture, depth and edges of a person’s face and their surroundings for signs of spoofing and requires no movement from the user.

{% image url="https://uploads.developerhub.io/prod/kvAX/nb6c9gj2e0u5pdjnn5vorzbf6jk8vxb36mi36m2m90c4txq8j5unxjs2xzysout2.png" mode="responsive" height="236" width="350" %}
{% /image %}