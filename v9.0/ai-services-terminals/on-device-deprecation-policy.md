---
type: page
title: Deprecation policy
listed: true
slug: on-device-deprecation-policy
description: 
index_title: Deprecation policy
hidden: 
keywords: 
tags: 
---

This page provides information on the deprecation policy associated with our On-Device AI services product. 

The deprecation/expiry date for each version is specified within the docker image that is distributed. When starting the on-device docker image, it will log this expiry date with different severity levels depending on how close we are to it.

You should migrate to a supported version before the end of its deprecation period, as the docker image will shut down if the date has passed.

The following table lists the available versions and their support cycle:

{% table widths="" %}
| Version | Deprecation Date | End of life | 
| ---- | ---- | ---- | 
| V1-beta-2 | 2025-05-13 | 2025-05-13 | 
| V1 | 2025-10-28 | 2025-10-28 | 
{% /table %}