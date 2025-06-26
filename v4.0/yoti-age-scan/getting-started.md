---
type: page
title: Getting Started
listed: true
slug: getting-started
description: 
index_title: Getting Started
hidden: 
keywords: 
tags: 
---

Welcome to the developer documentation for integrating Yoti Age Scan.

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      You will need the Yoti App on your phone and to have registered your business with Yoti. Click here for more info.
   </div>
   <div class="alert-links"> 
         <a target="_self" href="https://developers.yoti.com/yoti/getting-started-hub">View Onboarding with Yoti</a>
      <a target="_self" href="https://developers.yoti.com/yoti/generate-api-keys-hub">View Generate API Keys</a> 
   </div>
</div>
{% /html %}

The overview below sets out the entities and data flows involved.

---

## Technical overview of the Yoti Age Scan

The user's image is securely transmitted to the Yoti API (hosted in the United Kingdom and secured by TLS 1.2 encryption). After the age estimation is performed, the captured facial image is deleted from Yoti’s servers and Yoti returns a predicted age and uncertainty value.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1602180870/29764/hztzzbcgrvzedien5vsg.png" caption="Yoti Age Scan overview" mode="responsive" height="196" width="794" %}
{% /image %}

Optionally you can use Anti spoofing to add a layer of security to the service and ensure the user is using their own face for estimation. This will help prevent malicious users trying to user a fake image to get a higher or lower age estimation than a legitimate attempt would produce.

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
        To read more, please see our white paper.

    </div>
    <div class="alert-links"> 
        <a target="_blank" href="https://www.yoti.com/resources/yoti-age-white-paper/">Whitepaper</a>
   </div>
{% /html %}

---

## Requirements

The image requirements to use Age Scan are:

- Yoti only accepts JPEG’s encoded as a base64 image
- Base64 body must be below 100KB (~70KB JPEG)
- The minimum face dimensions we accept is 96 x 96 pixels

There’s a tradeoff between estimation accuracy and camera quality / light conditions, false-negative errors such as face not detected or spoofing attempt detected may be higher than expected due to one or more of the following factors:

{% table %}
| Condition | Description | 
| ---- | ---- | 
| Lighting | Provide UX and guidance to the user. Jump to [this section](https://developers.yoti.com/yoti-age-scan/user-experience) for more information. | 
| Face positioning | Guide the users to place their face is in the middle of the photo you are capturing. A near frontal pose with no obstruction to the facial features. | 
| Camera angle | Please try to get the users photo from face on to get the best result. The camera’s field of view is too small to provide suitable context around the facial image captured. This can negatively impact the ability of the algorithm to compare to other ‘normal’ images in its learned model. Generally ensuring this field of view is sufficient to fit at least 3 times the face size horizontally and 2 times vertically. | 
| Camera type | Yoti Age Scan does not work on infrared cameras. We are seeing acceptable performance on VGA cameras (640x480) with decent lenses in artificial lighting. For best performance we are happy to provide testing when evaluating camera options. | 
| Image cropping | Further image cropping can also reduce the context around the facial image captured. This can negatively impact the ability of the algorithm to compare to other ‘normal’ images in its learned model. Image scaling is the best approach to avoid this. | 
| Resolution | Resolution is not high enough (ideally a minimum of 800x600) to provide adequate image clarity for the age estimation to work. The configuration in place (threshold age and uncertainty of image value) provides a fail-safe to ensure minors are not being passed (false-positives). | 
| Glare / Blur | Insufficient anti-glare capabilities of either the lens or the glass will make it harder for the anti-spoofing to accurately detect edges around faces. This can negatively impact the ability of the algorithm to compare to other ‘normal’ images in its learned model. | 
| Zoom | Optical zoom effects can reduce the context around the facial image captured. This can negatively impact the ability of the algorithm to compare to other ‘normal’ images in its learned model. A distorted lens structure, such as a ‘fish-eye’ lens which is not how the AI model has been trained. | 
| Image compression | Too much image compression is applied to the captured image which creates ‘artifacts’ and inaccuracies in the image (ideally no more than 90% compression). This can negatively impact the ability of the algorithm to compare to other ‘normal’ images in its learned model. | 
|  |  | 
{% /table %}

### Hardware requirements

When using the Yoti API (Using the Yoti Service for image processing) the hardware requirements are as follows:

- CPU - 1GHz CPU x86 or x64
- 1 GB RAM (4GB RAM Recommended)
- Network connectivity

Yoti Age Scan does not work on infrared cameras. We are seeing acceptable performance on VGA cameras (640x480) with decent lenses in artificial lighting. For best performance we are happy to provide testing when evaluating camera options.

Please consult [Yoti](mailto:sdksupport@yoti.com) on these for hosted solution requirements.

---

## Using Yoti responsibly

We pride ourselves on how we handle our users' data. We use tech for good and enable users to securely prove their identity or age, always being transparent about what happens to their details.

- Be transparent about why you're collecting data and only use this data for those reasons.
- Only collect the information you actually need. Data minimisation is one of the main benefits of Yoti, so people don't have to provide more information than is actually necessary.
- Make sure any information you export to your own systems is stored securely. Data security is at the heart of what we do and we think it should be important to every organisation.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1604402428/72640/nuvgb0f6rqwwufibxklj.png" mode="responsive" height="376" width="384" %}
{% /image %}