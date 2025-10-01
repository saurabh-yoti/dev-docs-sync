---
type: page
title: Create an application
listed: true
slug: create-an-application
description: 
index_title: Create an application
hidden: 
keywords: 
tags: 
---

Yoti provides a portal that allows you to use our Identity verification service without doing any technical integration.

You will be able to create Identity verification sessions to send to your customers using our new user friendly product without using a line of code! Before you can do that, an application needs to be created in the Yoti Hub.

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Jump to
   </div>
   <div class="alert-text" >
      For a step by step guide on how to onboard with the hub head over to the Getting started section.
   </div>
   <div class="alert-links"> 
      <a  target="_self" href="https://developers.yoti.com/dbs-rtw-portal/getting-started
                               "> Onboarding with Yoti </a>
   </div>
</div>
{% /html %}

---

## Log into the Yoti Hub

1. Open the[ Yoti Hub](https://hub.yoti.com/login) on a desktop or laptop.
2. Scan the QR code using your Yoti app.
3. Complete the registration on the Yoti Hub.

---

## Create an application

Here, you will have to create an Identity verification application in the Yoti Hub. To create your application:-

- Click the **applications** tab in the side menu.
- Choose which product you would like to integrate with, select **Identity verification** here.

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/celvi0kcxavscpr5sbkc/1623406298.png" caption="Create an application" mode="responsive" height="1358" width="1734" %}
{% /image %}

- After this, press the **Continue** button**.**
- Fill in the 'Details' tab - including your application name and logo, then click **Create**.

{% table %}
| Details | Explained | 
| ---- | ---- | 
| Application Name | This is the name of your application in the hub and is used to differentiate between each application in the portal. | 
| Technical contact (optional) | This is the contact Yoti can contact you for changes, updates and feedback. | 
{% /table %}

- You will now see the following screen:

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/ztlnwpmvfn2wed1cfxdk/1623406385.png" caption="Creating an application &gt; Keys" mode="responsive" height="1338" width="1788" %}
{% /image %}

- Click on the **Keys** tab.
- Click the 'Generate Key Pair' button, you will be asked whether you want to store the keys.  Click this checkbox and the keys will automatically be managed by Yoti on your behalf. 

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/ioqxjxe7akliwhm4ubbc/1636396903.png" caption="Creating an application &gt; Keys &gt; Tick box" mode="responsive" height="1174" width="1054" %}
{% /image %}

If you ever decide that you no longer want Yoti to store your keys, you will be able to regenerate your keys and uncheck the checkbox.  This will prevent you or your users from being able to view existing data in the portal.

### Choose your configuration set up

Before you start here, get familiar with our user view. See what your users would go through by using the following [demo](https://yoti.world/yoti-idv/).

You will be provided with a list of checks that Identity verification provides. 

- Click on **portal preferences.**
- Please tick which scheme you wish to have as part of your user sessions. 

A session represents one end-to-end use of the ID verification service. Each time the ID verification service is initiated (regardless of which specific scheme) a new session is created.

{% image url="https://uploads.developerhub.io/prod/kvAX/vbnq262kahzc18rsis549bebjb10h206m3kbh92za0vvfis8nvw4oec0kvf6ela5.png" caption="Creating an application &gt; Portal Preferences" mode="responsive" height="685" width="927" %}
{% /image %}

### Settings

Here you can configure how long you want the session to be valid for, and how long you want to keep the images and sensitive data for.

{% image url="https://uploads.developerhub.io/prod/kvAX/eub2vgepskprw4byb7qau3am4fc1baybde7qiqfml9q7q6q37jncor9y4gs5n1u6.png" mode="full" height="372" width="1060" %}
{% /image %}

Yoti recommends you keep the data only if necessary. By default we set the session time to live for 1 week and the retention period to 3 months.

{% image url="https://uploads.developerhub.io/prod/kvAX/sb3vkg8j8ota77sk0rjqszh6onmrn4n7pixwucpnfhsxftwee2s249e9i1unvj02.png" mode="responsive" height="614" width="880" %}
{% /image %}

#### Client view

Here you can configure the user view

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/sm7ny10mvy8yercyehhk/1636397207.png" caption="Portal &gt; Preferences" mode="responsive" height="1054" width="1052" %}
{% /image %}

{% table %}
|  |  | 
| ---- | ---- | 
| Primary colour | Colour of the button on the user session view. | 
| Secondary colour | Coming soon! | 
| Font colour | Change the colour of the font of the user session view. | 
| Locale | Select a translation language. See [Overview](Overview) for translations supported. | 
| Preset issuing country | Allows you to set which country is preset in the user session view. | 
| Success URL | If the session is successfully completed you can redirect the user to a URL. | 
| Error URL | If the session is unsuccessful you can redirect the user to a URL. | 
{% /table %}

#### Mobile Handoff

You can enable a mobile handoff feature which will allow users to complete the session using their mobile devices. This must be on for DBS/RTW and cannot be disabled

{% image url="https://uploads.developerhub.io/prod/kvAX/mexpnk8rnidllrt8j9hqb6bni79ppbpbfy60pzya7qmdm1adounsjae3uoc0f3o5.png" mode="responsive" height="288" width="1396" %}
{% /image %}

## Add Users

To add a user and enforce permissions to your portal:-

- Go to the **portal users** tab

{% image url="https://uploads.developerhub.io/prod/kvAX/xtfi3yky4vik0cm7qnfxacg84rxy8xbrm29n9dgakeonq1z8cybxjpz7f0yqgyhl.png" mode="responsive" height="648" width="1732" %}
{% /image %}

- Click add new user
- Type in the person’s email address.
- Once you add a user, they will get emailed a link to the portal and will need to create an account on the portal.

By default people that are added to the portal will have the ‘View sessions’ permission.

{% image url="https://uploads.developerhub.io/prod/kvAX/x3crmobjxfaxdhgdxv585ofx5wtvx71xur155yxcc4pdbavofjhs8r07mdh25iwf.png" caption="Creating an application &gt; Users &gt; Permissions" mode="responsive" height="706" width="452" %}
{% /image %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
      Hub users are not automatically added to the Identity verification portal, so please add them yourself.
    </div>
</div>
{% /html %}

Every user will receive an email from Yoti. They will then need to register on the portal at [https://identity.yoti.com/iam/create](https://identity.yoti.com/iam/create). The new users will be guided through this via the email they receive.