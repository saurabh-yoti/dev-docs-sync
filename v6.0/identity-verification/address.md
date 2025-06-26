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

The user will have the option to upload an image or take a photo, this is configurable in your session creation. Yoti recommends you have both options available.

This section will describe:

- What an address check is.
- The results

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

---

## Address checks

This check will facilitate an extra verification of a user by searching a person’s details against a collated database from various sources worldwide.

Yoti will need to capture the user's address so you will need to allow the following checks:

{% table widths="247,0,0" %}
| Name | Resources | Type | Manual check available | 
| ---- | ---- | ---- | ---- | 
| Supplementary text data extraction | 1x Document Resource | Asynchronous | ✅ | 
| ID document text data extraction | 1x Document Resource | Asynchronous | ✅ | 
{% /table %}

---

## The results

Yoti performs numerous matches in order to generate this report. Yoti will also provide a recommendation for the status of the check:

{% table widths="190" %}
| Recommendation | Reasons | 
| ---- | ---- | 
| APPROVE 🟢 | At least one match was found. | 
| NOT_AVAILABLE 🟠 | Not enough information to do the requested check. This could be due to text data extraction failing. | 
| CONSIDER 🟠 | No records found to check against, or Name and DOB matched but address doesn't. Please see the sub checks for more detail. | 
{% /table %}

{% badge type="success" text="Hint: " /%} Only checks attempted will be shown in the response.

{% table %}
| Yoti Reason | Description | Automated | Result | 
| ---- | ---- | ---- | ---- | 
| name_match | Specifies whether the name has returned a match. | ✅ | If FAIL then the overall check recommendation will be CONSIDER with reason “NO_MATCH”. | 
| address_match | Specifies whether the address has returned a match. | ✅ | If FAIL then the overall check recommendation will be CONSIDER with reason “ADDRESS_MISMATCH”.\n\n\n\nIf both _address_match_ and _name_match_ fails, then the reason will be NO_MATCH. | 
| dob_match | Specifies whether the date of birth has returned a match.\n\nThis value will only appear if there was a match, since it’s optional in some cases. | ✅ | N/A | 
{% /table %}

### Consider result

For the list of consider reasons please see below.

{% table %}
| Yoti Reason | Recovery suggestion | 
| ---- | ---- | 
| NO_MATCH_FOUND | Ask the user to try again. | 
| ADDRESS_MISMATCH | Ask the user to check their address is the correct address and to try again. | 
{% /table %}

### Not available result

If Yoti was unable to perform checks here is a list of the responses we will return:

{% table widths="366" %}
| Yoti Reason | Recovery suggestion | 
| ---- | ---- | 
| NO_VALID_FIELDS\n\nThe uploaded documents did not contain all fields required to do the check. | Ask the user to try again. | 
{% /table %}

---

## Request Address check

If you would like to request this check you can in two ways:

- Use our [portal](https://developers.yoti.com/identity-verification/portal-guide#request-document-comparison-check).
- Use our [SDK ](https://developers.yoti.com/identity-verification/address-check)or [API](https://yoti.world/yoti-public-api/#/Backend%20Endpoints/post_sessions).