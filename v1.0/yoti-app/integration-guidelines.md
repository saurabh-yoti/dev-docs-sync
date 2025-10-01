---
type: page
title: Integration Guidelines
listed: true
slug: integration-guidelines
description: 
index_title: Integration Guidelines
hidden: 
keywords: 
tags: 
---

Our app can be seamlessly integrated with your website, app or custom product so you can perform secure identity checks. This is what we call a Yoti app integration.You'll be able to request specific details from a user's Yoti app directly from your website or app.

To download a copy of the below please click [here](https://s3-eu-west-1.amazonaws.com/prod.marketing.asset.imgs/integration/190815_Yoti_UsabilityGuidelinesForYotiAppIntegrations_2.0_ab.pdf).

So, what does a Yoti app integration include? Let's cover the basics.

---

## How Yoti app integration works

Integrating with Yoti lets your users securely share specific details using their Yoti app. 

To get started, users need to click a Yoti button on your website or app. This button opens a full-page overlay on the webpage, showing the details users are about to share. 

On a desktop browser, this overlay has a two-dimensional barcode that we ask users to scan with the Yoti app to continue. We use these codes to securely pass on bits of information; they're called Yoti QR codes. 

On a mobile browser, users simply need to tap the Share details button to continue.

Both methods prompt the Yoti app to display the details users are about to share and button to confirm this. 

If a user doesn't have the Yoti app, they'll be redirected to a mobile website with more information and links to download it. 

Once they confirm the share, their details are securely sent to your organisation. You can access them through a backend integration or from your Yoti Hub. 

{% image url="https://image-archive.developerhub.io/image/upload/17868/wdg2ae9knxoggbpo6s5e/1565952702.jpg" mode="responsive" height="1004" width="1152" %}
{% /image %}

### What your users will see on their desktop browser

When your user clicks the Yoti button on your website or app, a full-page overlay appears. This tells them exactly what details they'll be sharing and who they'll be sharing them with. 

{% image url="https://image-archive.developerhub.io/image/upload/17868/nzqwg9d0vnoewkjshxaw/1565952756.jpg" mode="responsive" height="1118" width="1160" %}
{% /image %}

1. Your application's logo and name. Make sure they match what's on the website or app your user has come from.
2. The specific details you're requesting users to share
3. On desktop browsers: a Yoti QR code that users scan with their Yoti app. On mobile browsers: a share button that will automatically open the Yoti app.3 
4. Your application's contact details and privacy policy. Make sure you provide these.
5. More information for users to find out how Yoti works and how to share details. 

### What your users will see in the Yoti app

Once your user has scanned the Yoti QR code on their desktop or tapped the Share details button on their mobile, the Yoti app automatically presents a share request screen. 

{% image url="https://image-archive.developerhub.io/image/upload/17868/owm2mfvcsil0ejsojljx/1565952853.jpg" mode="responsive" height="1172" width="832" %}
{% /image %}

1. Your application's logo and name. Make sure they match what's on the website or app your user has come from.
2. This will only show if you've requested photo authentication in your Yoti Hub. When a user taps Allow, this prompts them to scan their face with their front-facing camera.
3. The specific details you're requesting users to share. Any details with a blue tick are verified by Yoti.
4. Tapping Allow shares the requested details with your organisation. The user will then receive a share receipt in their Yoti app. 

### How to use Yoti responsibly

We pride ourselves on how we handle our users' data. We use tech for good and enable users to securely prove their identity, always being transparent about what happens to their details. We hope you believe in this too. 

- Be transparent about why you're collecting data and only use this data for those reasons. 
- Only collect the information you actually need. Data minimisation is one of the main benefits of Yoti, giving people ownership of their data. 
- Make sure the data you collect is stored safely. Data security is at the heart of what we do and we think it should be important to every organisation. 

{% image url="https://image-archive.developerhub.io/image/upload/17868/mmxwms4rofth6ecqdyc7/1565952938.jpg" mode="300" height="506" width="524" %}
{% /image %}

---

## Where Yoti can be used

Yoti applies to many different situations. It can be used in scenarios where someone would usually share personal, often private, information with an organisation or another person. 

### Use case example 1: Enabling KYC checks and identity verification

{% image url="https://image-archive.developerhub.io/image/upload/17868/e5s8o0p2sebs0e5z00gl/1565953003.jpg" mode="responsive" height="1024" width="1870" %}
{% /image %}

### Use case example 2: Proving age to access age-restricted websites

{% image url="https://image-archive.developerhub.io/image/upload/17868/mabjku2vuzjtmapxku5z/1565953177.jpg" mode="responsive" height="1002" width="1858" %}
{% /image %}

### Use case example 3: Proving age for age-restricted goods online

{% image url="https://image-archive.developerhub.io/image/upload/17868/ndp9q7da2vzbshbl8158/1565953207.jpg" mode="responsive" height="1014" width="1888" %}
{% /image %}

### Use case example 4: Creating verified user accounts to enhance trust and safety

{% image url="https://image-archive.developerhub.io/image/upload/17868/zqhziinqzv57sxnhso7c/1565953264.jpg" mode="responsive" height="988" width="1856" %}
{% /image %}

---

## Ensuring a good experience

We want to make Yoti available to anyone. So it's important that everyone has a smooth experience of Yoti, from start to finish. 

Let's take a look at how to create a clear and simple experience for your users. 

### Anatomy of a user-friendly Yoti integration

We recommend you follow these basic guidelines when you integrate the Yoti app. This is so you can reduce friction, provide your users with valuable information and create a seamless user experience. 

{% image url="https://image-archive.developerhub.io/image/upload/17868/xrzs5va66fouply5vey5/1563459707.png" mode="300" height="678" width="1240" %}
{% /image %}

1. Clearly say what the Yoti button is for. There's a reason you're integrating with Yoti and we'd like you to communicate that with your customers. Sharing identity online, especially using new technology, can make people nervous.
2. The Yoti button prominently. The button should be in clear view. Ideally, you won't need to scroll to see it.
3. Link to the Yoti website.  This provides people with more information about what Yoti is; everything is explained on our own website. There should be a link wherever the Yoti button is. It should direct people to: [https://www.yoti.com](https://www.yoti.com)

{% image url="https://image-archive.developerhub.io/image/upload/17868/e9lyfvf9ykn9idxu03jj/1563459865.png" mode="300" height="1830" width="1408" %}
{% /image %}

1. Add an explanation about what our partnership means for your customers. For example, if you’ve partnered with Yoti for secure ID verification, let your customers know. It will be difficult to build trust if they don’t know who we are. Find the best medium to inform customers about how Yoti is used within your service. This can be a paragraph of text, imagery, a list or even an explainer video (please contact [sdksupport@yoti.com](mailto:sdksupport@yoti.com) for assets).
2. It's okay to give your customers more insight into how Yoti works. Whenever you think it's appropriate, use one of the copy templates described below.

---

## Yoti button: dos and don'ts

Users know and trust the Yoti button. So, it should always be easy to recognise on your website. Please use the provided button design without making any visual changes.

The frontend code snippet we provide must be used as shown in the developer documentation. Don't modify the code or how the button should work. 

{% image url="https://image-archive.developerhub.io/image/upload/17868/gu43bhubjmuuhcbz3jah/1563460350.png" mode="responsive" height="2058" width="1722" %}
{% /image %}

### Yoti button: contextual labels

You should always use a relevant, contextual label with a Yoti button. You can use the following options to fit the terminology of your use case. 

- Prove age with Yoti - Whenever Yoti is being used primarily for age verification.
- Prove identity with Yoti - Whenever Yoti is being used primarily for ID verification.
- Log in with Yoti/Sign up with Yoti - Whenever Yoti is being used for online authentication or as an alternative to an email and password or social login.
- Use Yoti - Fallback option for generic uses.

{% image url="https://image-archive.developerhub.io/image/upload/17868/xusvwto11ulxqaslrbni/1563460446.png" mode="responsive" height="1904" width="1714" %}
{% /image %}

---

## How to talk about Yoti

**Keep it simple**

We like to keep things simple. We’re offering the world a simple and fast way of proving who they are. So, we want that to be reflected in how we talk about ourselves and how others talk about us. 

Concise sentences - Keeping it simple means avoiding long-winded sentences or huge paragraphs to explain who we are.

Avoid jargon - Sometimes it’s necessary to use technical language. But sometimes, it can be confusing. We want everyone to understand who we are and what we do. So, when possible, try to avoid jargon or complex terms that could be replaced with an understandable word or phrase. 

**Be clear**

Clarity is important. We pride ourselves on transparency. Nothing should be ambiguous - we want people to leave with more answers than questions. 

Make instructions clear- Instructions should be clear and concise. For example, creating a Yoti is easy, so we don’t want our steps to be so long and complex that people think otherwise.

Break up big blocks of text - When talking about Yoti, try to use bulleted lists or small snippets of text instead of long paragraphs. Instructions should be set out in a clear and step- by-step structure, usually in a bulleted or numbered format. 

**Be positive**

A negative tone is off-putting and can be, quite frankly, scary. A positive tone is reassuring for your customers and much easier to understand. 

Avoid ambiguity- Be confident and bold when talking about Yoti. A vague tone is negative because it causes doubt. Stay away from uncertain words, like 'might' or 'may'.

Be friendly- We are inclusive and open, so like to make sure we refer to people as 'you' and avoid rigid formality. Don't sound like a robot when explaining who we are because this can be uninviting.

Lead with positivity- Start a sentence off in a positive way when talking about Yoti. Don't create fear around sensitive topics involving personal data. Instead, focus on the benefits and the solutions that Yoti can provide. 

### Rules when addressing Yoti

{% table %}
| Description | Dont | Do | 
| ---- | ---- | ---- | 
| &lt;p&gt;Describe Yoti correctly&nbsp;&lt;/p&gt; | &lt;p&gt;Yoti advisers&lt;br&gt; Identity management application Online tool&nbsp;&lt;/p&gt; | &lt;p&gt;Digital identity platform&lt;br&gt; Your digital identity&lt;br&gt; The new way to prove your identity&nbsp;&lt;/p&gt; | 
| &lt;p&gt;Yoti is a single entity&lt;br&gt; &lt;/p&gt; | &lt;p&gt;Yoti are a digital identity platform Our trusted partners, Yoti&nbsp;&lt;/p&gt; | &lt;p&gt;Yoti is a digital identity platform Our trusted partner, Yoti&nbsp;&lt;/p&gt; | 
| &lt;p&gt;Always use Yoti as a noun, not a verb&nbsp;&lt;/p&gt; | &lt;p&gt;Just go and Yoti this Yotify your ID&nbsp;&lt;/p&gt; | &lt;p&gt;Use Yoti&lt;br&gt; &lt;/p&gt; | 
| &lt;p&gt;Name Yoti QR codes correctly&nbsp;&lt;/p&gt; | &lt;p&gt;Yoti code Yoti QR QR code&nbsp;&lt;/p&gt; | &lt;p&gt;Yoti QR code&nbsp;&lt;/p&gt; | 
| &lt;p&gt;Don’t make exaggeratory claims&nbsp;&lt;/p&gt; | &lt;p&gt;Yoti is the BEST digital identity platform&nbsp;&lt;/p&gt; | &lt;p&gt;Yoti is a digital identity platform&nbsp;&lt;/p&gt; | 
| &lt;p&gt;Don't mention the Yoti app's number of downloads, as this is subject to change&nbsp;&lt;/p&gt; | &lt;p&gt;4 million downloads already&nbsp;&lt;/p&gt; |  | 
| &lt;p&gt;Refer to the Yoti app as free to download and use&lt;br&gt; &lt;/p&gt; | &lt;p&gt;Download the Yoti app&nbsp;&lt;/p&gt; | &lt;p&gt;Download the free Yoti app&lt;br&gt; &lt;/p&gt; | 
| &lt;p&gt;Write Yoti correctly&lt;br&gt; &lt;/p&gt; | &lt;p&gt;YOTI&lt;br&gt; &lt;/p&gt; | &lt;p&gt;Download the free Yoti app&lt;br&gt; &lt;/p&gt; | 
| &lt;p&gt;Always refer to Yoti as Yoti&lt;br&gt; &lt;/p&gt; | &lt;p&gt;Your Own Trusted Identity&nbsp;&lt;/p&gt; | &lt;p&gt;Yoti - Your Own Trusted Identity&nbsp;&lt;/p&gt; | 
| &lt;p&gt;Use a positive tone&nbsp;&lt;/p&gt; | &lt;p&gt;Yoti doesn't let hackers attack your data.&nbsp;&lt;/p&gt; | &lt;p&gt;Yoti protects your data, keeping it safe with 256-bit encryption.&nbsp;&lt;/p&gt; | 
{% /table %}

### Text templates for providing information about Yoti

Please use the following text snippets when you want to share more information about Yoti. Don't rephrase the information already provided.

{% image url="https://image-archive.developerhub.io/image/upload/17868/apr8tzywm1m9etkhhs0d/1563461363.png" mode="responsive" height="1358" width="1884" %}
{% /image %}

---

## How we support your users

Transparency is one of our core values at Yoti. If your users ever have any questions about what Yoti is and how to use it, then we're here to help.

We recommend that you give guidance to your users in the following ways. 

Send them to the Yoti website where we explain what we're all about. 

Get in touch with our 24/7 support team. Direct them to our FAQs.