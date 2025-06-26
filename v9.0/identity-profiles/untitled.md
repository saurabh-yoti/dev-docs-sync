---
type: page
title: Face Match
listed: true
slug: untitled
description: 
index_title: Face Match
hidden: 
keywords: 
tags: 
---

If you wish to request a face match check from the user this section will provide you with all the details to complete this. Each check will provide a report of the result from the face match check.

Here we describe:

- What is a face match check.
- The outcome and recovery suggestions.

A face match check requests to assess whether the user's face matches the face on the ID document. The user's facial image is obtained from the liveness check, which must be performed first. In the event that a liveness check is not requested, the user will be prompted to capture an image of their face and provide their consent for this.

{% table %}
| Name | Resources | Manual check available | 
| ---- | ---- | ---- | 
| Liveness | 1x Liveness Resource | ❌ | 
| Face match | 1x Doc Resource & 1x Liveness Resource | ✅ | 
{% /table %}

### Enhance your check

Add these features to enhance your check for better results:

{% table widths="0,0,242" %}
| Name | Description | Resources | Manual check available | 
| ---- | ---- | ---- | ---- | 
| Mobile hand off | Start your session in web and allow the user to smoothly move to mobile. | N/A | N/A | 
{% /table %}

---

## The user flow

The face match is done in the background when enabling both the document check and liveness check.