---
type: page
title: Integration guide Dev
listed: true
slug: integration-guide-agescan
description: 
index_title: Integration guide Dev
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

### Technical Overview

The user's image is securely transmitted to the Yoti API (hosted in the United Kingdom and secured by TLS 1.2 encryption). After the age estimation is performed, the captured facial image is deleted from Yoti’s servers and Yoti returns a predicted age and uncertainty value.

{% image url="https://image-archive.developerhub.io/image/upload/23577/a9x040wyz3d2vevqn4m6/1575305084.jpg" caption="Yoti Age Scan overview" mode="responsive" height="348" width="1226" %}
{% /image %}

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

Optionally you can use [auto$](/yoti/knowledge-base-agescan) to add a layer of security to the service and ensure the user is using their own face for estimation. This will help prevent malicious users trying to user a fake image to get a higher or lower age estimation than a legitimate attempt would produce.