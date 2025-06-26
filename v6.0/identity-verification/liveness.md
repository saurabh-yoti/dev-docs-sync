---
type: page
title: Liveness
listed: true
slug: liveness
description: 
index_title: Liveness
hidden: 
keywords: 
tags: 
---

If you wish to request a liveness check from the user this section will provide you with all the details to complete this. Each check will provide a report of the result from the liveness check.

Here we describe:

- What is a liveness check.
- The results

---

## Liveness check

A requested check to assess whether the document scan is being performed by a real person, and not someone wearing a mask or an automated system. Whilst the liveness test is being performed Yoti will take 3 images of the user.

You must provide the max number of retries your users can have before the liveness is failed. This must be minimum 1 attempt. Yoti recommends 3 attempts as a max retry number.

{% table %}
| Name | Resources | Type | Manual check available | 
| ---- | ---- | ---- | ---- | 
| Liveness | 1x Liveness Resource | Synchronous | ❌ | 
{% /table %}

---

## The results

Liveness checks can sometimes be difficult for users to perform correctly, as they need to position themselves in front of the camera and move in a particular way. 

{% table widths="123" %}
| Response | Description | 
| ---- | ---- | 
| APPROVE 🟢 | The user has passed the liveness test | 
| REJECT 🔴 | Our result suggests it's likely that the user is an automated program (a 'bot'), or somebody holding a photograph, mask or other disguise in front of the camera. Ensure you have reviewed the document response, if this is approved you can ask your users to try a new session. | 
{% /table %}

As part of the liveness check, Yoti performs the following sub check on the face capture explained below which will either PASS or FAIL.

{% table %}
| Sub check | Description | 
| ---- | ---- | 
| liveness_auth | If FAIL, the check will recommend REJECT with no reason given. | 
{% /table %}

---

## Request a liveness check

If you would like to request this check you can in two ways:

- Use our [portal](https://developers.yoti.com/identity-verification/portal-guide#request-liveness-check).
- Use our [SDK](https://developers.yoti.com/identity-verification/biometric-checking) or [API](https://yoti.world/yoti-public-api/#/Backend%20Endpoints/post_sessions).