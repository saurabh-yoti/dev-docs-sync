---
type: page
title: Set up
listed: true
slug: portal-guide
description: 
index_title: Set up
hidden: 
keywords: 
tags: 
---

Yoti provides a portal that allows you to use our Identity verification service without doing any technical integration.

You will be able to create Identity verification sessions to send to your customers using our new user friendly product without using a line of code!

To get set up you will need to follow these steps:

1. Download the Yoti app.
2. Complete the registration process on our [Yoti Hub.](https://hub.yoti.com/login-organisations)
3. Create an application and choose your configuration setup.
4. Log on to the [portal](https://identity.yoti.com/iam/login)

The below will guide you through step by step on how to get set up.

{% badge type="warning" text="Help" /%} If you need any help please email [clientsupport@yoti.com](mailto:clientsupport@yoti.com).

---

### Supported Browsers

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1603187142/71142/rstg3qyxjlhzssaeqjfm.png" caption="Supported browsers" mode="600" height="216" width="688" %}
{% /image %}

---

## Download Yoti

Below are the download links for our app:

- Download in [App Store](https://apps.apple.com/gb/app/yoti-your-digital-identity/id983980808)
- Download in [Google Play](https://play.google.com/store/apps/details?id=com.yoti.mobile.android.live&amp;hl=en_GB)

Follow our onboarding process, add your official ID document and an email address to your account. Only **one** person from the business needs to onboard with Yoti. 

---

## Register with the hub

1. **[Open Yoti Hub](https://hub.yoti.com/login-organisations)** on a desktop or laptop.
2. Scan the QR code using your Yoti app.
3. Complete the registration on Yoti Hub.

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Jump to
   </div>
   <div class="alert-text" >
      For a step by step guide on how to onboard with the hub head over to the Getting started section.
   </div>
   <div class="alert-links"> 
      <a  target="_self" href="https://developers.yoti.com/yoti/getting-started
                               "> Onboarding with Yoti </a>
   </div>
</div>
{% /html %}

---

## Create an application

Here you will to create an Identity verification application in your Yoti hub. To create your application:-

- Click the **applications** tab in the side menu.
- Choose which product you would like to integrate with, select **Identity verification:**

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1623406298/v2_2762/celvi0kcxavscpr5sbkc.png" caption="Create an application" mode="responsive" height="1358" width="1734" %}
{% /image %}

- After pressing **Proceed**
- Fill in the Details tab - including your application name and logo, then click **Create**.

{% table %}
| Details | Explained | 
| ---- | ---- | 
| Application Name | This is the name of your application in the hub and is used to differentiate between each application in the portal. | 
| Technical contact | This is the contact Yoti can contact you for changes, updates and feedback. | 
{% /table %}

You will now see the following screen:

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1623406385/v2_2762/ztlnwpmvfn2wed1cfxdk.png" caption="Creating an application &gt; Keys" mode="responsive" height="1338" width="1788" %}
{% /image %}

- Click on the **Keys** tab
- Click the Generate keys button, you will be asked whether you want to store the keys.  Click this checkbox and the keys will automatically be managed by Yoti on your behalf. 

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1603126137/71142/ffqyux4zfj6icqxoyakp.png" caption="Creating an application &gt; Keys &gt; Tick box" mode="600" height="842" width="994" %}
{% /image %}

If you ever decide that you no longer want Yoti to store your keys, you will be able to regenerate your keys and uncheck the checkbox.  This will prevent you or your users from being able to view existing data in the portal.

### Choose your configuration set up

Before you start here get familiar with our user view. See what your users would go through by using the following [demo](https://yoti.world/yoti-idv/).

You will be provided with a list of checks that Identity verification provides. 

- Click on **portal preferences.**
- Please tick which checks and tasks you wish to have as part of your user sessions. 

A session represents one end-to-end use of the ID verification service. Each time the ID verification service is initiated (regardless of which specific tasks/checks are required) a new session is created.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1623406742/v2_2762/j3ybs4vvfy4bcmt4awxf.png" caption="Creating an application &gt; Portal Preferences" mode="responsive" height="1498" width="1838" %}
{% /image %}

Below describes the multiple checks Yoti provides for identity verification. We offer a manual check for most of the checks. If you require a manual check please select the following as part of your check:-

{% table %}
| Check type | Description | 
| ---- | ---- | 
| Always | The requested check will always get manually check regardless of the success of the automated check. | 
| Never | The requested check will never get manual checked. | 
| Fallback | The requested check will be manually checked if the automated check fails. | 
{% /table %}

You can select your preference in within each tick box check. 

### Checks explained

If you understand what checks you want, you can skip this section. 

{% table %}
| Name | Manual check available | 
| ---- | ---- | 
| Document authenticity | ✅ | 
| Text extraction | ✅ | 
| Supporting documents | ✅ | 
| Document comparison | ❌ | 
| Address check | ✅ | 
| AML check (COMING SOON) | ❌ | 
| Liveness check | ❌ | 
| Face match check | ✅ | 
{% /table %}

### Request liveness check

A requested check to assess whether the document scan is being performed by a real person, and not someone wearing a mask or an automated system.

You can allocate how many retries you want the user to complete. We recommend a maximum of 3. 

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1623409740/v2_2762/a6chgvifja6io3dlkcch.png" caption="Application &gt; Portal preferences" mode="responsive" height="716" width="1212" %}
{% /image %}

If you are collecting data from the US we highlight recommend you collect biometric consent and add a privacy policy. This is a small tick box in the Verification flow that the user has to click. 

### Request ID document check

A request to assess the characteristics of a document, to determine the validity of the ID document. Yoti will perform multiple checks on a ID document.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1623410013/v2_2762/um33cjng7hqnkiw28yfk.png" caption="Application &gt; Portal preferences" mode="600" height="700" width="954" %}
{% /image %}

You can configure two options here:

1. Decide on capture mode. Users can either upload / take an image of their photo. You can configure which setting you want by ticking the box above.
2. Filter out document types you want to accept. Click on the small arrow under Document 1 and choose your preferences. 

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1623410155/v2_2762/uirqduyogwf1ln9zswtq.png" caption="Application &gt; Portal preferences" mode="responsive" height="620" width="1002" %}
{% /image %}

If you would like to collect two ID documents please click request additional document click Request additonial document.

### Request Face match check

A request to assess whether the user's face matches the face on the ID document. You will need:

- A liveness check
- A document check

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1623410285/v2_2762/gfdd9jso1p9l6ivekzmh.png" caption="Application &gt; Portal preferences" mode="responsive" height="162" width="864" %}
{% /image %}

### Request Text extraction task

A request to obtain the data printed visually on a document, in structured form.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1623410338/v2_2762/f9h4ht3bzswlkekpqt9j.png" caption="Application &gt; Portal preferences" mode="responsive" height="162" width="906" %}
{% /image %}

### Request supplementary documents

Yoti offers the ability to request additional documents to enhance the verification of the user. This could be a

- Council tax bill
- Utility bill
- Phone bill
- Bank statement

Yoti does not perform a verification of the document. 

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1623410458/v2_2762/munvetzqmtuwvelko8cz.png" caption="Application &gt; Portal preferences" mode="responsive" height="620" width="1092" %}
{% /image %}

You can configure two options here:

1. Filter out document types you want to accept. Click on the small arrow under Document 1 and choose your preferences. 
2. You must have text data extraction enabled.

### Request document comparison check

If you request your users to upload more than one document we offer the ability to cross check the data. You must have text extraction on both documents enabled. 

### Request address check

This check will facilitate an extra verification of a user by searching a person’s details against a collated database from various sources worldwide. To complete this check Yoti must be provided with successful data extraction on the ID document with the following data:

- Name
- Date of birth
- Address

### Settings

Here you can configure how long you want the session to be valid for, and how long you want to keep the images / results for. 

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1623410824/v2_2762/ybacicmaoepkcid403cp.png" caption="Portal &gt; Preferences" mode="300" height="614" width="964" %}
{% /image %}

Yoti recommends you keep the data only if necessary. By default we set the session time to live for 1 week and the retention period to 3 months.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1623410851/v2_2762/sozuvqaorrjfuphkiwh5.png" caption="Portal &gt; Preferences" mode="300" height="546" width="906" %}
{% /image %}

### Client view

Here you can configure the user view

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1623410940/v2_2762/xplsv5xfhgjj2kwkqdqc.png" caption="Portal &gt; Preferences" mode="600" height="754" width="1026" %}
{% /image %}

{% table %}
| Configuration | Description | 
| ---- | ---- | 
| Primary colour | Colour of the button on the user session view. | 
| Secondary colour | Coming soon! | 
| Font colour | Change the colour of the font of the user session view. | 
| Locale | Select a translation language. See [](/identity-verification/overview) for translations supported. | 
| Preset issuing country | Allows you to set which country is preset in the user session view. | 
{% /table %}

If you require a manual check please select the following as part of your check:

{% table %}
| Check type | Description | 
| ---- | ---- | 
| Always | The requested check will always get manually check regardless of the success of the automated check. | 
| Never | The requested check will never get manual checked. | 
| Fallback | The requested check will be manually checked if the automated check fails. | 
{% /table %}

After you have decided what checks you want 

- **Save** your settings.
- Press **activate**. 

{% badge type="warning" text="Help" /%} If you are unsure what checks you need please feel free to get in touch with us at [clientsupport@yoti.com](mailto:clientsupport@yoti.com).

### Add users

To add a user and enforce permissions to your portal:- 

- Go to the **portal users** tab

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1623406826/v2_2762/zaesengamxv0dmz84k90.png" caption="Creating an application &gt; Portal Users" mode="responsive" height="648" width="1732" %}
{% /image %}

- Click add new user 
- Type in the person’s email address. 
- Once you add a user, they will get emailed a link to the portal and will need to create an account on the portal. 

By default people that are added to the portal will have the ‘View sessions’ permission.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1603126796/71142/gusdqmglmj2luv5003ik.png" caption="Creating an application &gt; Users &gt; Permissions" mode="300" height="1290" width="830" %}
{% /image %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
Note: Hub users are not automatically added to the Identity verification portal so please add yourself.   <div class="alert-links"> 

    </div>
</div>
{% /html %}

---

## Video explainer

Check out our video walking through all the above:

{% video %}
{% /video %}