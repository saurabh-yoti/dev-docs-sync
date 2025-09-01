---
type: page
title: Age estimation
listed: true
slug: age-estimation
description: 
index_title: Age estimation
hidden: 
keywords: 
tags: 
---

Here users will simply look at the camera on a device and have their photo taken.

{% callout type="info" title="Info" %}
This option should be configured with a threshold higher than your age of interest.

Yoti details true positive rates for different ages in the Facial Age Estimation whitepaper which can be found [here](https://www.yoti.com/blog/yoti-age-estimation-white-paper).
{% /callout %}

The image is analysed by an algorithm that has been trained to determine age by analysing facial features. A robust facial age estimation process should also include liveness detection technology to ensure it’s a real person in front of the camera.

Good for:

- People without ID documents
- Global coverage
- Low friction

{% html %}
<div style="padding:56.25% 0 0 0;position:relative;"><iframe src="https://player.vimeo.com/video/647416816?h=beb50a0088&amp;badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=58479&dnt=1" frameborder="0" allow="autoplay; fullscreen; picture-in-picture" allowfullscreen style="position:absolute;top:0;left:0;width:100%;height:100%;" title="AVS_AGE_ESTIMATION_SHORT.mp4"></iframe></div><script src="https://player.vimeo.com/api/player.js"></script>
{% /html %}

If you wish to enable the Age estimation service as an option to perform an age verification service.

{% code %}
{% tab language="json" %}
{
    "type": "OVER",
    "age_estimation": {
        "allowed": true,
        "threshold": 21,
        "level": "PASSIVE"
    },
    "ttl": 900,
    "reference_id": "over_18_example",
    "callback": {
       "auto": true,
       "url": "https://www.yoti.com"
    },
    "notification_url": "https://yourdomain.example/webhook",
    "cancel_url": "https://www.yoti.com",
    "synchronous_checks": true
}
{% /tab %}
{% /code %}

{% table widths="" %}
| Parameter | Types | Description | 
| ---- | ---- | ---- | 
| allowed | true / false | Enable the verification method to be available for the user to use. | 
| threshold | Integer e.g. 30 | Age threshold for under/over age limits. We recommend for this threshold to be more than the age you want to set as your barrier to entry. | 
| level | NONE PASSIVE | The level of anti-spoofing for each age verification method.\n\n\nPASSIVE enables a passive liveness test for age estimation. | 
{% /table %}

For extra security, you can also request a liveness test (level). This is to make sure it’s a real person behind the camera, and not a 2D image, mask or bot. The technology works by processing the image(s) through a sequence of deep neural networks. Each of these examine a different element of the image to look for clues that it might not be a real person.

---

## Liveness explained

### Passive liveness

Passive liveness looks at the texture, depth and edges of a person’s face and their surroundings for signs of spoofing and requires no movement from the user.

{% image url="https://uploads.developerhub.io/prod/kvAX/215zf1f470hsj87zw9qojg7n3p7fns12xhwa578ap3ighsk0ldf9glf5e3hbd6z6.png" caption="Passive liveness" mode="responsive" height="236" width="350" %}
{% /image %}