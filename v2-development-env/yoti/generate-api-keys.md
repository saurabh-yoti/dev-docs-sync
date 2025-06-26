---
type: page
title: Generate API keys Dev
listed: true
slug: generate-api-keys
description: 
index_title: Generate API keys Dev
hidden: 
keywords: 
tags: 
---

Yoti provides you with an onboarding tool to get you up and running with Yoti services.

This is where you will obtain your API keys, add your billing information and more.

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      You need to register your business with Yoti.
   </div>
   <div class="alert-links"> 
      <a target="_self" href="https://developers.yoti.com/yoti/getting-started-hub">Getting started</a>
   </div>
</div>
{% /html %}

**You will learn to how to:**

1. [Create an application](https://developers.yoti.com/yoti/generate-api-keys#creating-a-yoti-application)
2. [Create a scenario](https://developers.yoti.com/yoti/generate-api-keys#create-a-scenario)
3. [Collect keys](https://developers.yoti.com/yoti/generate-api-keys#collect-keys)
4. [Activate your application](https://developers.yoti.com/yoti/generate-api-keys#activating-your-application)

---

## 1. Create a Yoti application

To create your application, click the **applications** tab in the side menu. 

Here you can choose which product you would like to integrate with:

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1576162733/20575/wdycnnndkbdu8q1ur16m.jpg" caption="Creating an application" mode="responsive" height="1462" width="2138" %}
{% /image %}

{% html %}
<div class="alert-GTK">

    <div class="alert-title" id="GTK">

        Good to know

    </div>

    <div class="alert-text">

        If you pick Yoti Doc Scan or Yoti Age Scan, you will fill out a condensed form along with the key generation. 

    </div>

    <div class="alert-links"> 

   </div>

</div>
{% /html %}

After pressing **Proceed,** fill in the **Details** tab - including your application name and logo, then click **Create**.

### Yoti App application creation example

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1576164103/20575/m3tedobmgssao3zv5hom.jpg" caption="Example of Yoti App application creation" mode="responsive" height="1622" width="2022" %}
{% /image %}

### Yoti Doc Scan & Yoti Age Scan application creation example

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1576163732/20575/wwpno1djugoqv1xtswg0.jpg" caption="Example of Yoti Doc Scan or Yoti Age Scan application details" mode="responsive" height="1500" width="2060" %}
{% /image %}

---

## 2. Create your scenario

{% html %}
<div class="alert-GTK">

    <div class="alert-title" id="GTK">

        Good to know

    </div>

    <div class="alert-text">

     Skip this section if you are integrating Yoti Doc Scan or Yoti Age Scan

    </div>

    <div class="alert-links"> 

        <a href="https://developers.yoti.com/yoti/generate-api-keys#collect-keys">Collect Keys</a>

     

   </div>

</div>
{% /html %}

**Scenarios tab**

You will then need to fill out your scenarios. Scenarios allow you to define different sets of attributes to request from your users, while still using one application.

{% html %}
<div class="alert-know">
    <div class="alert-title" id="know">
        Knowledge base
    </div>
    <div class="alert-text">
        Attributes are personal details of a user, like their name, date of birth or address. 

Find out how View Yoti attributes work.
    </div>
    <div class="alert-links"> 
        <a  target="_self" href="https://developers.yoti.com/yoti/knowledge-base-hub#yoti-attributes-explained">View Yoti Attributes explained</a> 
    </div>
</div>
{% /html %}

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1572348655/20575/t58vskimgzkzuflxqkhp.jpg" caption="Creating a scenario" mode="600" height="1538" width="1752" %}
{% /image %}

Give your scenario a useful name, describing your use case and click **Proceed**. You will then be asked to select which attributes (personal details) you want to receive from your users.

---

## 3. Collect Keys

You need to download a PEM file containing your private key in order for your app to connect with Yoti.

 •     Click the Generate key pair button in the Keys tab to download.

•     Please keep this safe as this PEM file is essential to a Yoti integration.

If you lose or corrupt your PEM file you will be able to generate a new one. Regenerating your key pair will break your current application by invalidating your current PEM file and generated keys. This means you will be unable to decrypt new tokens until these are replaced by the newly generated ones.

### Yoti App integration collecting keys

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1572348706/20575/ywd60qbv0ragynm2pssz.jpg" caption="Generating keys and PEM File Yoti Digital ID" mode="600" height="1130" width="1790" %}
{% /image %}

The next stage is to collect various IDs and the key pair for your application.

**Application ID:**- This is required for the Yoti button that you'll add to your web apps front end code.

**Yoti Client SDK ID:**- You will need this on your backend to initialise the SDK and it is passed in each call to our servers.

**Scenario ID:**- This is used to associate the button generator with the appropriate scenario that you wish to use.

### Yoti Doc Scan & Yoti Age Scan collecting keys

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1576164519/20575/uzkoq8qltezeiokuoz5i.jpg" caption="Generating keys and PEM file Yoti Doc Scan or Yoti Age Scan" mode="responsive" height="1126" width="1884" %}
{% /image %}

The next stage is to collect various IDs and the key pair for your application.

**Yoti Client SDK ID** - You will need this on your backend to initialise the SDK and it is passed in each call to our servers. 

---

## 4. Activate your application

Once you have completed the above steps, you will be able to activate your Yoti application by clicking the Activate button in the top right.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1572348772/20575/mcq7o1hln5owczn59kau.jpg" caption="Activating your application" mode="600" height="536" width="1748" %}
{% /image %}

---

## Continue integration

Once you've onboarded your organisation in Yoti Hub and have generated your API keys, you can continue with integrating your chosen Yoti products or services:

{% table %}
| Product | Description | 
| ---- | ---- | 
| **[Yoti app](https://developers.yoti.com/yoti/integration-guide-app)** | Connect with already-verified customers | 
| **[Yoti Doc Scan](https://developers.yoti.com/yoti/integration-guide-sign)** | Identity verification embedded in your website or app. | 
| **[Yoti Age Scan](https://developers.yoti.com/yoti/getting-started-agescan)** | Instant, privacy-friendly age estimation. | 
{% /table %}