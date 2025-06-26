---
type: page
title: Yoti Age Scan
listed: true
slug: yoti-age-scan
description: 
index_title: Yoti Age Scan
hidden: 
keywords: 
tags: 
---

Yoti Age Scan is a secure age-checking service that can estimate a person’s age by looking at their face. This service has a wide application in the provision of any age-restricted goods and services, both online and in person.

Yoti Age Scan is based on on a machine learning technique known as neural networks which aims to emulate the behaviour of the human brain in order to perform simple tasks like estimating the age of an individual.

Yoti Age Scan is designed with user privacy and data minimisation in mind. It does not require users to register in advance, nor to provide any documentary evidence of their identity. It neither retains any information about users, nor any images of them. It simply estimates their age. However, where the age estimation is sufficiently close to the threshold of interest (for example, within 5 years of 18), the system can be configured to fall back to a method where the user must prove their age by another means (for example, using their Yoti app where their account is anchored with a verified ID document, or a manual check by a member of staff). 

To read more, please see our white paper [here](https://s3-eu-west-1.amazonaws.com/prod.marketing.asset.imgs/yoti-website/Yoti-Age-Scan_Digital.pdf). 

This document provides a technical overview of the different components including a functional brief to further the implementers understanding. This document also covers a step by step guide to completing the integration.

The Yoti Age scan service can provide an API endpoint which will estimate your age using an image - This will provide you back with a predicated age and uncertainty value.

Optionally you can provide a back-ground image to the Yoti service as an anti spoofing feature which is suitable for fixed camera deployments like retail store self checkout machines.

---

## Data privacy, network security

Yoti Age Scan has been designed to be anonymous with data privacy and security as primary considerations. The user does not have to register to use the service nor do they have to provide any information about themselves, they simply present their face in front of the camera. Their image is securely transmitted to the Yoti API (currently hosted in the United Kingdom and secured by TLS 1.2 encryption).  After the age estimation is performed, the captured facial image is deleted from Yoti’s servers.

---

## How to integrate

To use this service, please follow the four steps below:

1. [Download Yoti](/yoti-age-scan/yoti-age-scan#step-1-download-yoti)
2. [Create an organisation](/yoti-age-scan/yoti-age-scan#tep-2-create-an-organisation)
3. [Create an application](/yoti-age-scan/yoti-age-scan#tep-2-create-a-yoti-application)
4. [Setting up an age estimation endpoint](/yoti-age-scan/yoti-age-scan#step-4-setting-up-age-estimation-endpoint)

---

## Step 1: Download Yoti

To start your integration you will need to register your organisation with Yoti. The first step will require you to create an account using the free Yoti app and add your ID document and email address.

If you haven’t got it already, you can find it on both the [App Store](https://itunes.apple.com/gb/app/yoti-your-digital-identity-app/id983980808) and [Google Play](https://play.google.com/store/apps/details?id=com.yoti.mobile.android.live).

Once you have created your Yoti account, head over to sign up at: [https://hub.yoti.com/login-organisations](https://hub.yoti.com/login-organisations) on your desktop computer or laptop.

---

## Step 2: Create an organisation

Open the Yoti app on your phone, tap Scan Code and scan the QR code displayed on your desktop screen via the following url: [https://hub.yoti.com/login-organisations](https://hub.yoti.com/login-organisations)

In order to register your organisation, you will need to fill out a basic form with the following questions:

- Organisation details as shown on the company register for your jurisdiction. This is required for us to verify your company
- Registered company address. This is required as additional verification and to generate a billing address
- Director information. This will consist of the directors full name and email address for verification
- Yoti terms and conditions. If you require a copy of this please contact [onboarding@yoti.com](mailto:onboarding@yoti.com)
- Billing details

Your organisation is now created. Our onboarding team will review your application and be in touch within 2-3 hours during office hours on the status of your application. However, this will not prevent you from starting your integration.

Check out the video below to see how to create an organisation:

{% video %}
{% /video %}

---

---

## Step 3: Creating a Yoti application

Once you have created your organisation, the next step is to create an application. Head to [https://hub.yoti.com/login](https://hub.yoti.com/login) on your desktop computer and follow the next steps. Make sure you select your organisation and proceed to your organisations Hub.

To create your application, click on the Applications tab in the side menu. If this is your first time creating an application, you will see a short explanation and a 'Get started' button. The main objective here is to obtain an SDK ID and a PEM File to use this service.

**_Details tab_**

Your Application name and logo will be shown on the share screen in the Yoti app. Once you have finished filling out your details click the Create button. You will see a notification when this is successful. After completing the details tab, you’ll need to provide information in the other tabs.

### [**_Scenarios tab_**](https://yoti-developer-documentation.developerhub.io/yoti-hub/yoti-dashboard#scenarios-tab)

Scenarios allow you to define different sets of attributes to request from your users, while still using one application. You control the set of attributes to request by specifying a Scenario ID to use at the start of the user journey. Each individual user is uniquely identifiable by their Remember me ID, allowing them to be linked across multiple journeys regardless of the scenario each journey has used.

Give your scenario a useful name, describing your use case and click Proceed.

You will then be asked to select which attributes (details) you want to receive from your users. This is not applicable to you however so please just press submit.

### [**_Keys tab_**](https://yoti-developer-documentation.developerhub.io/v1.0/yoti-doc-scan-documentation/yoti-doc-scan-integration-introduction#keys-tab)

The next stage is to collect various ID’s and the key pair for your application.

{% table %}
| ID Type | Description | 
| ---- | ---- | 
| &lt;b&gt;Application ID*&lt;/b&gt; | &lt;p&gt;This is required for the Yoti button that you’ll add to your web app’s front end code.&lt;/p&gt; | 
| &lt;b&gt;Yoti Client SDK ID&lt;/b&gt; | You will need this on your back­end to initialise the SDK and it is passed in each call to our servers. | 
| &lt;b&gt;Scenario ID*&lt;/b&gt; | &lt;p&gt;This is used to associate the button generator with the appropriate scenario that you wish to use.&lt;/p&gt; | 
{% /table %}

_***Please note**: Not required for the Age Scan integration_

You need to download the PEM file containing your private key in order for your app to connect with Yoti. Just click the Generate key pair button in the keys tab to download it. Please keep this safe as this PEM file is essential to Yoti integration.

If you lose or corrupt your PEM file you will be able to generate a new one. Remember, regenerating your key pair will break your current application by invalidating your current PEM file and generated keys. This means you will be unable to decrypt new tokens until these are replaced by the newly-generated ones. Once you have selected all your attributes, you will need to define your call back URL and proceed.

### [**_Activating your application_**](https://yoti-developer-documentation.developerhub.io/v1.0/yoti-doc-scan-documentation/yoti-doc-scan-integration-introduction#activating-your-application)

Once you have completed the above steps, you will be able to activate your Yoti application by clicking the activate button in the top right.

_**Please note:**__Currently receipts for Age estimation are not stored in the Yoti Hub_

---

## Step 4: Setting up age estimation endpoint

In order to use the Age Scan Service you will need the SDK ID and PEM file from our Yoti Hub to complete this integration. The current requirements for the Age Scan Service are as follows:

- Minimum face size on photo of 96px
- Maximum size of the photo should be ~100KB
- JPEG image format

This API will provide a method to estimate an individual’s age to calculate the age and an uncertainty value (in years)  from a photo. If you require the antispoofing mechanism, please head to [this section](/yoti-age-scan/antispoofing).

### Age Estimation (No Anti-Spoofing)

The URI will take the form:

{% code %}
{% tab language="http" %}
POST /api/v1/age-verification/checks?nonce=(…)&timestamp=(…)
{% /tab %}
{% /code %}

{% table %}
| Parameter | Description | Example | 
| ---- | ---- | ---- | 
| nonce | Unique ID for this request transaction. This should be in GUID form and should be uniquely generated for each request | 23487c75-0d20-457f-918a-c0abe5b1473b&lt;br&gt; | 
| timestamp | A timestamp in milliseconds for the request | 1540457718692&lt;br&gt; | 
{% /table %}

### Authorisation and Headers

All requests to a Yoti API require a form of authorisation. The API requires the following headers:

{% table %}
| Header | Purpose | 
| ---- | ---- | 
| X-Yoti-Auth-Digest | Base64 encoded signed hash of the request, signed using the Key file pair associated with your Yoti Application. Steps to generate are described below.&lt;br&gt; | 
| X-Yoti-Auth-Id | The SDK ID associated with the Yoti Application. | 
| ContentType | The body content type – this will be application/json&lt;br&gt; | 
{% /table %}

The X-Yoti-Auth-Digest should be composed from the following:

- HTTP method, i.e. POST
- URI Path (from /checks onwards)
- Request Body – Encoded representation of the image

These should be appended with an ‘&’. For example:

{% code %}
{% tab language="http" %}
POST&/checks?nonce=b98a5ac6-5336-4594-8690-68a4e8223b0c&timestamp=1541694094210&<Body Omitted>
{% /tab %}
{% /code %}

This should then be signed using the Yoti Application PEM file, and the resulting signature encoded in Base64.

### Request body

{% table %}
| Element | Description | 
| ---- | ---- | 
| data | A base64 encoded representation of the image to test | 
{% /table %}

{% code %}
{% tab language="json" %}
{
  "data": "<Base64 Encoded Image>"
}
{% /tab %}
{% /code %}

### Example request

**Hostname**: Available upon request  at [sdksupport@yoti.com](mailto:sdksupport@yoti.com).

{% code %}
{% tab language="http" %}
POST https://<HOSTNAME>:<PORT>/api/v1/age-verification/checks?nonce=14df1d24-dd6f-4482-8eea-701e7c376ee0&timestamp=1541695312125&<Body Omitted>
{% /tab %}
{% /code %}

**Headers**

{% code %}
{% tab language="http" %}
X-Yoti-Auth-Id: a1c06cbb-e810-4150-bf7a-67073b659f8d
X-Yoti-Auth-Digest: qoMA1Pb8IaC4vv7DzgkZY5tD0hkHT+bV1rnFX3EDMfr3lHilbdZakE....
ContentType: application/json
{% /tab %}
{% /code %}

**Body**

{% code %}
{% tab language="json" %}
{
  "data": " /9j/4AAQSkZJRgABAgAAAQABAAD/2wBDAAgGBgcGBQgHBw……"
}
{% /tab %}
{% /code %}

### Example response

This request will return a HTTP 200 OK if the age can be estimated.

{% code %}
{% tab language="json" %}
{
  "pred_age": 29.7475, //predicted age in years
  "uncertainty": 2.04677 //the uncertainty value in years
}
{% /tab %}
{% /code %}

### Other response codes

{% table %}
| Code | Description | 
| ---- | ---- | 
| 401 | Unauthorised. There is an error in the X-Yoti-Auth-Digest signature or SDK ID&lt;br&gt; | 
| 400 | Bad request - details provided in response body | 
| 403 | InvalidOrgStatus: the organisation status must be PENDING or VERIFIED&lt;br&gt;DisabledApp: the application must be enabled to request the age estimation&lt;br&gt; | 
| 404 | ApplicationNotFound: the application was not found on connect side; | 
| 500 | Internal server error&lt;br&gt; | 
{% /table %}

{% table %}
| Code | Description | 
| ---- | ---- | 
| 1 | Image too big&lt;br&gt; | 
| 2 | Unable to decode image (not a jpeg or wrong base64 string)&lt;br&gt; | 
| 4 | No face detected | 
| 5 | Spoofing attempt detected | 
| 8 | No image detected | 
{% /table %}

---

## [Support](https://developers.yoti.com/yoti-app-integration#support)

If you have any other questions please do not hesitate to contact [sdksupport@yoti.com](mailto:sdksupport@yoti.com).

If you would like an example of the age estimation product in our GitHub please let us know.

_Once we have answered your question we may contact you again to discuss Yoti products and services. If you’d prefer us not to do this, please let us know when you e-mail._