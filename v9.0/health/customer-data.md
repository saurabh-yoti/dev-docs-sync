---
type: page
title: Customer data
listed: true
slug: customer-data
description: 
index_title: Customer data
hidden: 
keywords: 
tags: 
---

Add your customer data here for either:

- Pre registrations
- Invites
- Self-registrations

The customer will receive an email with a link and go through the customer flow. This is documented on the[ testing scheme](https://developers.yoti.com/health/testing-schemes) page.

You can either upload a CSV file or add individuals one by one. The data added is searchable by Date of Birth, Email or Full Name from the collection flow.

## Add an individual

1. Press ADD CUSTOMER

{% image url="https://uploads.developerhub.io/prod/kvAX/hpkzjdj9mkm8a7ghtnyi2c3pryda1o3b4687pj9dn18fve3ivk99f65c4vnfjrp8.png" caption="Customer data &gt; Invites" mode="responsive" height="334" width="3282" %}
{% /image %}

2. Add your customer details

{% image url="https://uploads.developerhub.io/prod/kvAX/4auafghv7os9u28g9xhl7o4lmdk5yaw0le46jy61vw5has1aez4d8o980ld6gue3.png" caption="Customer data &gt; Invites &gt; Add customer" mode="300" height="1154" width="536" %}
{% /image %}

Testing option has the drop down:

- Self registration before visit
- Collect sample remotely
- Home testing with verification

Testing scheme has three drop down options:

- Day 2
- Test to release
- Standard.

3. Add the customer details. They will receive an email and go through the customer flow. 

---

## Upload a file

1. Press UPLOAD FILE
2. Add a CSV

Upload a csv file following this structure:

{% image url="https://uploads.developerhub.io/prod/kvAX/n34qyv4lfj13ldzi8wi19z8pcpnwqyyo3oqfty3pbnviq796hirqbcowsmbsda27.png" caption="CSV Structure" mode="responsive" height="65" width="413" %}
{% /image %}

- full_name
- email
- date_of_birth, should follow this structure: YYYY-MM-DD.
- type supports the following options:
    - SELF_REGISTRATION
    - SELF_SWAB
    - HOME_TEST
    - HOME_TEST_UNVERIFIED

3. Once the file is uploaded, the customers will immediately receive an invite email with their unique url. The table will be updated to display the invites sent.
_