---
type: page
title: Integrating Yoti & Receipts
listed: true
slug: integrating-yoti-receipts
description: 
index_title: Integrating Yoti & Receipts
hidden: 
keywords: 
tags: 
---

## Creating a Yoti application

Once you have created your organisation, the next step is to create a Yoti Application. Head over to [https://hub.yoti.com/](https://www.yoti.com/dashboard) on your desktop computer and follow the next steps. Make sure you select your organisation and enter your Hub.

To create your application, click on the Applications tab on the side menu. If this is your first time creating an Application, you will see a short explanation and a Get Started button.

**_Details tab_**

Please fill out your details, your Application name and logo will be shown on the share screen in the Yoti app. Once you have finished filling out your details click the Create button. You will see a notification when this is successful. After completing the details tab, you’ll need to provide information in the other tabs.

**_Scenarios tab_**

Scenarios allow you to request different attributes from your users inside the same Application. 

1. Give your scenario a useful name, describing your use case and click proceed.
2. Select which attributes (details) you want to receive from your users.
3. Enter your call back URL. This will be a subdomain of your previously specified domain.

Once created, you will get a Scenario ID that you can use to guide your user through the appropriate flow in your journey.

{% table %}
| Attributes | Description | Source&nbsp; &nbsp; &nbsp;&nbsp; | 
| ---- | ---- | ---- | 
| Remember me ID | A unique ID that recognises Yoti users returning to your application. You will also receive a Parent Remember me ID which can be used to link users across applications. | Yoti | 
| ID Photo | Photo of the user taken with the Yoti app. | Yoti | 
| Full Name | The user's full name as a string. | ID Document | 
| Given Name(s) | The user's first name and middle names. | ID Document | 
| Family Name | The user's last name. | ID Document | 
| Mobile Number | The user's mobile number. | Manual Entry &amp; OTP | 
| Email Address | The user's email address. | Manual Entry &amp; OTP | 
| Age | - Date of Birth&lt;br&gt;- Verify Condition - Age is Over/Under &lt;b&gt;X&lt;/b&gt; age | ID Document | 
| Address | The user's address. | ID Document | 
| Gender | The user's gender. | ID Document | 
| Nationality | The user's nationality. | ID Document&lt;br&gt; | 
| Photo Authentication | Type of authentication, user will take a selfie. This will not be stored and will occur on the Yoti app during the share. | Yoti | 
{% /table %}

Any given application will have a single Application ID, Client SDK ID and .pem file, but will use different a Scenario ID for each journey you wish to define.

You will be given your Scenario ID once you activate your application. You will also see your Scenario IDs in the scenarios list.

**_Keys tab_**

The next stage is to collect various IDs and the key pair for your application.

{% table %}
| ID Type | Description | 
| ---- | ---- | 
| Application ID | This is required for the Yoti button that you'll add to your web apps front end code.&lt;br&gt; | 
| Yoti Client SDK ID | You will need this on your backend to initialise the SDK and it is passed in each call to our servers.&lt;br&gt; | 
| Scenario ID* | This is used to associate the button generator with the appropriate scenario that you wish to use. | 
{% /table %}

*You will find your Scenario IDs in the Scenarios tab.

You need to download the .pem file containing your private key in order for your app to connect with Yoti. Click the Generate key pair button in the keys tab to download it. 

Please keep this safe as this .pem file is essential to Yoti integration. If you lose or corrupt your .pem file you will be able to generate a new one. Remember, regenerating your key pair will break your current application by invalidating your current .pem file and generated keys. This means you will be unable to decrypt new tokens until these are replaced by the newly-generated ones.

**_Activating your application_**

Once you have completed the above steps, you will be able to activate your Yoti application by clicking the activate button in the top right.

You can track your receipt count on the summary page for the applications.

**_Deleting your application_**

To delete your application, click on the application, click the drop down near the edit button and press delete.

There is also an option to deactivate your application which will keep an archive of your receipts and integration as a paused state. Users will not be able to scan the QR code on your integration until it gets activated again.

Note - if you delete your application we cannot recover this for you and you will lose all your receipts. Your Yoti integration will also break.

---

## Receipts

Whenever details are shared through Yoti, each party involved immediately receives a record of the activity: who they shared with, what was shared, and the date/time.

You will see the receipts of your Applications in the receipts tab ordered by date.  You will need to have your phone connected to Hub in order to view receipts.

We at Yoti can never see your receipts - they are stored encrypted and we have no access to the key needed to decrypt the receipts.

**_Download, filter, delete receipts_**

To download the receipts there is an export to CSV button, this will download all of the receipts in the selected time period. By default we display receipt from the last month.

To filter receipts, you can use our date filter. This will display the receipts from this time period.

You can delete receipts for a certain time period or for a certain user.

To delete receipts by time period, filter the list based on the date range that you want to remove and click the Delete button in the dropdown menu next to Export to CSV.

To delete receipts for a user you will need to find the users Remember Me ID. This can be done via exporting the data and searching for the user by name/unique identifier. Change the filter from Date to Remember Me ID and paste the Remember Me ID in.  You will find the delete button in the dropdown menu next to Export to CSV. 

**_Source and verifiers_**

To view further information about how Yoti has verified the user's details, you can click on the Show sources and verifiers tick box at the top of an individual receipt. 

Please see [Source and verifiers section](https://developers.yoti.com/yoti-app-integration/yoti-attributes-explained#source-and-verifiers) for more information.