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
- The results

---

## AML check

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

If you would like to tailor your lists or have access to the portal please contact us.  Fuzziness is a name matching technique which is used to reduce the impact of misspellings / small variations to reduce false positives. Yoti's default fuzzy logic is set to 50%, this means the minimum word length to allow fuzziness is 5. e.g. Christopher ​matches Christophar but Cris​ w​on’t match​ C​rih.

Differences in punctuation, honorifics, suffixes and case sensitivity do not block matches.

Yoti will need to capture the following user attributes:

- Name
- Date of birth
- Country ISO code

To retrieve this please ensure you use the following checks:

{% table widths="169,0,0" %}
| Name | Resources | Type | Manual check available | 
| ---- | ---- | ---- | ---- | 
| Text extraction on a ID document | 1x Document Resource | Asynchronous | ✅ | 
{% /table %}

## The results

Yoti performs a numerous amount of sub-checks on the document submitted in order to generate this report request:

{% table widths="183" %}
| Recommendation | Explained | 
| ---- | ---- | 
| NOT_AVAILABLE 🟠 | Not enough information to do the requested check. This could be due to text data extraction failing. | 
| CONSIDER 🟠 | If one or more sub check fails. | 
{% /table %}

Each check type will potentially return multiple sub checks in the breakdown reflecting what was requested. In addition each failing sub check will contain additional details on what was flagged:

{% table %}
| Yoti Reason | Description | 
| ---- | ---- | 
| number_of_hits | This is the total number of hits against watchlist types that matches that sub check or any of its subcategories. | 
| closest_match | This is a comma separated list of match_types for the entry that we determined to be the best match for this sub check. | 
{% /table %}

---

### Consider result

In addition to the normal report, watchlist checks will also return a WatchlistSummary object. Please see here for more details:

{% table widths="131,0,0" %}
| Yoti Reason | Description | Automated | Result | 
| ---- | ---- | ---- | ---- | 
| sanction | This sub check will be present if _sanctions_ were chosen as a category  OR an entity was found that is on a _sanction_ watchlist. | ✅ | If this fail's, the check will recommend CONSIDER with reason POTENTIAL_MATCH. | 
| warning | This sub check will be present if _sanctions_ were chosen as a category OR an entity was found that is on a _warning_ watchlist. | ✅ | If this fail's, the check will recommend CONSIDER with reason POTENTIAL_MATCH. | 
| fitness_probity | This sub check will be present if _sanctions_ were chosen as a category OR an entity was found that is on a _fitness_probity_ watchlist. | ✅ | If this fail's, the check will recommend CONSIDER with reason POTENTIAL_MATCH. | 
| pep | This sub check will be present if _sanctions_ were chosen as a category OR an entity was found that is on a _pep_ watchlist. | ✅ | If this fail's, the check will recommend CONSIDER with reason POTENTIAL_MATCH. | 
| adverse media | This sub check will be present if _adverse-media_ were chosen as a category OR an entity was found that is on a _adverse-media_ watchlist. | ✅ | If this fail's, the check will recommend CONSIDER with reason POTENTIAL_MATCH. | 
| custom_search | Only present for advanced checks.\n\nIf a _search_profile_ was used instead of types in the search config. | ✅ | This will fail if any other sub checks fails.\n\n\n\nIf this is pass, no other sub checks will be shown (since we can not tell which ones are requested from the _search_profile_ name. | 
{% /table %}

### Not available result

For the list of not available reasons please see below.

{% table %}
| Yoti Reason | Recovery suggestion | 
| ---- | ---- | 
| NO_VALID_FIELDS\n\n\n\nThe uploaded documents did not contain all fields required to do the check. | Ask the user to try again. | 
{% /table %}

---

## Request AML check

If you would like to request this check you can in two ways:

- Use our [portal](https://developers.yoti.com/identity-verification/portal-guide#request-aml-check).
- Use our [SDK](https://developers.yoti.com/identity-verification/aml-screening-check) or [API](https://yoti.world/yoti-public-api/#/Backend%20Endpoints/post_sessions).