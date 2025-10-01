---
type: page
title: No code platform (beta)
listed: true
slug: no-code-platform-docscan
description: 
index_title: No code platform (beta)
hidden: 
keywords: 
tags: 
---

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
This product is in the BETA stage. Any feedback on the product would be much appreciated.    </div>
    <div class="alert-links"> 
       <a href="mailto:sdksupport@yoti.com">SDK Support contact</a>

    </div>
</div>
{% /html %}

The Yoti Identity platform allows you to use our Yoti Doc Scan product without doing any technical integration.

You will be able to create Yoti Doc scan sessions to send to your customers using our new user friendly product.

To get set up you will need to follow these steps:

1. [Download and create a Yoti app.](https://developers.yoti.com/yoti/no-code-platform-docscan#download-yoti)
2. [Complete the registration process on our Yoti Hub.](https://developers.yoti.com/yoti/no-code-platform-docscan#register-with-the-hub)
3. [Create an application and choose your configuration setup.](https://developers.yoti.com/yoti/no-code-platform-docscan#choose-your-configuration-set-up)
4. [Log on to the Yoti Identity platform.](https://developers.yoti.com/yoti/no-code-platform-docscan#log-in-to-yoti-identity-platform)

### Supported Browsers

{% image url="https://image-archive.developerhub.io/image/upload/71142/rstg3qyxjlhzssaeqjfm/1603187142.png" caption="Supported browsers" mode="600" height="216" width="688" %}
{% /image %}

---

## Download Yoti

Below are the download links for our app:

[Download in App Store](https://apps.apple.com/gb/app/yoti-your-digital-identity/id983980808)

[Download in Google Play](https://play.google.com/store/apps/details?id=com.yoti.mobile.android.live&amp;hl=en_GB)

Follow our onboarding process, add your official ID document, a mobile number and an email address to your account. Only one person from the business needs to onboard with Yoti. 

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
      <a  target="_self" href="https://developers.yoti.com/yoti/getting-started-hub"> Onboarding with Yoti </a>
   </div>
</div>
{% /html %}

---

## Create an application

Here you will to create a Yoti Doc Scan application in your Yoti hub. To create your application, click the **applications** tab in the side menu.

Here you can choose which product you would like to integrate with, select Doc Scan:

{% image url="https://image-archive.developerhub.io/image/upload/71142/zkwlb0vfrarvqhwc1mfb/1602164366.png" caption="Create an application" mode="responsive" height="732" width="974" %}
{% /image %}

After pressing **Proceed,** fill in the **Details** tab - including your application name and logo, then click **Create**.

{% image url="https://image-archive.developerhub.io/image/upload/71142/idyccev8qr7dxusqwd2v/1602164398.png" caption="Example of Yoti Doc Scan application details" mode="responsive" height="730" width="1058" %}
{% /image %}

You will now see the following screen:

{% image url="https://image-archive.developerhub.io/image/upload/71142/q19shyankutumbjy5tsg/1603126068.png" caption="Creating an application > Keys" mode="responsive" height="339" width="569" %}
{% /image %}

When you are on the Keys tab and click the Generate keys button, you will be asked whether you want to store the keys.  Click this checkbox and the keys will automatically be managed by Yoti on your behalf. 

{% image url="https://image-archive.developerhub.io/image/upload/71142/ffqyux4zfj6icqxoyakp/1603126137.png" caption="Creating an application > Keys > Tick box" mode="600" height="842" width="994" %}
{% /image %}

If you ever decide that you no longer want Yoti to store your keys, you will be able to regenerate your keys and uncheck the checkbox.  This will prevent you or your users from being able to view existing data in the Yoti Identity platform.

### Choose your configuration set up

You will be provided with a list of checks Yoti Identity platform. Please tick which checks and tasks you wish to have as part of your user sessions. A session represents one end-to-end use of the ID verification service. Each time the ID verification service is initiated (regardless of which specific tasks/checks are required) a new session is created.

{% image url="https://image-archive.developerhub.io/image/upload/71142/hskdbeydobn9zmrqsbpv/1603126274.png" caption="Creating an application > Preferences" mode="responsive" height="466" width="874" %}
{% /image %}

A summary of the checks are:

{% table %}
| Feature | Description | Manual check option | 
| ---- | ---- | ---- | 
| Document authenticity | A request to assess the characteristics of a document, to determine the validity of the ID document.\n\n\n\nBy default, this will enable the document authenticity check which is used to determine the validity of the document.\n\n\n\nYou are able to request your user to add multiple ID documents and are able to specify what document types you accept. | N | 
| Liveness | A requested check to assess whether the document scan is being performed by a real person and not someone wearing a mask or an automated system.\n\nYou must provide the max number of retries your users can have before the liveness is failed. This must be at least 1. Yoti recommends 3 as a max retry number. | N | 
| Face match | A request to assess whether the user's face matches the face on the ID document. The user's facial image is obtained from the liveness check, which must be performed first. | Y | 
| Text extraction | A request to obtain the data printed visually on a document, in structured form. | Y | 
| Preferences | The preferences section of the session configuration allows you to customise the look and feel of the session for your users and set basic details such as timeouts.  Where possible we have tried to set sensible defaults for these however they can be adjusted as you think appropriate. | N | 
{% /table %}

If you require a manual check please select the following as part of your check:

{% table %}
| Check type | Description | 
| ---- | ---- | 
| Always | The requested check will always get manually check regardless of the success of the automated check. | 
| Never | The requested check will never get manual checked. | 
| Fallback | The requested check will be manually checked if the automated check fails. | 
{% /table %}

After you have decided what checks you want save your settings and **activate**. 

### Add users

To add a user and enforce permissions to your Yoti identity platform go to the **users** tab when creating a Doc Scan application. 

{% image url="https://image-archive.developerhub.io/image/upload/71142/yg3iw8mvia7gd7srdqey/1603126375.png" caption="Creating an application > Users" mode="responsive" height="348" width="672" %}
{% /image %}

Click **add new user** and type in the person’s email address. Once you add a user, they will get emailed a link to the Yoti Identity platform and will need to create an account on the platform. 

By default people that are added to the platform will have the ‘View sessions’ permission.

{% image url="https://image-archive.developerhub.io/image/upload/71142/gusdqmglmj2luv5003ik/1603126796.png" caption="Creating an application > Users > Permissions" mode="300" height="1290" width="830" %}
{% /image %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
Note: Hub users are not automatically added to the Yoti Identity platform so please add yourself to Yoti Identity platform.    <div class="alert-links"> 

    </div>
</div>
{% /html %}

Check out our video walking through all the above:

{% video %}
{% /video %}

---

## Log in to Yoti Identity Platform

Once you have set your preferences you can now begin using the platform. If you have added yourself to the application created above you should receive an email directing you to the platform.

Log in URL: [https://identity.yoti.com/](https://identity.yoti.com/)

Create an account or scan the QR code. Your email address should be the same as what you inputted in your application. 

{% image url="https://image-archive.developerhub.io/image/upload/71142/sn6k0zmktb7wettxfkyc/1603127218.png" caption="Login Screen" mode="600" height="1478" width="2106" %}
{% /image %}

All users are required to set up 2 factor authentication to access the Yoti Identity platform,  This can either be done as part of one step when using the Yoti app or a popular authentication app such as Google Authenticator or Authy.

Your home page will be a list of applications, click the relevant doc scan application. If this is your first time using the product there will only be one. 

---

## Creating a session

Creating a session in the Yoti Identity platform is straightforward as all of the session configuration has already been defined through the Hub. 

For each session you will need to provide:

- A Name.
- An email address 

This information will **NOT** be verified by Yoti and is used to help you search for the session later on.

Press Create.

{% image url="https://image-archive.developerhub.io/image/upload/71142/z5imgttqy9fj92bwtbl7/1603127429.png" caption="Create a session" mode="600" height="1080" width="1466" %}
{% /image %}

You will need to enter the users name and email address.

{% image url="https://image-archive.developerhub.io/image/upload/71142/sel89qojj7dg2ykjtepo/1603127519.png" caption="Create a session > Enter user details" mode="600" height="924" width="1452" %}
{% /image %}

When you have created a session, you will be see a button on a sessions details page to copy the session link. This will be sent to your user.

{% image url="https://image-archive.developerhub.io/image/upload/71142/og8redaadk4cfbnbn3s6/1603127561.png" caption="Session has started" mode="600" height="1050" width="1472" %}
{% /image %}

This must be completed by the user, if you wish to change any of the tasks and checks you must do this within the session preferences created in the hub. 

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
A user will need to have specific permissions to perform these actions that can be added in Hub.
    </div>
</div>
{% /html %}

## Viewing sessions

If you would like to see progress on your session. Click the session you are interested in:

{% image url="https://image-archive.developerhub.io/image/upload/71142/xqmz37hgle0mxrvoprgm/1603127921.png" caption="Session" mode="responsive" height="780" width="1476" %}
{% /image %}

You can search by email, name or select the session you are interested in.

{% image url="https://image-archive.developerhub.io/image/upload/71142/sbvdhoou7rzoxagmkp61/1603127757.png" caption="Session > Session details" mode="responsive" height="778" width="1480" %}
{% /image %}

You can then expand each of the checks to see the overall results. For example:

{% image url="https://image-archive.developerhub.io/image/upload/71142/ufmbbfj5e8yv3nyx9ztf/1603127826.png" caption="Session > Session details > Passport" mode="600" height="1292" width="1476" %}
{% /image %}

## Results from the session

Once the session has been started the state of the session will be in progress. The state will be shown at the top banner. Below are the different states:

{% table %}
| Value | Description | 
| ---- | ---- | 
| IN PROGRESS | Yoti is still working on tasks and checks for the user's ID. | 
| COMPLETED | Yoti has completed checks and tasks. | 
| EXPIRED | Yoti could not complete the checks and tasks. | 
{% /table %}

 To understand responses and reports from doc scan please head over to the appropriate section:

- [Document Authenticity](https://developers.yoti.com/yoti/understanding-the-report#document-authenticity-report)
- [Liveness](https://developers.yoti.com/yoti/understanding-the-report#liveness-report)
- [Face Match](https://developers.yoti.com/yoti/understanding-the-report#face-match-report)
- [Text extraction](https://developers.yoti.com/yoti/understanding-the-report#text-extraction-report)

The above will explain recommendations Yoti will return. It is at your discretion if you want to overall APPROVE / REJECT a user. Hence at the top of each session there will be an option for you to make a decision on the client session once the session has been completed. 

{% image url="https://image-archive.developerhub.io/image/upload/71142/xdzq5omtdprkvblwd4ft/1603128781.png" caption="Session > Decision" mode="300" height="622" width="1480" %}
{% /image %}

This session will be overall marked with your decision.

---

## Deleting a session

You have two options when deleting the session.  You can either

- Delete the media associated with the session
- Delete the session entirely.  Note: a user will need to have specific permissions to perform these actions that can be added in Hub.

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
A user will need to have specific permissions to perform these actions that can be added in Hub.
    </div>
</div>
{% /html %}

**Deleting the media**

By deleting the media associated with the session, you can remove all of you customer’s PII and still keep the recommendations from Yoti, the session details and the decision you have added for your records.  The check will continue to show up in the session list.

To do this you will need to find the correct session and click through each media item and delete them individually at the moment.  In the future we will allow you to delete it all in one go.

{% image url="https://image-archive.developerhub.io/image/upload/71142/qgl2wugzag7bbobcsxtl/1603128937.png" caption="Session > Session Details > Delete image" mode="600" height="1420" width="2052" %}
{% /image %}

**Deleting the session**

By deleting the session, you will be deleting all records of the session.  This will remove the session from the session list and delete all media as well as the recommendations from Yoti, the session details and the decision you have added.

To do this you will need to find the correct session and click delete. 

{% image url="https://image-archive.developerhub.io/image/upload/71142/gw3vqc3kvzjvqnw7u8ew/1603128860.png" caption="Session details > Delete session" mode="600" height="1284" width="2068" %}
{% /image %}

---

## Log out

To log out of the Yoti Identity platform click the menu button in the top right corner of the page and click on the log out button. If you do not log out your account will stay logged in for 24 hours until it auto logs you out. 

{% image url="https://image-archive.developerhub.io/image/upload/71142/ng8bxnqbncfg1o8kawqb/1603129016.png" caption="Logout" mode="300" height="518" width="428" %}
{% /image %}