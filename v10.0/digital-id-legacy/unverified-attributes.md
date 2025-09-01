---
type: page
title: Unverified attributes
listed: true
slug: unverified-attributes
description: 
index_title: Unverified attributes
hidden: 
keywords: 
tags: 
---

If you would like to support customers who have onboarded with Yoti but have not got verified attributes. You can tick the attribute and tick the box below allowing unverified attributes in the Yoti Hub.

{% badge type="info" text="Hint" /%} If you would like to support customers who have onboarded with Yoti using their Aadhaar card, you will need to make sure that the attributes (where applicable) are set to Allow unverified {attribute name}. As an example, please see a subset of the available attributes below where support for unverified has been selected:

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1615325972/v2_2762/rb3rha8zn1bwnozkzoiv.png" caption="Unverified attributes" mode="300" height="1432" width="1120" %}
{% /image %}

Attributes supported from the Aadhaar card:

{% table %}
| Attribute | Description | 
| ---- | ---- | 
| full_name | The user's full name. If family_name/given_names are present, this will be equal to the string ${given_names} + " " + ${family_name}. | 
| gender | Corresponds to the gender on the registered document; will be one of the strings "MALE", "FEMALE", "TRANSGENDER" or "OTHER". | 
| date_of_birth | Date of birth of the user. | 
| structured_postal_Address | The structured postal address of user. | 
{% /table %}