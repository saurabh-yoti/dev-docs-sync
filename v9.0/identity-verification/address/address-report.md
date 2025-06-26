---
type: page
title: Report
listed: true
slug: address-report
description: 
index_title: Report
hidden: 
keywords: 
tags: 
---

Yoti performs numerous matches in order to generate this report. Yoti will also provide a recommendation for the status of the check:

{% table widths="190" %}
| Recommendation | Reasons | 
| ---- | ---- | 
| 🟢  APPROVE | At least one match was found. | 
| 🟠  NOT_AVAILABLE | Not enough information to do the requested check. This could be due to text data extraction failing. | 
| 🟠 CONSIDER | No records found to check against, or Name and DOB matched but address doesn't. Please see the sub checks for more detail. | 
{% /table %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
       Only checks attempted will be shown in the report.
    </div>
    <div class="alert-links"> 
   </div>
</div>
{% /html %}

{% table %}
| Yoti Reason | Description | Automated | Result | 
| ---- | ---- | ---- | ---- | 
| name_match | Specifies whether the name has returned a match. | ✅ | If FAIL then the overall check recommendation will be CONSIDER with reason “NO_MATCH”. | 
| address_match | Specifies whether the address has returned a match. | ✅ | If FAIL then the overall check recommendation will be CONSIDER with reason “ADDRESS_MISMATCH”.\n\n\n\nIf both _address_match_ and _name_match_ fails, then the reason will be NO_MATCH. | 
| dob_match | Specifies whether the date of birth has returned a match.\n\nThis value will only appear if there was a match, since it’s optional in some cases. | ✅ | N/A | 
| deceased | Specifies if the person is deceased. | ✅ | If there is no address_match found this sub_check won't be run. | 
| electoral_roll | Specifies if the person can be found on the electoral roll. | ✅ | If there is no address_match found this sub_check won't be run. | 
| pep_warning | Specifies if there are any warnings related to this person, or if they are a pep. | ✅ | If there is no address_match found this sub_check won't be run. | 
| sanctions_warning | Specifies if the person has been found on the UK HM Treasury financial sanctions list or the OFAC Specially Designated Nationals database. | ✅ | If there is no address_match found this sub_check won't be run. | 
| multiple_sources_match | &gt; Specifies how many data sources the third-party can match the person’s details with. | ✅ | If there is no address_match found this sub_check won't be run. | 
{% /table %}

## Consider report

For the list of consider reasons please see below.

{% table %}
| Yoti Reason | Recovery suggestion | 
| ---- | ---- | 
| NO_MATCH_FOUND | Ask the user to try again. | 
| ADDRESS_MISMATCH | Ask the user to check their address is the correct address and to try again. | 
{% /table %}

## Not available report

If Yoti was unable to perform checks here is a list of the responses we will return:

{% table widths="366" %}
| Yoti Reason | Recovery suggestion | 
| ---- | ---- | 
| NO_VALID_FIELDS\n\nThe uploaded documents did not contain all fields required to do the check. | Ask the user to try again. | 
{% /table %}

---

## Request Address check

If you would like to request this check you can in two ways:

- Use our portal.
- Use our SDK.