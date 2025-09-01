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

A liveness check is to assess whether the document scan is being performed by a real person, and not someone wearing a mask or an automated system.

{% image url="https://uploads.developerhub.io/prod/kvAX/d9mekm625vpo96mqrthl801ye3yaos9oj9wftjg7mtn1lnyijvakh2uemujdpa5e.gif" caption="Active liveness" mode="300" height="644" width="644" %}
{% /image %}

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

{% image url="https://uploads.developerhub.io/prod/kvAX/kw5cittpb5th85t1g0kiq49m3bq17y46qgr3qxpqcapq4y97v4tk5qwib73bnxnk.png" mode="responsive" height="1236" width="1880" %}
{% /image %}

{% image url="https://uploads.developerhub.io/prod/kvAX/9nhneqyvlr26zbtwybl5vd5wh8xcuc0w49wmiqayc5h34ojzz7o85mdu4wm0smm9.png" mode="responsive" height="1176" width="1856" %}
{% /image %}

3. The user will be presented with an oval or face-shaped overlay depending on the liveness type. They will need to position their face correctly for an automatic scan. If this is not possible, they have to press i'm ready.

{% image url="https://uploads.developerhub.io/prod/kvAX/415dysy336l9ww9r4qbwkc0rryw8o21hsetssd25k1rry2ye4n5e63x0xyu64350.png" caption="User flow: Liveness start" mode="responsive" height="1200" width="1846" %}
{% /image %}

We will provide in-session feedback during the liveness flow.

4. The user will move forwards/backwards or align their face until liveness is complete. They will be presented with a complete screen.

{% image url="https://uploads.developerhub.io/prod/kvAX/8zgt4ojr1ewf8zktr48ajetfpc3g158zkkdqxs4oyqej6f8fkpqc62vykkufjj5w.png" caption="User flow complete screen" mode="responsive" height="1194" width="1854" %}
{% /image %}