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

Welcome to the developer documentation for integrating the Digital ID app.

Our Digital ID has two ways you can integrate:

{% badge type="custom" text="PORTAL" /%} No need to write any code.

{% badge type="custom" text="SDKS" /%} The SDK integration has advanced features such as creating your own credential and location constraint.

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      You will need to create a Yoti Hub account with an e-mail & password or using the Yoti App on your phone and register your business with Yoti. Click below for more info.
   </div>
   <div class="alert-links"> 
      <a  target="_self" href="https://developers.yoti.com/digital-id/getting-started-v2"> Onboarding with Yoti </a>
   </div>
</div>
{% /html %}

The overview below sets out the entities and data flows involved.

{% badge type="warning" text="Help" /%} If you need any help please contact us [here](https://yoti.force.com/yotisupport/s/contactsupport).

---

## Technical overview

The diagram below describes the login process and how a backend integrated with the Yoti architecture.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1557841032/12870/j5aji8dciamlodmziekk.png" caption="Backend integration process diagram" mode="600" height="1504" width="1244" %}
{% /image %}

Integrating with Yoti lets your users securely share specific details using their Digital ID app. We call these details attributes, the next page goes into detail on what the [auto$](/digital-id/yoti-attributes) are. 

To get started, users need to click a [Yoti button](/digital-id/createbutton) on your website or app. This button opens a full-page overlay on the webpage, showing the details users are about to share.

Once they confirm the share, their details are securely sent to your organisation. You can access them through a backend integration or from the [**Yoti Hub**.](https://hub.yoti.com/login)

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
Yoti offers a free "learn more" page which is included within the button. This will guide your users through on how to scan the QR code.    </div>
    <div class="alert-links"> 
        <a target="_self" href="https://developers.yoti.com/digital-id/createbutton">Enable this feature</a> 
              <a target="_self" href="https://yoti.world/digital-id/">See this feature</a> 
    </div>
</div>
{% /html %}

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1575299208/20473/kgramshxfo4qala15zar.jpg" caption="The steps users take on mobile and desktop." mode="600" height="1150" width="1294" %}
{% /image %}

---

## Feature list

The Digital ID service is very adaptable, please see below for functionality offered.

{% table %}
| Name | Description | 
| ---- | ---- | 
| QR codes | Yoti provides multiple QR code types for users to scan with their Digital ID app including our partnership QR codes. | 
| Retrieve verified attributes | Customer details from a government issued ID is stored as attributes on the Digital ID app. You can request specific verified details and understand which source the attribute came from. | 
| Retrieve unverified attributes | Some customers may not be able to add verified details in the Digital ID app, thus Yoti provides the ability for you to collect attributes unverified if you wish to enable this. | 
| Optional attributes | Some customers may not have all the verified details in the Digital ID app you are requesting. Thus Yoti provides the ability for you to collect attributes the customer does have if you wish to enable this. | 
| Create your own credential | Yoti allows you to issue your own 'attribute' to a Yoti user, with the ability to share, receive and revoke this attribute via the app. | 
| Geolocation | Provide an expected location area where the device should be when doing the share. | 
| Learn more page | This provides a user guide for the user with the QR code. This is a useful tool and free to use! | 
| Remember me ID | Yoti generates a user identifier to your web application. Allowing you to use this attribute as a returning user. | 
| Source constraints | You can choose which type of document you want to retrieve the attribute's from. | 
| Forgerock | Yoti has integrated with [ForgeRock](https://backstage.forgerock.com/marketplace/api/catalog/entries/AWvSfgpmUlk5xAiiw8ns) | 
{% /table %}

---

## Translations supported

Yoti offers translation of our Yoti app in the below languages:

- Brazilian Portuguese (português brasileiro) 🇧🇷
- English 🏴󠁧󠁢󠁥󠁮󠁧󠁿
- French (Français) 🇫🇷
- German (Deutsch) 🇩🇪
- Latin American Spanish (español latinoamericano) 🇪🇸

---

## The user flow

When your user clicks the Yoti button on your website or app, a full-page overlay appears. This tell them exactly what details they'll be sharing and who they'll be sharing them with.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1575299278/20473/viciawwxgwqppmu9tujp.jpg" caption="A diagram of our overlay with numbered areas" mode="full" height="1298" width="1324" %}
{% /image %}

1. Your application's logo and name. Make sure they match what's on the website or app your user has come from.
2. The specific details you're requesting users to share.
3. On desktop browsers: a Yoti QR code that users scan with their Digital ID app. On mobile browsers: a share button that will automatically open the Digital ID app.
4. Your application's contact details and privacy policy. Make sure you provide these.
5. More information for users to find out how Yoti works and how to share details.

Once your user has scanned the QR code on their desktop or tapped the Share details button on their mobile, the Digital ID app automatically presents a share request screen.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1575299328/20473/tssxstmljcgo0egnqkdx.jpg" caption="A diagram of our share details screen in the Yoti app with numbered areas." mode="300" height="952" width="636" %}
{% /image %}

1. Your application's logo and name. Make sure they match what's on the website or app your user has come from.
2. This will only show if you've requested photo authentication in Yoti Hub. If you request this, the user will be asked to scan their face using their front-facing camera.
3. The specific details you are requesting users to share. Any details with a blue tick are verified by Yoti.
4. Tapping Allow shares the requested details with your organisation. The user will then receive a share receipt in their Digital ID app.

Yoti can be used in many different situations. It can be used in scenarios where someone would usually share personal, often private, information with an organisation or another person.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1575299455/20473/mxiacan4oy2nzozyfbaz.jpg" caption="A diagram of a generic user flow using Yoti." mode="full" height="798" width="1458" %}
{% /image %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
        You have control over what you want your users to see before they use Yoti. Please read our page on scenarios to ensue you provide the correct information, using the correct layout.
    </div>
    <div class="alert-links"> 
        <a target="_self" href="https://developers.yoti.com/digital-id/scenario-examples">View scenario examples</a> 
    </div>
</div>
{% /html %}

---

## Video explainer

{% html %}
<div style="padding:56.25% 0 0 0;position:relative;"><iframe src="https://player.vimeo.com/video/939495192?h=6543347b86&badge=0&autopause=0&player_id=0&app_id=58479&dnt=1/embed" allow="autoplay; fullscreen; picture-in-picture" allowfullscreen frameborder="0" style="position:absolute;top:0;left:0;width:100%;height:100%;"></iframe></div>
{% /html %}

---

## Supported browsers

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1608728857/72625/rypdac67giybzfpxz5tg.png" caption="Supported browsers" mode="600" height="1256" width="1178" %}
{% /image %}

---

## Using Yoti responsibly

We pride ourselves on how we handle our users' data. We use tech for good and enable users to securely prove their identity or age, always being transparent about what happens to their details.

- Be transparent about why you're collecting data and only use this data for those reasons.
- Only collect the information you actually need. Data minimisation is one of the main benefits of Yoti, so people don't have to provide more information than is actually necessary.
- Make sure any information you export to your own systems is stored securely. Data security is at the heart of what we do and we think it should be important to every organisation.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1575299497/20473/vwj6x1hjvfni5rzvlho3.jpg" mode="300" height="440" width="438" %}
{% /image %}

$plugin[19ag7p8lxst]