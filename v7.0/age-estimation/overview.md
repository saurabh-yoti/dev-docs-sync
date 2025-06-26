---
type: page
title: Overview
listed: true
slug: overview
description: 
index_title: Overview
hidden: 
keywords: 
tags: 
---

Welcome to the developer documentation for integrating Age estimation.

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      You will need the Yoti App on your phone and to have registered your business with Yoti. Click here for more info.
   </div>
   <div class="alert-links"> 
         <a target="_self" href="https://developers.yoti.com/yoti/age-estimation/getting-started">View Onboarding with Yoti</a>
   </div>
</div>
{% /html %}

The overview below sets out the entities and data flows.

Yoti offers two API's to integrate this service:

1. [Age estimation with anti-spoofing API](https://developers.yoti.com/age-estimation/integration-guide).  This service allows you integrate: age estimation, and or a passive anti-spoofing with face capture. This service has high image quality requirements.
2. [Age estimation API](https://developers.yoti.com/age-estimation/request-age). This service allows you to integrate age estimation only. 

{% badge type="warning" text="Help" /%} If you are still unsure what product to integrate please email [clientsupport@yoti.com](mailto:clientsupport@yoti.com).

---

## Technical overview

The user's image is securely transmitted to the Yoti API (hosted in the United Kingdom and uses TLS 1.3 encryption in transit). After the age estimation is performed, the captured facial image is discarded and Yoti returns a predicted age and uncertainty value.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1602180870/29764/hztzzbcgrvzedien5vsg.png" caption="Age estimation overview" mode="responsive" height="196" width="794" %}
{% /image %}

Optionally you can use Anti-spoofing to add a layer of security to the service and ensure the user is using their own face for estimation. Yoti uses machine learning to train a deep neural network to recognise presentation attacks. This will help prevent malicious users trying to user a fake image to get a higher or lower age estimation than a legitimate attempt would produce.

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
        To read more, please see our white paper.

    </div>
    <div class="alert-links"> 
        <a target="_blank" href="https://www.yoti.com/wp-content/uploads/Yoti-Age-Estimation-White-Paper-October-2021-20211026.pdf">Whitepaper</a>
   </div>
{% /html %}

---

## Requirements

The image requirements to use our services are:

{% table widths="133,340" %}
| Condition | Age estimation with anti-spoofing | Age estimation | 
| ---- | ---- | ---- | 
| Quantity | Only one single face in the image. | Only one single face in the image. | 
| Image type | Yoti only accepts JPEGs (95 to 100 quality) and PNGs. Please avoid image format conversion to avoid degrading the image quality. Multiple changes will introduce quality losses in the image. | Yoti only accepts JPEG’s encoded as a base64 image | 
| Image resolution | The recommended minimum resolution is 1280 x 720px. The maximum resolution accepted is FullHD 1920 x 1080px. | The minimum face dimensions we accept is 96 x 96 pixels | 
| Colour | The image must be colour (RGB). Yoti does not accept black and white or filtered images. | The image must be colour (RGB). Yoti does not accept black and white or filtered images. | 
| Size | The minimum image size is 50KB. The maximum image size is 1.5 MB. | Base64 body must be below 100KB (~70KB JPEG) | 
{% /table %}

There’s a tradeoff between estimation accuracy and camera quality / light conditions, false-negative errors such as face not detected or spoofing attempt detected may be higher than expected due to one or more of the following factors:

{% table %}
| Condition | Description | 
| ---- | ---- | 
| Lighting | Provide UX and guidance to the user. Jump to [auto$](/age-estimation/user-experience) for more information. | 
| Face positioning | Guide the users to place their face in the middle of the photo you are capturing. A near frontal pose with no obstruction to the facial features. The minimum inter ocular distance is 120 pixels. | 
| Camera angle | Please try to get a face-on photo of the user to get the best result. The camera’s field of view is too small to provide suitable context around the facial image captured. | 
| Camera type | The API does not work on infrared cameras. To ensure the best performance we are happy to support your testing when evaluating camera options. | 
| Image cropping | Further image cropping can also reduce the context around the facial image captured. This can negatively impact the ability of the algorithm to compare to other ‘normal’ images in its learned model. | 
| Glare / Blur | Insufficient anti-glare capabilities of either the lens or the glass will make it harder for the anti-spoofing to accurately detect edges around faces. This can negatively impact the ability of the algorithm to compare to other ‘normal’ images in its learned model. | 
| Zoom | Optical zoom effects can reduce the context around the facial image captured. This can negatively impact the ability of the algorithm to compare to other ‘normal’ images in its learned model. A distorted lens structure, such as a ‘fish-eye’ lens which is not how the AI model has been trained. | 
| Image compression | Too much image compression is applied to the captured image which creates ‘artefacts’ and inaccuracies in the image (ideally no more than 90% compression). This can negatively impact the ability of the algorithm to compare to other ‘normal’ images in its learned model. | 
{% /table %}

## Using Yoti responsibly

We pride ourselves on how we handle our users' data. We use tech for good and enable users to securely prove their identity or age, always being transparent about what happens to their details.

- Be transparent about why you're collecting data and only use this data for those reasons.
- Only collect the information you actually need. Data minimisation is one of the main benefits of Yoti, so people don't have to provide more information than is actually necessary.
- Make sure any information you export to your own systems is stored securely. Data security is at the heart of what we do and we think it should be important to every organisation.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1604402428/72640/nuvgb0f6rqwwufibxklj.png" mode="300" height="376" width="384" %}
{% /image %}