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

{% image url="https://uploads.developerhub.io/prod/kvAX/d9mekm625vpo96mqrthl801ye3yaos9oj9wftjg7mtn1lnyijvakh2uemujdpa5e.gif" caption="Active liveness" mode="300" height="644" width="300" %}
{% /image %}

{% image url="https://uploads.developerhub.io/prod/kvAX/h9xbots542r30io4ifoczumoa96zdjkx1r56c9q5vif18n9i5w9dn9dflq26qp7a.png" caption="Static liveness" mode="set" height="953" width="314" %}
{% /image %}

You must provide the maximum number of retries your users can have, before the liveness is failed. There must be a minimum of 1 attempt. Yoti recommends 3 attempts as a max retry number.

{% table widths="" %}
| Name | Resources | Manual check available | 
| ---- | ---- | ---- | 
| Liveness | 1x Liveness Resource | ❌ | 
{% /table %}

### Liveness types

Yoti provides two types of liveness - Active (Zoom) and Passive (Static). Depending on your type of integration, you might find one of the liveness options more suitable.

- **Active liveness** requires the user to move closer to further away from the screen while centring their face within an Oval. On a Mobile device the user is expected to move their phone closer to their face
- **Passive liveness** requires a single image of the user, captured within an overlay presented on screen

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
2. Yoti will provide an overview of what the liveness entails. There is a 'more about verification' screen which users can also read further.

{% image url="https://uploads.developerhub.io/prod/kvAX/qvf4g1aj1fk3jme5has0e3l6nsk0n0eyoavrqns48fqkloqrxavdaf8attiggble.png" mode="responsive" height="1208" width="1884" %}
{% /image %}

{% image url="https://uploads.developerhub.io/prod/kvAX/m7vbd0zx4mu77d5vepqpazxnac8wdrsamu7cohmeqbegutp91qr4hy486s0t48gq.png" caption="User flow: Pre read for Active liveness" mode="responsive" height="1250" width="1830" %}
{% /image %}

{% image url="https://uploads.developerhub.io/prod/kvAX/el60i40dl16dmk8litukexfizgyz7rhnx5908pxroul39ham9fy7qdi6m9330084.png" caption="User flow: Pre read for Passive liveness" mode="responsive" height="1244" width="1908" %}
{% /image %}

3. The user will be presented with an oval or face-shaped overlay depending on the liveness type. They will need to position their face correctly for an automatic scan. If this is not possible, they have to press i'm ready.

{% image url="https://uploads.developerhub.io/prod/kvAX/obtuwrcuhui38dgyxuqqryraqvwexqvghgvimieecq3ixm22omy6q9h59d9eqa5e.png" caption="User flow: Active liveness start" mode="responsive" height="976" width="1846" %}
{% /image %}

{% image url="https://uploads.developerhub.io/prod/kvAX/1hkfrfp98jul4va4r596fwmb4jdy4bvpn98ing12joba08fqyznzfakb1jns8tki.png" caption="User flow: Passive liveness start" mode="responsive" height="1222" width="1898" %}
{% /image %}

We will provide in-session feedback during the liveness flow. 

4. The user will move forwards/backwards or align their face until liveness is complete. They will be presented with a complete screen. 

{% image url="https://uploads.developerhub.io/prod/kvAX/8zgt4ojr1ewf8zktr48ajetfpc3g158zkkdqxs4oyqej6f8fkpqc62vykkufjj5w.png" caption="User flow complete screen" mode="responsive" height="1194" width="1854" %}
{% /image %}

At this point you can redirect the user to a success URL / Error URL.