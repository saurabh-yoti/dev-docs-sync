---
type: page
title: Data Collection
listed: true
slug: data-collection
description: 
index_title: Data Collection
hidden: 
keywords: 
tags: 
---

You can configure what additional personal information you request when a customer gets tested. You can set up Yoti and online form customers to suit your business needs.

You must have the **Settings** permission to be able to manage data collection in the Yoti Testing Platform.

---

## Data minimisation by default

Customers should provide as little personal information to be able to get tested. That’s why by default, Yoti customers only share their photo and Remember Me ID.

---

## Asking for more information

Asking for more information from your Yoti customers will increase the time it takes for them to get set up with Yoti, before they arrive to get tested. A request for verified details may require customers to add one or more ID documents to their Yoti. Think about whether you really need this information for testing purposes.

---

## Configuring your data collection settings

1. Go to **Admin** and select **Settings**.
2. Select **Data Collection.**
3. Under **Data Collection**, find the data you wish to capture and check the checkbox to activate it. The table below lists the available data types.
4. Turn **Symptom questionnaire** On/Off depending if your organisation requires this information or not.
5. Turn **Pre-registered customer flow** On/Off depending if your organisation allows customers to pre-register. You can learn more about this feature in [Customer data pre-registration](https://app.developerhub.io/yoti-developer-documentation/v4.0/yoti-testing-platform/data-collection).

Please note that some data types are necessary for either Yoti app or online form services to function and cannot be switched off in the Yoti Testing Platform.

{% table %}
| Attribute | Yoti app | Online form | 
| ---- | ---- | ---- | 
| Photo | Photos are necessary for the Yoti app to function and cannot be switched off in our systems. | Not available | 
| Remember Me ID | Remember Me IDs are necessary for the Yoti app to function and cannot be switched off in our systems. | Not available | 
| Phone number | You can choose to ask for a phone number from a Yoti customer. | You can choose to ask for a phone number from a web form customer. | 
| Name | You can choose to ask for a name from a Yoti customer. | Names are necessary for the online form to function and cannot be switched off in our systems. | 
| Email address | You can choose to ask for an email address from a Yoti customer. | Email addresses are necessary for the online form to function and cannot be switched off in our systems. | 
| Date of birth | You can choose to ask for a date of birth from a Yoti customer. | You can choose to ask for a date of birth from a web form customer. | 
| Document details\n\n(Passport, Driving licence, National ID, Pass card) | You can choose to ask for document details from a Yoti customer. Including document number, issuing country and date of expiry. | You can choose to ask for document details from a web form customer. Including document number, issuing country and date of expiry. | 
| Address | You can choose to ask for an address from a Yoti customer. | You can choose to ask for an address from a web form customer. | 
| Gender | You can choose to ask for a gender from a Yoti customer. | You can choose to ask for a gender from a web form customer. | 
| Nationality | You can choose to ask for a nationality from a Yoti customer. | You can choose to ask for a nationality from a web form customer. | 
| Health number | You can choose to ask for a health number from a Yoti customer. | You can choose to ask for a health number from a web form customer. | 
{% /table %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Remember Me ID
    </div>
    <div class="alert-text">
        When a user shares their details with you, Yoti generates two user identifiers and provides them to the Yoti Testing Platform. One of these identifiers relates the user globally across your organisation and the second is specific to the Yoti Testing Platform they are sharing with. When a customer’s test sample is scanned again, the same identifier is provided, so that Yoti Testing Platform can recognise them and link them to their specific sample. The same method is used to record all samples collected from this customer, creating an anonymous test history log.
    </div>
    <div class="alert-links"> 

</div>
{% /html %}