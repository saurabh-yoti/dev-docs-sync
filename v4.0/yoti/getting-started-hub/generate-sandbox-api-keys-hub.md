---
type: page
title: Generate Sandbox API Keys
listed: true
slug: generate-sandbox-api-keys-hub
description: 
index_title: Generate Sandbox API Keys
hidden: 
keywords: 
tags: 
---

Yoti provides a sandbox for the [Yoti App](https://developers.yoti.com/yoti/getting-started-app) and [Doc Scan](https://developers.yoti.com/yoti/getting-started-docscan) integration.

PLEASE NOTE: Our mobile SDKs (iOS/Android/React Native) do not support Sandbox Keys.

{% html %}
<div class="alert-BYS">

   <div class="alert-title" id="BYS">

      Before you start

   </div>

   <div class="alert-text" >

      You will need the Yoti app on your phone and to have registered your business with Yoti.

     We also recommend familiarising yourself with the Yoti integrations to understand the data flow.

   </div>

   <div class="alert-links"> 

      <a target="_self" href="https://developers.yoti.com/yoti/getting-started-hub">Getting Started</a> 

      <a target="_self" href="https://developers.yoti.com/yoti-app/integration-guide-app">Yoti App Integration Guide</a> 
      <a target="_self" href="https://developers.yoti.com/yoti-doc-scan/integration-guide-docscan">Yoti Doc Scan Integration Guide</a> 

   </div>

</div>
{% /html %}

To make a start log into the [Yoti Hub](https://hub.yoti.com/) and make sure you are within your verified organisation by clicking your organisation post login.

{% image url="https://image-archive.developerhub.io/image/upload/27268/yjlqzg82qdyeuz1syiay/1585242508.jpg" caption="Click your organisation" mode="300" height="470" width="602" %}
{% /image %}

Once logged in, choose '**Sandbox**' from the navigation bar.

{% image url="https://image-archive.developerhub.io/image/upload/27268/xqpdk2belqzeuxray6d2/1585242548.jpg" caption="Login > Sandbox" mode="300" height="992" width="580" %}
{% /image %}

Select **GET STARTED** to create your Sandbox application, create the keys on the right tab, Yoti App or Yoti Doc Scan. 

{% image url="https://image-archive.developerhub.io/image/upload/27268/stmkxnq15iyhz2aiuexq/1585242582.jpg" caption="Login > Sandbox > Get started" mode="responsive" height="382" width="1194" %}
{% /image %}

Enter a sandbox application name and hit **SAVE** to generate a Sandbox ID and Keypair.

{% image url="https://image-archive.developerhub.io/image/upload/27268/pjm8aioymuidpojfhjis/1585242620.jpg" caption="Login > Sandbox > Get started > Keys" mode="responsive" height="176" width="1632" %}
{% /image %}

Take note of your **Sandbox Client SDK ID**, and hit **GET KEYS** to generate your keypair. You will only need your private key (**privateKey.pem)** to use the Yoti app sandbox.

{% html %}
<div class="alert-SAND">
    <div class="alert-title" id="SAND">
    <i _ngcontent-cvo-c21="" class="fas fa-external-link-alt" style="margin-left: -35px; margin-right: 15px"></i>  
      Sandbox
    </div>
    <div class="alert-text">
       Head over to learn how to create a sandbox session.
    </div>
    <div class="alert-links"> 
              <a href="/yoti-app/sandbox-app">Yoti App Sandbox</a>

        <a href="https://developers.yoti.com/yoti-doc-scan/sandbox-docscan">Yoti Doc Scan Sandbox</a>
    </div>
</div>

</div>
{% /html %}