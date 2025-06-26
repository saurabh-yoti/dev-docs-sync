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

If you wish to request a liveness check from the user, this section provides you with all the details to complete this. Each check will provide a report of the result from the liveness check.

Here we describe:

- What is a liveness check.
- Types of liveness.
- The outcome and recovery suggestions.

A liveness check is to assess whether the document scan is being performed by a real person, and not someone wearing a mask or an automated system. Whilst the liveness test is being performed, Yoti will take 3 images of the user.

{% image url="https://uploads.developerhub.io/prod/kvAX/d9mekm625vpo96mqrthl801ye3yaos9oj9wftjg7mtn1lnyijvakh2uemujdpa5e.gif" caption="Active liveness" mode="300" height="644" width="644" %}
{% /image %}

You must provide the maximum number of retries your users can have, before the liveness is failed. There must be a minimum of 1 attempt. Yoti recommends 3 attempts as a max retry number.

{% table %}
| Name | Resources | Manual check available | 
| ---- | ---- | ---- | 
| Liveness | 1x Liveness Resource | ❌ | 
{% /table %}

### Liveness types

Yoti provides two types of liveness - Active (or Zoom) and Passive (or Static). Depending on your scenario, you might find one of the liveness options more suitable.

- **Active liveness** requires a user to move their face closer and farther in an attempt to capture liveness in both the smaller and larger ovals presented on the screen.
- **Passive liveness** requires a user to align their face in the overlay presented with an outline of a face.

### Enhance your check

Add these features to enhance your check for better results

{% table widths="0,0,242" %}
| Name | Description | Resources | Manual check available | 
| ---- | ---- | ---- | ---- | 
| Mobile hand off | Start your session in web and allow the user to smoothly move to mobile. | N/A | N/A | 
| Liveness attempts | Increase the number of liveness attempts you allow a user to try. | N/A | ❌ | 
{% /table %}

Common causes for liveness failure include (with suggestions to improve):

- Lighting that's too dark or bright - Change position to have clear light in front and reduce background lighting
- Geometric backgrounds - Perform the liveness in front of a plain background
- Glare - Make sure your camera lens is clear and avoid having reflective surfaces in frame
- Angle - Ensure you're level with the camera and looking straight
- Eye contact - Try to look at or near the camera and that your eyes are visible.

---

## User Flow

1. The user will be prompted to provide their consent.

{% image url="https://uploads.developerhub.io/prod/kvAX/t2ki58j06fgvy176bj8nz4bzpglwu44zi7smzu4v246dzmtpk4x66apkeqz5i5n7.png" caption="User flow: Consent screen" mode="responsive" height="1194" width="1860" %}
{% /image %}

2. Yoti will provide an overview of what the liveness entails. There is a 'more about verification' screen which users can also read further.

{% image url="https://uploads.developerhub.io/prod/kvAX/uamc5ch0k1westm8ww0hg9uhzq4hvjo99v13zvgg33eqf3lcdkolqo5wc6x5m3jn.png" caption="User flow: Pre read for liveness" mode="responsive" height="1188" width="1830" %}
{% /image %}

3. The user will be presented with an oval or face-shaped overlay depending on the liveness type. They will need to position their face correctly for an automatic scan. If this is not possible, they have to press i'm ready.

{% image url="https://uploads.developerhub.io/prod/kvAX/415dysy336l9ww9r4qbwkc0rryw8o21hsetssd25k1rry2ye4n5e63x0xyu64350.png" caption="User flow: Liveness start" mode="responsive" height="1200" width="1846" %}
{% /image %}

We will provide in-session feedback during the liveness flow. 

4. The user will move forwards/backwards or align their face until liveness is complete. They will be presented with a complete screen. 

{% image url="https://uploads.developerhub.io/prod/kvAX/8zgt4ojr1ewf8zktr48ajetfpc3g158zkkdqxs4oyqej6f8fkpqc62vykkufjj5w.png" caption="User flow complete screen" mode="responsive" height="1194" width="1854" %}
{% /image %}

At this point you can redirect the user to a success URL / Error URL.