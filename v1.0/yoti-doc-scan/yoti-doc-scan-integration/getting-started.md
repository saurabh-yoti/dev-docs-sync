---
type: page
title: Getting started
listed: true
slug: getting-started
description: 
index_title: Getting started
hidden: 
keywords: 
tags: 
---

Let’s get started on integrating Yoti Doc Scan with your site.

First, you will need to have the free Yoti app on your phone. If you haven’t got it already, you can find it on both [App Store](https://itunes.apple.com/gb/app/yoti-your-digital-identity-app/id983980808) and the [Google Play](https://play.google.com/store/apps/details?id=com.yoti.mobile.android.live).

The integration process starts with onboarding with Yoti to generate some API keys. Please complete the following steps:

1. [Creating a Yoti organisation](/yoti-doc-scan/getting-started#creating-an-organisation)
2. [Creating a Yoti application](/yoti-doc-scan/getting-started#creating-an-application)

These steps are explained in more detail just below.

Then you will need to complete the technical integration using the API keys for Yoti Doc Scan by the following steps:

1. [Generating a session](https://developers.yoti.com/yoti-doc-scan/generating-the-session)
2. [Launching the Yoti Client SDK](https://developers.yoti.com/yoti-doc-scan/launching-the-yoti-client-sdk)
3. [Session retrieval](https://developers.yoti.com/yoti-doc-scan/session-retrieval)
4. [Session media retrieval](https://developers.yoti.com/yoti-doc-scan/session-media-content-retrieval)

---

## [Creating an organisation](https://yoti-developer-documentation.developerhub.io/v1.0/yoti-doc-scan-documentation/yoti-doc-scan-integration-introduction#step-1-creating-an-organisation)

Open the Yoti app on your phone, tap Scan Code and scan the QR code displayed on your desktop screen via the following url:[https://hub.yoti.com/login-organisations](https://hub.yoti.com/login-organisations)

Once there, you will need to fill out a basic form with the following questions:

- Organisation details as shown on the company register for your jurisdiction. This is required for us to verify your company
- Registered company address. This is required as additional verification and to generate a billing address
- Director information. This will consist of the directors full name and email address for verification
- Yoti terms and conditions. If you require a copy of this please contact [onboarding@yoti.com](mailto:onboarding@yoti.com)
- Billing details

Your organisation is now created. Our onboarding team will review your application and be in touch within 2-3 hours during office hours on the status of your application. However, this will not prevent you from starting your integration.

Check out the video below to see how to create an organisation:

{% video %}
{% /video %}

### [Setting up collaborators](https://yoti-developer-documentation.developerhub.io/v1.0/yoti-doc-scan-documentation/yoti-doc-scan-integration-introduction#setting-up-collaborators)

To add collaborators to your organisation:

- Go the to side menu and click people
- Click add administrator
- Fill in the details - please make sure the email address you use to invite the user to your organisation is the same as their email address in their Yoti

Once you have completed this we will authorise your organisation and you can proceed to the next step and create a Yoti application.

{% video %}
{% /video %}

---

## [Creating an application](https://yoti-developer-documentation.developerhub.io/v1.0/yoti-doc-scan-documentation/yoti-doc-scan-integration-introduction#step-2-creating-an-application)

Once you have created your organisation, the next step is to create an application. Head over to [https://hub.yoti.com/login](https://hub.yoti.com/login) on your desktop computer and follow the next steps. Make sure you select your organisation and enter your Hub.

To create your application, head over to the Applications tab on the side menu. If this is your first time creating an application, you will see a short explanation and a 'Get started' button. The main objective is to obtain an SDK ID and a PEM File to use this service.

### [**_Details tab_**](https://yoti-developer-documentation.developerhub.io/yoti-hub/yoti-dashboard#details-tab)

Please fill out your details, Your Yoti application name and logo will be shown on the share screen in the Yoti Doc Scan iframe. Once you have finished filling out your details click the Create button. You will see a notification when this is successful. After completing the details tab, you’ll need to provide information in the other tabs.

### [**_Scenarios tab_**](https://yoti-developer-documentation.developerhub.io/yoti-hub/yoti-dashboard#scenarios-tab)

Scenarios allow you to define different sets of attributes to request from your users, while still using one application. You control the set of attributes to request by specifying a Scenario ID to use at the start of the user journey. Each individual user is uniquely identifiable by their rememberMeId, allowing them to be linked across multiple journeys regardless of the scenario each journey has used.

Give your scenario a useful name, describing your use case and click proceed.

You will then be asked to select which attributes (details) you want to receive from your users. This is not applicable to you however so please just press submit.

_Please note: Not required for the Doc Scan integration_

### [**_Keys tab_**](https://yoti-developer-documentation.developerhub.io/v1.0/yoti-doc-scan-documentation/yoti-doc-scan-integration-introduction#keys-tab)

The next stage is to collect various ID’s and the key pair for your application.

**Application ID*:** This is required for the Yoti button that you’ll add to your web app’s front end code.

**Yoti Client SDK ID:** You will need this on your back­end to initialise the SDK and it is passed in each call to our servers.

**Scenario ID***: This is used to associate the button generator with the appropriate scenario that you wish to use.

_*Please note: Not required for the Doc Scan integration_

You need to download the PEM file containing your private key in order for your app to connect with Yoti. Just click the Generate key pair button in the keys tab to download it. Please keep this safe as this PEM file is essential to Yoti integration.

If you lose or corrupt your PEM file you will be able to generate a new one. Remember, regenerating your key pair will break your current application by invalidating your current PEM file and generated keys. This means you will be unable to decrypt new tokens until these are replaced by the newly-generated ones. Once you have selected all your attributes, you will need to define your callback URL and proceed.

### [**_Activating your application_**](https://yoti-developer-documentation.developerhub.io/v1.0/yoti-doc-scan-documentation/yoti-doc-scan-integration-introduction#activating-your-application)

Once you have completed the above steps, you will be able to activate your Yoti application by clicking the activate button in the top right.

You can track your receipt count at the summary page for the applications.*

_*Currently receipts for Doc Scan are not stored in the Yoti Hub._

### [**_Deleting your application_**](https://yoti-developer-documentation.developerhub.io/v1.0/yoti-doc-scan-documentation/yoti-doc-scan-integration-introduction#deleting-your-application)

To delete your application, click on the application, click the drop down near the edit button and press delete.

There is also an option to deactivate your application which will keep an archive of your receipts and integration as a paused state. Users will not be able to scan the QR code on your integration.

_**Important** - If you delete your application we cannot recover this for you and you will lose all your receipts. Your Yoti integration will also break._

---