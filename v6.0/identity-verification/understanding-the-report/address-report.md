---
type: page
title: Address report
listed: false
slug: address-report
description: 
index_title: Address report
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

For the list of checks please see below.

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

For the list of not available reasons please see below.

{% table widths="366" %}
| Yoti Reason | Recovery suggestion | 
| ---- | ---- | 
| NO_VALID_FIELDS\n\nThe uploaded documents did not contain all fields required to do the check. | Ask the user to try again. | 
{% /table %}

###