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

Welcome to the developer documentation for integrating our AI Services:

- Age estimation
    - Version 2: This requires a higher quality image, and allows to combine age estimation with our anti-spoofing check.
    - Version 1: This allows a lower quality image, and only performs age estimation.

- Face capture
- Anti-spoofing - This service works best on mobile. This allows to integrate our passive liveness detection as a standalone check.

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

{% badge type="warning" text="Help" /%} If you are still unsure what product to integrate please email [clientsupport@yoti.com](mailto:clientsupport@yoti.com).

---

## Technical overview

The user's image is securely transmitted to the Yoti API (hosted in the United Kingdom and uses TLS 1.3 encryption in transit). 

Optionally you can use Anti-spoofing to add a layer of security to the service and ensure the user is using their own face for estimation. Yoti uses machine learning to train a deep neural network to recognise presentation attacks. This will help prevent malicious users trying to user a fake image to get a higher or lower age estimation than a legitimate attempt would produce.

After the service is performed, the captured facial image is discarded and Yoti returns:

- Predicted age and uncertainty value.
- Anti-spoofing score.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1602180870/29764/hztzzbcgrvzedien5vsg.png" caption="Age estimation overview" mode="responsive" height="196" width="794" %}
{% /image %}

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

## Using Yoti responsibly

We pride ourselves on how we handle our users' data. We use tech for good and enable users to securely prove their identity or age, always being transparent about what happens to their details.

- Be transparent about why you're collecting data and only use this data for those reasons.
- Only collect the information you actually need. Data minimisation is one of the main benefits of Yoti, so people don't have to provide more information than is actually necessary.
- Make sure any information you export to your own systems is stored securely. Data security is at the heart of what we do and we think it should be important to every organisation.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1604402428/72640/nuvgb0f6rqwwufibxklj.png" mode="300" height="376" width="384" %}
{% /image %}