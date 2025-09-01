---
type: page
title: Report
listed: true
slug: aml-report
description: 
index_title: Report
hidden: 
keywords: 
tags: 
---

Yoti performs a numerous amount of sub-checks on the document submitted in order to generate this report request:

{% table widths="183" %}
| Recommendation | Explained | 
| ---- | ---- | 
| 🟠  NOT_AVAILABLE | Not enough information to do the requested check. This could be due to text data extraction failing. | 
| 🟠  CONSIDER | If one or more sub check fails. | 
{% /table %}

Each check type will potentially return multiple sub checks in the breakdown reflecting what was requested. In addition each failing sub check will contain additional details on what was flagged:

{% table %}
| Yoti Reason | Description | 
| ---- | ---- | 
| number_of_hits | This is the total number of hits against watchlist types that matches that sub check or any of its subcategories. | 
| closest_match | This is a comma separated list of match_types for the entry that we determined to be the best match for this sub check. | 
{% /table %}

---

## Consider report

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

## Not available report

For the list of not available reasons please see below.

{% table %}
| Yoti Reason | Recovery suggestion | 
| ---- | ---- | 
| NO_VALID_FIELDS\n\n\n\nThe uploaded documents did not contain all fields required to do the check. | Ask the user to try again. | 
{% /table %}

---

## Request AML check

If you would like to request this check you can in two ways:

- Use our portal.
- Use our SDK.