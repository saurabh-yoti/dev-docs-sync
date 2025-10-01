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

Welcome to the developer documentation for integrating Yoti MyFace, our liveness detection service.

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      You will need to download the Yoti app on your phone and register your business with Yoti.
   </div>
   <div class="alert-links"> 
      <a  target="_self" href="https://developers.yoti.com/yoti/getting-started-hub"> Onboarding with Yoti </a>
      <a  target="_self" href="https://developers.yoti.com/yoti/generating-the-api-keys-hub"> Generate API Keys </a> 
   </div>
</div>
{% /html %}

You can integrate Yoti MyFace as a standalone service, or in conjunction with our age estimation service Yoti Age Scan.  To find out more about Yoti Age Scan head over [here](https://developers.yoti.com/yoti-age-scan). 

The overview below sets out the entities and data flows involved. 

---

## Technical overview of Yoti MyFace

MyFace is a low-friction passive liveness detection service that can be integrated seamlessly into a workflow. It’s a simple process for users, only requiring them to take a selfie. Yoti uses machine learning to train a deep neural network to recognise presentation attacks.

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/nu6iojfl4v7cltyg0ih4/1612431880.png" caption="MyFace" mode="responsive" height="196" width="794" %}
{% /image %}

The user's image is securely transmitted to the Yoti API (hosted in the United Kingdom and secured by TLS 1.2 encryption). The checks employed can be triggered dynamically depending on the confidence score generated from successive checks.

Optionally, you can add our [age estimation](https://developers.yoti.com/yoti-age-scan/getting-started) service with MyFace liveness as they were built to complement each other.

---

## Requirements

The image requirements to use myFace are:

{% table %}
| Condition | Description | 
| ---- | ---- | 
| Quantity | Only one single face in the image. | 
| Image type | Yoti only accepts JPEGs (95 to 100 quality) and PNGs. Please avoid image format conversion to avoid degrading the image quality. Multiple changes will introduce quality losses in the image. | 
| Image resolution | The recommended minimum resolution is 1280 x 720px. The maximum resolution accepted is FullHD 1920 x 1080px. | 
| Colour | The image must be colour (RGB). Yoti does not accept black and white or filtered images. | 
| Size | The minimum image size is 50KB. The maximum image size is 1.5 MB. | 
{% /table %}

There’s a tradeoff between estimation accuracy and camera quality / light conditions, false-negative errors such as face not detected or spoofing attempt detected may be higher than expected due to one or more of the following factors:

{% table %}
| Condition | Description | 
| ---- | ---- | 
| Lighting | Provide guidance to the user. | 
| Face positioning | Guide the users to place their face in the middle of the photo you are capturing. A near frontal pose with no obstruction to the facial features. The minimum inter ocular distance is 120 pixels. | 
| Camera angle | Please try to get a face-on photo of the user to get the best result. The camera’s field of view is too small to provide suitable context around the facial image captured. | 
| Camera type | MyFace does not work on infrared cameras. For best performance we are happy to provide testing when evaluating camera options. | 
| Image cropping | Further image cropping can also reduce the context around the facial image captured. This can negatively impact the ability of the algorithm to compare to other ‘normal’ images in its learned model. | 
| Glare / Blur | Insufficient anti-glare capabilities of either the lens or the glass will make it harder for the anti-spoofing to accurately detect edges around faces. This can negatively impact the ability of the algorithm to compare to other ‘normal’ images in its learned model. | 
| Zoom | Optical zoom effects can reduce the context around the facial image captured. This can negatively impact the ability of the algorithm to compare to other ‘normal’ images in its learned model. A distorted lens structure, such as a ‘fish-eye’ lens, will not work as this is not how the AI model has been trained. | 
| Image compression | Excessive image compression applied to the captured image will create ‘artefacts’ and inaccuracies in the image (ideally use JPEGs images with no lower than 90% quality). This can negatively impact the ability of the algorithm to compare to other ‘normal’ images in its learned model. | 
{% /table %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
Head over to our user experience section to create an optimal experiences for your customers and increase conversion  </div>
    <div class="alert-links"> 
       <a href="https://developers.yoti.com/yoti-myface/user-experience">User experience</a>

    </div>
</div>
{% /html %}

---

## Using Yoti responsibly

We pride ourselves on how we handle our users' data. We use tech for good and enable users to securely prove their identity or age, always being transparent about what happens to their details.

{% image url="https://image-archive.developerhub.io/image/upload/72640/nuvgb0f6rqwwufibxklj/1604402428.png" mode="300" height="376" width="384" %}
{% /image %}

- Be transparent about why you're collecting data and only use this data for those reasons.
- Only collect the information you actually need. Data minimisation is one of the main benefits of Yoti, so people don't have to provide more information than is actually necessary.
- Make sure any information you export to your own systems is stored securely. Data security is at the heart of what we do and we think it should be important to every organisation.