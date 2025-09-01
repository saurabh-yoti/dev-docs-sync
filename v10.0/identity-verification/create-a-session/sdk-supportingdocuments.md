---
type: page
title: Supporting documents
listed: true
slug: sdk-supportingdocuments
description: 
index_title: Supporting documents
hidden: 
keywords: 
tags: 
---

Yoti offers the ability to request additional documents to enhance the verification of the user. You can request this on its own as part of a new session or include in your current session.

Please see our document comparison feature to compliment supporting documents.

{% html %}
<div class="alert-GTK">

    <div class="alert-title" id="GTK">

        Good to know

    </div>

    <div class="alert-text">

Yoti will only compare the NAME of the users between the documents uploaded.
    </div>

    <div class="alert-links"> 

   </div>

</div>
{% /html %}

Currently Yoti supports the ability to upload a:

- Utility bill
- Council tax bill
- Phone bill
- Bank statement

{% code %}
{% tab language="javascript" title="Node.js" %}
const supportingDocumentObjective = new ProofOfAddressObjectiveBuilder().build();

const supportingDocument = new RequiredSupplementaryDocumentBuilder()
    .withObjective(supportingDocumentObjective)
    .build();

const sessionSpec = new SessionSpecificationBuilder()
    // ...  
    .withRequiredDocument(supportingDocument)
    // ...
    .build();
{% /tab %}
{% tab language="java" %}
ProofOfAddressObjective proofOfAddressObjective = ProofOfAddressObjective
        .builder()
        .build();

RequiredSupplementaryDocument supportingDocument = RequiredSupplementaryDocument
        .builder()
        .withObjective(proofOfAddressObjective)
        .build();

SessionSpec sessionSpec = SessionSpec.builder()
        // ...
        .withRequiredDocument(supportingDocument)
        // ...
        .build();
{% /tab %}
{% tab language="php" %}
<?php

$supportingDocumentObjective = (new ProofOfAddressObjectiveBuilder())->build();

$supportingDocument = (new RequiredSupplementaryDocumentBuilder())
		->withObjective($supportingDocumentObjective)
		->build();

$sessionSpec = (new SessionSpecificationBuilder())
		// ...
		->withRequiredDocument($supportingDocument)
		// ...
		->build();
{% /tab %}
{% tab language="csharp" %}
var supportingDocumentObjective = new ProofOfAddressObjectiveBuilder().Build();

var supportingDocument = new RequiredSupplementaryDocumentBuilder()
	.WithObjective(supportingDocumentObjective)
	.Build();

var sessionSpec = new SessionSpecificationBuilder()
	// ...  
	.WithRequiredDocument(supportingDocument)
	// ...
	.Build();
{% /tab %}
{% tab language="go" %}
proofOfAddressObjective, err := objective.NewProofOfAddressObjectiveBuilder().Build()

supplementaryDoc, err := filter.NewRequiredSupplementaryDocumentBuilder().
		WithObjective(proofOfAddressObjective).
		Build()

sessionSpec, err = create.NewSessionSpecificationBuilder().
//..
WithRequiredDocument(supplementaryDoc).
//..
Build()
{% /tab %}
{% tab language="json" %}
{
    "required_documents": [
        {
            "type": "SUPPLEMENTARY_DOCUMENT",
            "objective": {
                "type": "PROOF_OF_ADDRESS"
            }
        }
    ]
}
{% /tab %}
{% /code %}

### Text Extraction

A request to obtain the data printed visually on a document, in structured form. If machine data extraction is not successful, there is an option (selected at session creation) to fall back to manual data extraction. This generates a ‘text data check’ automatically.

{% code %}
{% tab language="javascript" title="Node.js" %}
const supportingDocumentDataExtraction = new RequestedSupplementaryDocTextExtractionTaskBuilder()
    .withManualCheckFallback()
    .build();

const sessionSpec = new SessionSpecificationBuilder()
    // ...
    .withRequestedTask(supportingDocumentDataExtraction)
    // ...
    .build();
{% /tab %}
{% tab language="java" %}
RequestedSupplementaryDocTextExtractionTask supportingDocumentDataExtraction = RequestedSupplementaryDocTextExtractionTask
        .builder()
        .withManualCheckFallback()
        .build();

SessionSpec sessionSpec = SessionSpec.builder()
        // ...
        .withRequestedTask(supportingDocumentDataExtraction)
        // ...
        .build();
{% /tab %}
{% tab language="php" %}
<?php

$supportingDocumentDataExtraction = (new RequestedSupplementaryDocTextExtractionTaskBuilder())
		->withManualCheckFallback()
		->build();

$sessionSpec = (new SessionSpecificationBuilder())
    // ...
    ->withRequestedTask($supportingDocumentDataExtraction)
    // ...
    ->build();
{% /tab %}
{% tab language="csharp" %}
var supportingDocumentDataExtraction = new RequestedSupplementaryDocTextExtractionTaskBuilder()
	.WithManualCheckFallback()
	.Build();

var sessionSpec = new SessionSpecificationBuilder()
	// ...
	.WithRequestedTask(supportingDocumentDataExtraction)
	// ...
	.Build();
{% /tab %}
{% tab language="go" %}
var supplementaryDocTextExtractionTask *task.RequestedSupplementaryDocTextExtractionTask
	supplementaryDocTextExtractionTask, err = task.NewRequestedSupplementaryDocTextExtractionTaskBuilder().
		WithManualCheckFallback().
		Build()

sessionSpec, err = create.NewSessionSpecificationBuilder().
//..
WithRequestedTask(supplementaryDocTextExtractionTask).
//..
Build()
{% /tab %}
{% tab language="json" %}
{
    "requested_tasks": [
        {
            "type": "SUPPLEMENTARY_DOCUMENT_TEXT_DATA_EXTRACTION",
            "config": {
                "manual_check": "FALLBACK"
            }
        }
    ]
}
{% /tab %}
{% /code %}

{% table widths="" %}
| Manual Data extraction | Description | 
| ---- | ---- | 
| withManualCheckFallback | This will initiate manual data extraction only if the automatic extraction fails. We strongly recommend this option. | 
| withManualCheckNever | If the ID fails on automatic extraction, Yoti will not attempt manual extraction and will return a failure in the report. | 
| withManualCheckAlways | The document is always referred for manual review at Yoti's Security Centre, regardless of whether machine data extraction has succeeded or failed. | 
{% /table %}

### Filtering documents

You can filter documents by country or by document type.

{% code %}
{% tab language="javascript" title="Node.js" %}
const supportingDocument = new RequiredSupplementaryDocumentBuilder()
    .withObjective(supportingDocumentObjective)
		.withCountryCodes(["GBR","USA"])
		.withDocumentTypes(["UTILITY_BILL"])
    .build();
{% /tab %}
{% tab language="java" %}
RequiredSupplementaryDocument supportingDocument = RequiredSupplementaryDocument
        .builder()
        .withObjective(proofOfAddressObjective)
  			.withCountryCodes(["GBR","USA"])
				.withDocumentTypes(["UTILITY_BILL"])
        .build();
{% /tab %}
{% tab language="php" %}
$supportingDocument = (new RequiredSupplementaryDocumentBuilder())
		->withObjective($supportingDocumentObjective)
		->withCountryCodes(["GBR","USA"])
		->withDocumentTypes(["UTILITY_BILL"])
		->build();
{% /tab %}
{% tab language="go" %}
supplementaryDoc, err := filter.NewRequiredSupplementaryDocumentBuilder().
		WithObjective(proofOfAddressObjective).
    WithCountryCodes([]string{"GBR"}).
    WithDocumentTypes([]string{"PASSPORT"}).
		Build()
{% /tab %}
{% tab language="json" %}
{
    "required_documents": [
        {
            "type": "SUPPLEMENTARY_DOCUMENT",
            "country_codes": [
                "GBR",
                "USA"
            ],
            "document_types": [
                "UTILITY_BILL"
            ],
            "objective": {
                "type": "PROOF_OF_ADDRESS"
            }
        }
    ]
}
{% /tab %}
{% /code %}

### Document comparison check

For requesting one  ID document and one supporting document from the user please see below for configuration:

{% code %}
{% tab language="javascript" title="Node.js" %}
const documentComparisonCheck = new RequestedIdDocumentComparisonCheckBuilder().build();

const sessionSpec = new SessionSpecificationBuilder()
    // ...
    .withRequestedCheck(documentComparisonCheck)
    // ...
    .build();
{% /tab %}
{% tab language="java" %}
RequestedIdDocumentComparisonCheck requestedIdDocumentComparisonCheck = RequestedIdDocumentComparisonCheck.builder().build();

SessionSpec sessionSpec = SessionSpec.builder()
        // ...
        .withRequestedCheck(requestedIdDocumentComparisonCheck)
        // ...
        .build();
{% /tab %}
{% tab language="php" %}
<?php

$documentComparisonCheck = (new RequestedIdDocumentComparisonCheckBuilder())->build();

$sessionSpec = (new SessionSpecificationBuilder())
    // ...
    ->withRequiredDocument($documentComparisonCheck)
    // ...
    ->build();
{% /tab %}
{% tab language="csharp" %}
var sessionSpec = new SessionSpecificationBuilder()
    // ...
    .WithRequestedCheck(
    	new RequestedThirdPartyIdentityCheckBuilder()
    	.Build())
    // ...
    .Build();
{% /tab %}
{% tab language="go" %}
var idDocsComparisonCheck *check.RequestedIDDocumentComparisonCheck
	idDocsComparisonCheck, err = check.NewRequestedIDDocumentComparisonCheckBuilder().
		Build()

sessionSpec, err = create.NewSessionSpecificationBuilder().
//..
WithRequestedCheckidDocsComparisonCheck).
//..
Build()
{% /tab %}
{% tab language="json" %}
{
    "requested_checks": [
        {
            "type": "ID_DOCUMENT_COMPARISON",
            "config": {}
        }
    ]
}
{% /tab %}
{% /code %}

Yoti will check and compare the following user data and provide you with a sub check result:

- Name
- Date of birth