---
type: page
title: AML
listed: true
slug: sdk-aml
description: 
index_title: AML
hidden: 
keywords: 
tags: 
---

It is possible to extend the Identity verification integration by requesting an watchlist, PEPs and sanctions check as part of a session.

Additionally, Yoti offers ongoing monitoring of a person such that the relying party is notified if a particular person appears on a list over time, after the initial screening.

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
Please read through our document check section   </div>
   <div class="alert-links"> 
         <a target="_self" href="https://developers.yoti.com/identity-verification/document-checking">Document check</a>
   </div>
</div>
{% /html %}

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

A **successful** text data extraction of the name, address and date of birth. If we are unable to extract the data the check will not be performed. Yoti does not support non-Latin characters currently.

You may want to look at our document settings section in [auto$](/identity-verification/document-checking) to filter out specific documents.

If you decide to ask for two documents, both the primary and secondary ID document will be sourced for attributes required to complete the check. If a supporting document is supplied, the attributes from that will be used, otherwise we’ll use the one from primary or secondary ID document.

Yoti has three types of integrations with our watchlist screening:

{% table widths="149,0,0" %}
|  | Access to the AML portal | Custom search profiles | Ongoing monitoring | 
| ---- | ---- | ---- | ---- | 
| Standard check | ❌ | ❌ | ❌ | 
| Direct check | ✅ | ✅ | ✅ | 
{% /table %}

---

## Standard search check

A simplified generic check designed for quick queries covering:

- sanction
- warning
- fitness-probity
- pep
    - pep-class-1
    - pep-class-2
    - pep-class-3
    - pep-class-4

- adverse-media
    - adverse-media-financial-crime
    - adverse-media-violent-crime
    - adverse-media-sexual-crime
    - adverse-media-terrorism
    - adverse-media-fraud
    - adverse-media-narcotics
    - adverse-media-general

To request this check, a `RequestedWatchlistScreeningCheck` must be specified.

{% code %}
{% tab language="javascript" %}
const watchlistScreeningCheck = new RequestedWatchlistScreeningCheckBuilder()
        .withAdverseMediaCategory()
        .withSanctionsCategory()
        .build()
{% /tab %}
{% tab language="java" %}
RequestedWatchlistScreeningConfig watchlistScreeningConfig = RequestedWatchlistScreeningConfig.builder()
.withSanctionsCategory()
.withAdverseMediaCategory()
.build();

RequestedWatchlistScreeningCheck requestedWatchlistScreeningCheck = RequestedWatchlistScreeningCheck.builder()
.withConfig(watchlistScreeningConfig)
.build();
{% /tab %}
{% tab language="php" %}
<?php
  
$watchScreeningConfig = (new RequestedWatchlistScreeningConfigBuilder())
            ->withSanctionsCategory()
            ->withAdverseMediaCategory()
            ->build();

$watchlistScreeningCheck = (new RequestedWatchlistScreeningCheckBuilder())
                    ->withConfig($watchScreeningConfig)
                    ->build()
{% /tab %}
{% tab language="python" %}
# COMING SOON
{% /tab %}
{% tab language="csharp" %}
var watchlistScreeningCheck = new RequestedWatchlistScreeningCheckBuilder()
                    .ForAdverseMedia()
                    .ForSanctions()
                    .Build()
{% /tab %}
{% tab language="go" %}
var watchlistScreeningCheck *check.RequestedWatchlistScreeningCheck
	watchlistScreeningCheck, err = check.NewRequestedWatchlistScreeningCheckBuilder().
		WithAdverseMediaCategory().
		WithSanctionsCategory().
		Build()
{% /tab %}
{% tab language="json" %}
{
    "type": "WATCHLIST_SCREENING",
    "config": {
        "manual_check": "NEVER",
        "categories": [
            "ADVERSE-MEDIA",
            "SANCTIONS"
        ]
    }
}
{% /tab %}
{% /code %}

{% badge type="custom" text="Note" /%} You will not have access to the portal, or ongoing monitoring.

---

## Direct screening check

If you have further requirements than the above for example:

- Customised search profiles
- Ongoing monitoring. This is a daily process where all searches with monitor enabled will be re-screened withTypes the parameters in place at the time of the search. You will be notified if there any changes.
- Access to the portal 
- Edit our default settings on checks.

To request this check, a `RequestedWatchlistAdvancedCaCheck` must be specified.

{% code %}
{% tab language="javascript" %}
const searchProfileSources = new RequestedSearchProfileSourcesBuilder()
          							 			 .withSearchProfile('searchProfile')
          						       	 .build()

const typeListSources = new RequestedTypeListSourcesBuilder()
          							  .withTypes(['pep', 'fitness-probity', 'warning'])
          								.build()

const exaxtMatchingStrategy = new RequestedExactMatchingStrategyBuilder()
          						          .build()

const fuzzyMatchingStrategy = new RequestedFuzzyMatchingStrategyBuilder()
																.withFuzziness(0.5)
          						          .build()

const customConfig = new RequestedCustomAccountWatchlistAdvancedCaConfigBuilder()
                       .withRemoveDeceased(true)
        							 .withShareUrl(true)
        							 .withSources(searchProfileSources)
        							 .withMatchingStrategy(exaxtMatchingStrategy)
                       .withApiKey('someComplyAdvanceApiKey')
                       .withMonitoring(true)
                       .withTags(SOME_OBJ)
                       .withClientRef("someClientRef")
        							 .build();

const watchlistAdvancedCaCheck = new RequestedWatchlistAdvancedCaCheckBuilder()
                                   .withConfig(customConfig)
                                   .build()
{% /tab %}
{% tab language="java" %}
// Requested Sources
        RequestedCaSources searchProfileSources = RequestedSearchProfileSources.builder()
                .withSearchProfile("SearchProfile")
                .build();
        RequestedCaSources typeListSources = RequestedTypeListSources.builder()
                .withTypes(Arrays.asList("firstType", "secondType"))
                .build();
        // Matching Strategies
        RequestedCaMatchingStrategy fuzzinessMatchingStrategy = RequestedFuzzyMatchingStrategy.builder()
                .withFuzziness("inputfuzzinessnumber")
                .build();

        RequestedWatchlistAdvancedCaConfig customConfig = 	   RequestedCustomAccountWatchlistAdvancedCaConfig.builder()
                .withSources(typeListSources)
                .withMatchingStrategy(fuzzinessMatchingStrategy)
                .withRemoveDeceased(true)
                .withShareUrl(true)
                .withApiKey("someComplyAdvanceApiKey")
                .withClientRef("someClientRef")
                .withMonitoring(true)
                .withTags(SOME_MAP);

        RequestedWatchlistAdvancedCaCheck requestedWatchlistAdvancedCheck = RequestedWatchlistAdvancedCaCheck.builder()
                .withConfig(customConfig)
                .build();
{% /tab %}
{% tab language="php" %}
$searchProfileSources = (new RequestedSearchProfileSourcesBuilder())
		->withSearchProfile("SearchProfile")
		->build();

$typeListSources = (new RequestedTypeListSourcesBuilder())
            ->withTypes(['pep','fitness-probity','warning'])
            ->build();

$exactMatchingStrategy = (new RequestedExactMatchingStrategyBuilder())
		->build();

$fuzzyMatchingStrategy = (new RequestedFuzzyMatchingStrategyBuilder())
            ->withFuzziness(0.5)
            ->build();

$customConfig = (new RequestedCustomAccountWatchlistAdvancedCaConfigBuilder())
    ->withMatchingStrategy($exactMatchingStrategy)
    ->withSources($searchProfileSources)
    ->withShareUrl(true)
    ->withRemoveDeceased(false)
    ->withApiKey("someComplyAdvanceApiKey")
    ->withClientRef("someClientRef")
    ->withMonitoring(true)
    ->withTags(SOME_OBJ)
    ->build();

$watchlistAdvancedCaCheck = (new RequestedWatchlistAdvancedCaCheckBuilder())
            ->withConfig($customConfig)
            ->build()
{% /tab %}
{% tab language="python" %}
# COMING SOON
{% /tab %}
{% tab language="csharp" %}
List<string> sourcesTypesList = new List<string> { "pep", "warning" };

var searchProfileSources = new RequestedSearchProfileSourcesBuilder()
          							 			 .WithSearchProfile('searchProfile')
          						       	 .Build()

var exaxtMatchingStrategy = new RequestedExactMatchingStrategyBuilder()
          						          .Build()

var fuzzyMatchingStrategy = new RequestedFuzzyMatchingStrategyBuilder()
																.WithFuzziness(0.5)
          						          .Build()

string apiKey = "someComplyAdvanceApiKey";
string clientRef = "someClientRef";
bool monitoring = true;
bool removeDeceased = true;
bool shareUrl = false;
  
var customConfig = new RequestedCustomAccountWatchlistAdvancedCaConfigBuilder()
                       .WithRemoveDeceased(removeDeceased)
        							 .WithShareUrl(shareUrl)
        							 .WithSources(sourcesTypesList)
        							 .WithMatchingStrategy(exaxtMatchingStrategy)
                       .WithApiKey(apiKey)
                       .WithMonitoring(monitoring)
                       .WithTags(new Dictionary<string, string> { { "tag1", "value1" }, { "tag2", "value2" } })
                       .WithClientRef(clientRef)
        							 .Build();

var watchlistAdvancedCaCheck = new RequestedWatchlistAdvancedCaCheckBuilder()
                                   .WithConfig(customConfig)
                                   .Build()
{% /tab %}
{% tab language="go" %}
// COMING SOON
{% /tab %}
{% tab language="json" title="JSON 1" %}
{
    "type": "WATCHLIST_ADVANCED_CA",
    "config": {
        "type": "WITH_CUSTOM_ACCOUNT",
        "manual_check": "NEVER",
        "remove_deceased": true,
        "share_url": true,
        "sources": {
            "type": "TYPE_LIST",
            "types": [
                "pep",
                "fitness-probity",
                "warning"
            ]
        },
        "matching_strategy": {
            "type": "EXACT",
            "exact_match": true
        },
        "api_key": "someComplyAdvanceApiKey",
        "monitoring": true,
        "tags": {
            "name": "ADVANCED_check"
        },
        "client_ref": "ww-ref"
    }
}
{% /tab %}
{% tab language="json" title="JSON 2" %}
{
    "type": "WATCHLIST_ADVANCED_CA",
    "config": {
        "type": "WITH_CUSTOM_ACCOUNT",
        "remove_deceased": true,
        "share_url": false,
        "sources": {
            "type": "PROFILE",
            "search_profile": "someStringHere"
        },
        "matching_strategy": {
            "type": "FUZZY",
            "fuzziness": 0.3
        },
        "api_key": "someComplyAdvanceApiKey",
        "monitoring": true,
        "tags": {
            "name": "ADVANCED_check"
        },
        "client_ref": "ww-ref"
    }
}
{% /tab %}
{% /code %}

{% table %}
| Object | Type | Description | 
| ---- | ---- | ---- | 
| SearchProfile | String | The ID of any of your previously created search profiles, which can be found in the main platform UI for search profiles | 
| Types | "sanction", "pep", "warning" | What kind of alert or warning is associated with the entity. | 
| Fuzziness | Float(0.0 to 1.0) | Determines how closely the returned results must match the supplied name. | 
| Remove Deceased | Boolean | A flag which when set, removes deceased people from search results. | 
| ShareUrl | Boolean | Include a shareable URL to access search publicly | 
| APIKey | String | Your API key from ComplyAdvantage | 
| Client Ref | String | Your reference for this person/entity for which you are searching. Used for tracking searches and auto-whitelisting recurring results | 
| Monitoring | Boolean | Enable ongoing monitoring | 
| Tag | Object | Object of name =&gt; value pairs (name must be string), must be existing comply advantage tags | 
{% /table %}

{% badge type="info" text="CONTACT" /%} If you are interested in using this check please contact Yoti. Yoti will enrol you on our platform and you will be able to configure your settings. Yoti aims to get you all set up within 3 days.