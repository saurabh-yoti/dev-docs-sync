---
type: page
title: AML
listed: true
slug: aml
description: 
index_title: AML
hidden: 
keywords: 
tags: 
---

It is possible to extend the Identity verification integration by requesting an watchlist, PEPs and sanctions check as part of a session.

This section will describe:

- What an AML check is.
- Outcome and recovery suggestions.

Yoti provides a seamless and integrated way to request a watchlist, PEPs and sanctions screening as part of an IDV session providing you results to interpret both in isolation and in context of the other checks carried out as part of that session.  Details of any matches will be accessible to you, and there will be adequate methods of ‘filtering’ results to limit the risk of false positives.

Additionally, Yoti offers ongoing monitoring of a person such that the relying party is notified if a particular person appears on a list over time, after the initial screening.

{% table %}
| AML checks | Description | 
| ---- | ---- | 
| Sanctions and watchlists | 1,000s of global government regulatory and law enforcement watchlists and over 100 International and National Sanctions lists. | 
| PEPs | Consolidated, dynamic global database on politically exposed persons with over 5,000 data sources. | 
| Adverse media | The world’s most accurate database of adverse information and media entities with FATF-aligned categorisation. | 
| Ongoing monitoring | Get alerts to changes in risk status with automated monitoring against real-time databases. | 
{% /table %}

If you would like to tailor your lists or have access to the portal please contact us. 

The below settings need to be stated in a custom API request: 

- Fuzziness
- Source Selection- Listing types or Search Profiles

If they’re not stated, fuzziness will be automatically set at 50% and all available sources will be selected.

Yoti will need to capture the following user attributes:

- Name
- Date of birth
- Country ISO code

To retrieve this please ensure you use the following checks:

{% table widths="169,0" %}
| Name | Resources | Manual check available | 
| ---- | ---- | ---- | 
| Text extraction on a ID document | 1x Document Resource | ✅ | 
{% /table %}

### Enhance your check

Add these features to enhance your check for a stronger verification.

{% table widths="0,0,242" %}
| Name | Description | Resources | Manual check available | 
| ---- | ---- | ---- | ---- | 
| Mobile hand off | Start your session in web and allow the user to smoothly move to mobile. | N/A | N/A | 
{% /table %}

---

## The user flow

The AML check is done in the background when enabling the data extraction check, the user will go through the document upload flow.