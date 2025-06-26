---
type: page
title: Integration guide
listed: true
slug: integration-guide
description: 
index_title: Integration guide
hidden: 
keywords: 
tags: 
---

There are four steps to follow to integrate the Identity verification SDK:

1. Install the SDK
2. Create the session
3. Launch the user view
4. Retrieve the results

This section will explain how to install the SDK. 

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      You will need to access your Yoti Hub account with an e-mail & password or using the Yoti mobile app and to have registered your business with Yoti. Click below for more info.
   </div>
   <div class="alert-links"> 
         <a target="_self" href="https://developers.yoti.com/yoti/identity-verification/getting-started">View Onboarding with Yoti</a>
   </div>
</div>
{% /html %}

---

## Installing the SDK

Please use our Yoti SDKs to automatically build the relevant session for you. First you will need the following information about your application from [Yoti Hub](https://hub.yoti.com/login):

- Yoti SDK ID
- Your application key pair.

The Yoti SDKs are available via popular dependency management systems. Further details can be found on the pages of the [auto$](/identity-verification/quick-start).

{% code %}
{% tab language="javascript" %}
npm install -S -E yoti
{% /tab %}
{% tab language="java" %}
// If you are using Maven, add the following dependency:
<dependency>
    <groupId>com.yoti</groupId>
    <artifactId>yoti-sdk-api</artifactId>
    <version>3.8.0</version>
</dependency>

// If you are using Gradle, add the following dependency:  
implementation group: 'com.yoti', name: 'yoti-sdk-api', version: '3.8.0'
{% /tab %}
{% tab language="php" %}
// Get the Yoti PHP SDK library via a Composer package
composer require yoti/yoti-php-sdk
{% /tab %}
{% tab language="python" %}
pip install yoti
{% /tab %}
{% tab language="csharp" %}
// To install the Yoti NuGet package you will need to install NuGet.
// To import the latest Yoti SDK into your project, enter the following
// command from NuGet Package Manager Console in Visual Studio:

Install-Package Yoti

// For other installation methods, see https://www.nuget.org/packages/Yoti
{% /tab %}
{% tab language="go" %}
// As of version 2.4.0, modules are used. This means it's not necessary to get a copy or fetch all dependencies 
// as instructed below, as the Go toolchain will fetch them as necessary. 
// You can simply add a `require github.com/getyoti/yoti-go-sdk/v3` to go.mod.
// To download and install the Yoti SDK and its dependencies, run the following command from your terminal:

go get "github.com/getyoti/yoti-go-sdk/v3"
{% /tab %}
{% /code %}