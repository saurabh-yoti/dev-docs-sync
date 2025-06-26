---
type: page
title: Address
listed: true
slug: address
description: 
index_title: Address
hidden: 
keywords: 
tags: 
---

It is possible to extend the Identity verification integration by requesting an address check as part of a session.

To receive a customer’s verified address or further proof the customer is who they say they are, they can upload one of the supporting documents:

- Council Tax bill
- Bank statement
- Phone bill
- Utility bill

This section will describe:

- What an address check is.
- Outcome report with recovery suggestions.

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
Yoti recommends that you inform your users that their data might be checked against a third party data source as part of the identity check.    </div>
    <div class="alert-links"> 

   </div>
</div>
{% /html %}

This check will facilitate an extra verification of a user by searching a person’s details against a collated database from various sources worldwide.

Yoti will need to capture the user's address so you will need to allow the following checks:

{% table widths="247,0" %}
| Name | Resources | Manual check available | 
| ---- | ---- | ---- | 
| Supplementary text data extraction | 1x Document Resource | ✅ | 
| ID document text data extraction | 1x Document Resource | ✅ | 
{% /table %}

Note: not all ID documents contain the users address.

### Enhance your check

Add these features to enhance your check for a stronger verification.

{% table widths="0,0,242" %}
| Name | Description | Resources | Manual check available | 
| ---- | ---- | ---- | ---- | 
| Document comparison | If you request your users to upload more than one document we offer the ability to cross check the data | 2x Document Resource | ❌ | 
{% /table %}

We strongly recommend for data extraction you configure ALWAYS go to a manual check for optimum results.

---

## The user flow

1. The user will be presented with a screen to select their issuing country and document type.

{% image url="https://uploads.developerhub.io/prod/kvAX/eiu7emzhasdouvnp5j4hf9vz96nb69n31cbrfbh8o77h81tf13tk1t9r3b5sn74g.png" caption="User flow: Select document type." mode="responsive" height="1154" width="1852" %}
{% /image %}

2. The user will be provided with requirements of the document and context before uploading.

{% image url="https://uploads.developerhub.io/prod/kvAX/9h3sh9mifszu1yd1p8qg0s2aix68r6me80ymgnl8gandiag10e71133kly6mp1ht.png" caption="User flow: Context screen." mode="responsive" height="1180" width="1826" %}
{% /image %}

3. The user will be asked to upload their document.

{% image url="https://uploads.developerhub.io/prod/kvAX/eraqg5t6tu6z5vcq72r1lgodx42y2yi78je9a0cjmna4t44t6uln6xcfetvq0jd3.png" caption="User flow: Upload document" mode="responsive" height="1210" width="1844" %}
{% /image %}

4. The user will be shown the completed screen.

{% image url="https://uploads.developerhub.io/prod/kvAX/opqt79zo7g7zupgsgasibnvercjix8bpaobmfmin2gwz9u3crnfwl9rd5e384n8j.png" caption="User flow: Completed screen." mode="responsive" height="1200" width="1856" %}
{% /image %}

At this point you can redirect the user to a success URL / Error URL.