---
type: page
title: Database
listed: false
slug: database
description: 
index_title: Database
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
      This feature is not available via our UX yet.
    </div>
    <div class="alert-links"> 

   </div>
</div>
{% /html %}

Here you can verify your users name, date of birth and address against a credit reference agency database.

In some countries, users will be on a database if they have signed a credit agreement. This may exclude those in lower income groups or younger adults and students.

Good for:

- Background checks
- Specific countries

The user will be asked to prove their age using your name, date of birth and address.

Yoti will send these details to a credit reference agency provider to confirm they are accurate and obtain or confirm your date of birth.

You can receive:

- If you are ‘over’ or ‘under’ their age requirement

We never store or share your details with anyone other than the provider.

If you wish to enable the database check service as an option to perform an age verification service. The database check involves sending a POST request to our API with some of the users personal information sent in the request body. This information is compared to a CRA provider to determine if the user is over 18. (important) this check will only confirm if the user is over/under 18 no threshold can be set

{% code %}
{% tab language="http" %}
POST https://age.yoti.com/api/v1/address/background
{% /tab %}
{% /code %}

## Headers explained

The following elements are needed in the header:

{% table %}
| Header | Description | 
| ---- | ---- | 
| Yoti-Sdk-Id | Your unique Sdk id | 
| Authorization | Your API key (bearer token) | 
{% /table %}

## Body explained

All fields are mandatary. 

{% code %}
{% tab language="json" %}
{
   "first_name": "John",
   "last_name": "Doe",
   "country": "GB",
   "address_lines": [
      "address_line1",
      "address_line2",
      "address_line3"
   ],
   "postal_code": "postcode",
   "date_of_birth": "mm-dd-yyyy"
}
{% /tab %}
{% /code %}

## Response

{% code %}
{% tab language="json" %}
{
   "status": "COMPLETE",
   "result": true,
   "age": 18,
   "method": "ADDRESS",
   "type": "OVER"
}
{% /tab %}
{% /code %}