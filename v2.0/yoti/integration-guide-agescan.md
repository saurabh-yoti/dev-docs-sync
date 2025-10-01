---
type: page
title: Integration guide
listed: true
slug: integration-guide-agescan
description: 
index_title: Integration guide
hidden: 
keywords: 
tags: 
---

The below will guide you through the configuration and implementation steps that are necessary in order to use a secure age-checking service that can estimate a person’s age by looking at their face.

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      You will need the Yoti App on your phone and to have registered your business with Yoti.
   </div>
   <div class="alert-links"> 
      <a target="_self"  href="https://developers.yoti.com/yoti/getting-started-hub"> View Onboarding with Yoti </a>
      <a  target="_self" href="https://developers.yoti.com/yoti/generating-the-api-keys"> View Generate API Keys </a> 
   </div>
</div>
{% /html %}

The integrations steps are as follows, see below or jump straight to the documentation:

[1) Get age estimation](https://developers.yoti.com/yoti/integration-steps-agescan)

---

### Technical Overview

The user's image is securely transmitted to the Yoti API (hosted in the United Kingdom and secured by TLS 1.2 encryption). After the age estimation is performed, the captured facial image is deleted from Yoti’s servers and Yoti returns a predicted age and uncertainty value.

{% image url="https://image-archive.developerhub.io/image/upload/23577/a9x040wyz3d2vevqn4m6/1575305084.jpg" caption="Yoti Age Scan overview" mode="responsive" height="348" width="1226" %}
{% /image %}

Optionally you can use Anti spoofing to add a layer of security to the service and ensure the user is using their own face for estimation. This will help prevent malicious users trying to user a fake image to get a higher or lower age estimation than a legitimate attempt would produce.

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know... 
    </div>
    <div class="alert-text">
        To read more, please see our white paper.
    </div>
    <div class="alert-links"> 
        <a href="https://www.yoti.com/blog/yoti-age-scan-whitepaper/">White paper</a>
   </div>
</div>
{% /html %}