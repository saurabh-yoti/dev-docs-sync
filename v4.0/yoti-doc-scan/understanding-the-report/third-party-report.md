---
type: page
title: Third party report
listed: true
slug: third-party-report
description: 
index_title: Third party report
hidden: 
keywords: 
tags: 
---

## Proof of address report

We introduce a new recommendation for proof of address called CONSIDER.

{% table %}
| Recommendation | Reasons | 
| ---- | ---- | 
| APPROVE | At least one match was found. | 
| NOT_AVAILABLE | Not enough information to do the requested check. This could be due to text data extraction failing. | 
| CONSIDER | No records found to check against, or Name and DOB matched but address doesn't. Please see the sub checks for more detail. | 
{% /table %}

### Consider result

For the list of consider reasons please see below.

{% table %}
| Yoti Reason | Description | Recovery suggestion | 
| ---- | ---- | ---- | 
| NO_MATCH_FOUND | Returned if either the name or address fails to return a match. | Ask the user to try again. | 
| ADDRESS_MISMATCH | The address provided did not match the address on record. | Ask the user to check their address is the correct address and to try again. | 
{% /table %}

### Not available reason

{% table %}
| Yoti Reason | Description | Recovery suggestion | 
| ---- | ---- | ---- | 
| NO_VALID_FIELDS | The uploaded documents did not contain all fields required to do the check. | Ask the user to try a different document. | 
{% /table %}

### Sub checks explained

{% table %}
| Yoti Reason | Description | 
| ---- | ---- | 
| name_match | Specifies whether the name has returned a match.\n\nIf FAIL then the overall check recommendation will be CONSIDER with reason “NO_MATCH”. | 
| address_match | Specifies whether the address has returned a match.\n\n\n\nIf FAIL then the overall check recommendation will be CONSIDER with reason “ADDRESS_MISMATCH”. \n\n\n\nIf both _address_match_ and _name_match_ fails, then the reason will be NO_MATCH. | 
| dob_match | Specifies whether the date of birth has returned a match.\n\nThis value will only appear if there was a match, since it’s optional in some cases. | 
{% /table %}

---

## AML report

This feature is coming soon! Come back soon to check it out.