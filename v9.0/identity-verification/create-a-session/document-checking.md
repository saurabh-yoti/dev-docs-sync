---
type: page
title: Document
listed: true
slug: document-checking
description: 
index_title: Document
hidden: 
keywords: 
tags: 
---

If you wish to request a document from the user this section will provide you with all the details to complete this. Each check will provide a report of the result from the document check. The user will have the option to upload an image or take a photo, this is configurable in the [auto$](/identity-verification/client-preferences) section. 

Here we describe how to:

- Request a document authenticity check on one or more documents. 
- Request a supporting document - currently we support capturing a council bill, phone bill, utility bill and bank statement.

{% table widths="" %}
| Name | Resources | Type | Manual check available | 
| ---- | ---- | ---- | ---- | 
| Document authenticity | 1x Document Resource | Asynchronous | ✅ | 
| Text extraction | 1x Document Resource | Asynchronous | ✅ | 
| Supporting documents | 1x Document Resource | Asynchronous | ✅ | 
| Document comparison | 2x Document Resource | Asynchronous | ❌ | 
{% /table %}

We provide guidelines in our user view on how to capture the clearest image. The [user view ](https://developers.yoti.com/identity-verification/render-the-user-view)will also handle requesting the number of sides of the document needed for verification.

---

## Document Authenticity

A request to assess the characteristics of a document, to determine the validity of the ID document. Yoti will perform multiple checks on a ID document. 

{% code %}
{% tab language="javascript" title="Node.js" %}
const documentAuthenticityCheck = new RequestedDocumentAuthenticityCheckBuilder()
   .withManualCheckFallback()
   .build();
{% /tab %}
{% tab language="java" %}
RequestedDocumentAuthenticityCheck documentAuthenticityCheck = RequestedDocumentAuthenticityCheck.builder().withManualCheckFallback().build();
{% /tab %}
{% tab language="php" %}
<?php

$documentAuthenticityCheck = (new RequestedDocumentAuthenticityCheckBuilder()->withManualCheckFallback())->build();
{% /tab %}
{% tab language="python" %}
documentAuthenticityCheck = RequestedDocumentAuthenticityCheckBuilder().with_manual_check_fallback().build()
{% /tab %}
{% tab language="csharp" %}
var documentAuthenticityCheck = new RequestedDocumentAuthenticityCheckBuilder().WithManualCheckFallback().Build();
{% /tab %}
{% tab language="go" %}
var documentAuthenticityCheck *check.RequestedDocumentAuthenticityCheck
documentAuthenticityCheck, err = check.NewRequestedDocumentAuthenticityCheckBuilder().
  WithManualCheckFallback().
	Build()
{% /tab %}
{% tab language="json" %}
{
    "requested_checks": [
        {
            "type": "ID_DOCUMENT_AUTHENTICITY",
            "config": {
                "manual_check": "FALLBACK"
            }
        }
    ]
}
{% /tab %}
{% /code %}

{% table widths="201" %}
| Manual Authenticity check | Description | 
| ---- | ---- | 
| withManualCheckFallback | The document inspection falls back to a manual process, if automation does not auto approve or auto reject. | 
| withManualCheckNever | The document inspection never falls back to a manual process. This would be an automated only assessment. | 
| withManualCheckAlways | The document is always referred for manual review in Yoti's Security Centre.\n\n\n\nNote: This config may result in additional charges. | 
{% /table %}

Please see below sections on how to minimise which countries / documents are shown to the user. You can also see our documents coverage using our API.

If the document has a barcode on the document we will attempt to do a barcode comparison check. We will attempt to compare the data and provide you the result. 

### Text Extraction

If you are capturing a users document you may find it usual to capture the data on the document. A request to obtain the data printed visually on a document, in structured form. If machine data extraction is not successful, there is an option (selected at session creation) to fall back to manual data extraction. This generates a ‘text data check’ automatically, and the document is reviewed by one of our document processing experts.

{% code %}
{% tab language="javascript" title="Node.js" %}
const textExtractionTask = new RequestedTextExtractionTaskBuilder()
    .withManualCheckFallback()
    .withCreateExpandedDocumentFields(false)
    .build();
{% /tab %}
{% tab language="java" %}
RequestedIdDocTextExtractionTask idDocTextExtractionTask = RequestedIdDocTextExtractionTask.builder()
    .withManualCheckFallback()
    .build();
{% /tab %}
{% tab language="php" %}
<?php

$textExtractionTask = (new RequestedTextExtractionTaskBuilder())
    ->withManualCheckFallback()
    ->withCreateExpandedDocumentFields(false)
    ->build();
{% /tab %}
{% tab language="python" %}
textExtractionTask = RequestedTextExtractionTaskBuilder()
    .with_manual_check_fallback()
    .build()
{% /tab %}
{% tab language="csharp" %}
var textExtractionTask = new RequestedTextExtractionTaskBuilder()
    .WithManualCheckFallback()
    .WithCreateExpandedDocumentFields()
    .Build();
{% /tab %}
{% tab language="go" %}
var textExtractionTask *task.RequestedTextExtractionTask
textExtractionTask, err = task.NewRequestedTextExtractionTaskBuilder().
    WithManualCheckFallback().
    WithExpandedDocumentFields(false).
    Build()
{% /tab %}
{% tab language="json" %}
{
    "requested_tasks": [
        {
            "type": "ID_DOCUMENT_TEXT_DATA_EXTRACTION",
            "config": {
                "manual_check": "FALLBACK",
                "create_expanded_document_fields": true
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
| withManualCheckAlways | The document is always referred for manual review in Yoti's Security Centre, regardless of whether machine data extraction has succeeded or failed.\n\n\n\nNote: This config may result in additional charges. | 
| withCreateExpandedDocumentFields | If set to true enables the retrieval of expanded document fields including the "source" of each document field. | 
{% /table %}

### NFC (native only)

Near Field Communication (NFC) protocol helps two devices communicate wirelessly when they are placed near each other. NFC hardware is being included in more and more devices, and readers in documents thus we have added the ability to extract data using NFC.

{% code %}
{% tab language="javascript" title="Node.js" %}
const textExtractionTask = new RequestedTextExtractionTaskBuilder()
    .withManualCheckFallback()
    .withChipDataDesired()
    .build();
 
// Ignore NFC chip
const textExtractionTask = new RequestedTextExtractionTaskBuilder()
    .withManualCheckFallback()
    .withChipDataIgnore()
    .build();
{% /tab %}
{% tab language="java" %}
RequestedIdDocTextExtractionTask idDocTextExtractionTask = 
  RequestedIdDocTextExtractionTask.builder()
  	.withManualCheckFallback()
    .withChipDataDesired()
  	.build();

// Ignore NFC chip
RequestedIdDocTextExtractionTask idDocTextExtractionTask = 
  RequestedIdDocTextExtractionTask.builder()
  	.withManualCheckFallback()
    .withChipDataIgnore()
  	.build();
{% /tab %}
{% tab language="php" %}
<?php

$textExtractionTask = (new RequestedTextExtractionTaskBuilder())
		->withManualCheckFallback()
  	->withChipDataDesired()
  	->build();

// Ignore NFC chip
$textExtractionTask = (new RequestedTextExtractionTaskBuilder())
  	->withManualCheckFallback()
  	->withChipDataIgnore()
  	->build();
{% /tab %}
{% tab language="python" %}
textExtractionTask = RequestedTextExtractionTaskBuilder().with_manual_check_fallback().with_chip_data_desired.build()

# Ignore NFC chip
textExtractionTask = RequestedTextExtractionTaskBuilder().with_manual_check_fallback().with_chip_data_ignore.build()
{% /tab %}
{% tab language="csharp" %}
var textExtractionTask = new RequestedTextExtractionTaskBuilder()
    .WithManualCheckFallback()
    .WithChipDataDesired()
    .Build();

// Ignore NFC chip
var textExtractionTask = new RequestedTextExtractionTaskBuilder()
    .WithManualCheckFallback()
    .WithChipDataIgnore()
    .Build();
{% /tab %}
{% tab language="go" %}
var textExtractionTask *task.RequestedTextExtractionTask
textExtractionTask, err = task.NewRequestedTextExtractionTaskBuilder().
    WithManualCheckFallback().
    WithChipDataDesired().
    Build()

// Ignore NFC chip
var textExtractionTask *task.RequestedTextExtractionTask
textExtractionTask, err = task.NewRequestedTextExtractionTaskBuilder().
    WithManualCheckFallback().
    WithChipDataIgnore().
    Build()
{% /tab %}
{% tab language="json" %}
{
    "requested_tasks": [
        {
            "type": "ID_DOCUMENT_TEXT_DATA_EXTRACTION",
            "config": {
                "manual_check": "FALLBACK",
                "chip_data": "DESIRED"
            }
        }
    ]
}

// Ignore NFC chip
{
    "requested_tasks": [
        {
            "type": "ID_DOCUMENT_TEXT_DATA_EXTRACTION",
            "config": {
                "manual_check": "FALLBACK",
                "chip_data": "IGNORE"
            }
        }
    ]
}
{% /tab %}
{% /code %}

{% table widths="" %}
| NFC enablement | Description | 
| ---- | ---- | 
| withChipDataDesired | Enable NFC capabilities | 
| withChipDataIgnore | Disable NFC capabilities | 
{% /table %}

---

## Request multiple documents

It is possible to ask for more than one ID document from the user in the same session using an array.  You will receive two reports and images of all documents submitted. 

{% code %}
{% tab language="javascript" title="Node.js" %}
const {
    SessionSpecificationBuilder,
    DocumentRestrictionsFilterBuilder,
    DocumentRestrictionBuilder,
    RequiredIdDocumentBuilder
} = require('yoti');

const requiredDocument = new RequiredIdDocumentBuilder()
    .build();

const anotherRequiredDocument = new RequiredIdDocumentBuilder()
    .build();

const sessionSpec = new SessionSpecificationBuilder()
    // Additional required document
    .withRequiredDocument(requiredDocument)
    .withRequiredDocument(anotherRequiredDocument)
    .build();
{% /tab %}
{% tab language="java" %}
import com.yoti.api.client.docs.session.create.filters.RequiredIdDocument;
import com.yoti.api.client.docs.session.create.SessionSpec;

RequiredDocument requiredIdDocument = RequiredIdDocument.builder().build();

RequiredDocument anotherRequiredIdDocument = RequiredIdDocument.builder().build();

SessionSpec sessionSpec = SessionSpec.builder()
        // Additional required document
        .withRequiredDocument(requiredIdDocument)
        .withRequiredDocument(anotherRequiredIdDocument)
        .build();
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\DocScan\Session\Create\SessionSpecificationBuilder;
use Yoti\DocScan\Session\Create\Filters\Document\DocumentRestrictionBuilder;
use Yoti\DocScan\Session\Create\Filters\Document\DocumentRestrictionsFilterBuilder;
use Yoti\DocScan\Session\Create\Filters\RequiredIdDocumentBuilder;

$requiredDocument = (new RequiredIdDocumentBuilder())
    ->build();

$anotherRequiredDocument = (new RequiredIdDocumentBuilder())
    ->build();

$sessionSpec = (new SessionSpecificationBuilder())
    // Additional required document
    ->withRequiredDocument($requiredDocument)
    ->withRequiredDocument($anotherRequiredDocument)
    ->build();
{% /tab %}
{% tab language="python" %}
from yoti_python_sdk.doc_scan import (
    SessionSpecBuilder
)

from yoti_python_sdk.doc_scan.session.create.filter import (
    DocumentRestrictionBuilder,
    DocumentRestrictionsFilterBuilder,
    RequiredIdDocumentBuilder
)

required_document = RequiredIdDocumentBuilder().build()

another_required_document = RequiredIdDocumentBuilder().build()

session_spec = (
    SessionSpecBuilder()
    # Additional required document
    .with_required_document(required_document)
    .with_required_document(another_required_document)
    .build()
)
{% /tab %}
{% tab language="csharp" %}
using Yoti.Auth.DocScan.Session.Create;

var requiredDocument = new RequiredIdDocumentBuilder().Build();
  
var anotherRequiredDocument = new RequiredIdDocumentBuilder().Build();

var sessionSpec = new SessionSpecificationBuilder()
    // Additional required document
    .WithRequiredDocument(requiredDocument)
    .WithRequiredDocument(anotherRequiredDocument)
    .Build();
{% /tab %}
{% tab language="go" %}
idDoc, err := filter.NewRequiredIDDocumentBuilder().Build()

anotherIdDoc, err := filter.NewRequiredIDDocumentBuilder().Build()

sessionSpec, err = create.NewSessionSpecificationBuilder().
		// Additional required document
		WithRequiredDocument(idDoc).
		WithRequiredDocument(anotherIdDoc).
		Build()
{% /tab %}
{% tab language="json" %}
{
    "required_documents": [
        {
            "type": "ID_DOCUMENT"
        },
        {
            "type": "ID_DOCUMENT"
        }
    ]
}
{% /tab %}
{% /code %}

If you wish to add filters on which documents you want to show please see section below.

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
If you are requesting multiple documents from your users you must make sure that you avoid creating sessions where the same document would be used to satisfy multiple selections.    </div>
    <div class="alert-links"> 

   </div>
</div>
{% /html %}

### Document comparison check

If you request your users to upload more than one document we offer the ability to cross check the data, please see below for configuration:

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
    ->withRequestedCheck($documentComparisonCheck)
    // ...
    ->build();
{% /tab %}
{% tab language="csharp" %}
var documentComparisonCheck = new RequestedIdDocumentComparisonCheckBuilder().Build();

var sessionSpec = new SessionSpecificationBuilder()
	// ...
	.WithRequestedCheck(documentComparisonCheck)
	// ...
	.Build();
{% /tab %}
{% tab language="python" %}
documentComparisonCheck = RequestedIDDocumentComparisonCheckBuilder().build()
    
session_spec = (
    SessionSpecBuilder()
     // ...
    .with_requested_check(documentComparisonCheck)
    .build()
)
{% /tab %}
{% tab language="go" %}
var idDocsComparisonCheck *check.RequestedIDDocumentComparisonCheck
		idDocsComparisonCheck, err = check.NewRequestedIDDocumentComparisonCheckBuilder().
		Build()

sessionSpec, err = create.NewSessionSpecificationBuilder().
		// ...
		WithRequestedCheck(idDocsComparisonCheck).
    // ...
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

---

## Document settings

This section will outline helpful api features we have.

1. List of documents supported
2. Restriction of documents / countries. If you do not wish to accept all documents or countries you can configure your session to add / remove which countries and document types are displayed to the user on the user view.

### Supported Documents

To see all documents that are supported please see the code snippet below.

{% code %}
{% tab language="javascript" title="Node.js" %}
const path = require('path');
const fs = require('fs');

const { IDVClient } = require('yoti');

const YOTI_CLIENT_SDK_ID = 'YOUR_SDK_ID';
const YOTI_PEM = fs.readFileSync(path.join(__dirname, '/path/to/pem'));
const idvClient = new IDVClient(YOTI_CLIENT_SDK_ID, YOTI_PEM);

idvClient.getSupportedDocuments().then((supportedDocuments) => {
    supportedCountries = supportedDocuments.getSupportedCountries();
    supportedCountries.map((country) => {
        countryCode = country.getCode();
        documents = country.getSupportedDocuments();
    });
});
{% /tab %}
{% tab language="java" %}
import com.yoti.api.client.docs.DocScanClient;
import com.yoti.api.client.docs.DocScanClientBuilder;
import com.yoti.api.client.docs.support.SupportedCountry;
import com.yoti.api.client.docs.support.SupportedDocument;
import com.yoti.api.client.docs.support.SupportedDocumentsResponse;

DocScanClient docScanClient = DocScanClient.builder()
        .withClientSdkId("YOUR_CLIENT_SDK_ID")
        .withKeyPairSource(ClassPathKeySource.fromClasspath("/path/to/pem"))
        .build();

SupportedDocumentsResponse supportedDocuments = docScanClient.getSupportedDocuments();
List<? extends SupportedCountry> supportedCountries = supportedDocuments.getSupportedCountries();

for (SupportedCountry country : supportedCountries) {

   String countryCode = country.getCode();
   List<? extends SupportedDocument> documents = country.getSupportedDocuments();

}
{% /tab %}
{% tab language="php" %}
<?php

require_once './vendor/autoload.php';

use Yoti\DocScan\DocScanClient;

$YOTI_CLIENT_SDK_ID = 'YOUR_SDK_ID';
$YOTI_PEM = '/path/to/pem';

$client = new DocScanClient($YOTI_CLIENT_SDK_ID, $YOTI_PEM);

$supportedDocuments = $client->getSupportedDocuments();
$supportedCountries = $supportedDocuments->getSupportedCountries();

foreach($supportedCountries as $country) {
  
    $countryCode = $country->getCode();
    $documents = $country->getSupportedDocuments();
  
}
{% /tab %}
{% tab language="python" %}
from yoti_python_sdk.doc_scan import (
    DocScanClient
)

YOTI_CLIENT_SDK_ID = 'YOUR_SDK_ID'
YOTI_PEM = '/path/to/pem'

doc_scan_client = DocScanClient(YOTI_CLIENT_SDK_ID, YOTI_PEM)

supported_documents = doc_scan_client.get_supported_documents()
supported_countries = supported_documents.supported_countries

for country in supported_countries:
    country_code = country.code
    documents = country.supported_documents
{% /tab %}
{% tab language="csharp" %}
using System.IO;
using System.Net.Http;
using Yoti.Auth;
using Yoti.Auth.DocScan;
using Yoti.Auth.DocScan.Session.Create;
using Yoti.Auth.DocScan.Session.Create.Check;
using Yoti.Auth.DocScan.Session.Create.Task;

...
const string YOTI_CLIENT_SDK_ID = "YOTI_CLIENT_SDK_ID";
const string PEM_PATH = "/path/to/pem";

StreamReader privateKeyStream = System.IO.File.OpenText(PEM_PATH);
var key = CryptoEngine.LoadRsaKey(privateKeyStream);

var docScanClient = new DocScanClient(YOTI_CLIENT_SDK_ID, key, new HttpClient());
GetSupportedDocuments getSupportedDocuments = docScanClient.GetSupportedDocuments();

// get methods
{% /tab %}
{% tab language="java" title="Java v2" %}
import com.yoti.api.client.docs.DocScanClient;
import com.yoti.api.client.docs.DocScanClientBuilder;
import com.yoti.api.client.docs.support.SupportedCountry;
import com.yoti.api.client.docs.support.SupportedDocument;
import com.yoti.api.client.docs.support.SupportedDocumentsResponse;

DocScanClient docScanClient = DocScanClientBuilder.newInstance()
        .withClientSdkId("YOUR_CLIENT_SDK_ID")
        .withKeyPairSource(ClassPathKeySource.fromClasspath("/path/to/pem"))
        .build();

SupportedDocumentsResponse supportedDocuments = docScanClient.getSupportedDocuments();
List<? extends SupportedCountry> supportedCountries = supportedDocuments.getSupportedCountries();

for (SupportedCountry country : supportedCountries) {

   String countryCode = country.getCode();
   List<? extends SupportedDocument> documents = country.getSupportedDocuments();

}
{% /tab %}
{% /code %}

Yoti will return a list of countries listed by ISO 3166 country code. Each country will list an array of supported documents from that country.

### Filtering Settings

{% table widths="" %}
| Settings | Description | 
| ---- | ---- | 
| Orthogonal restrictions | Allow (whitelist) or remove (blacklist) by country and document type independently. | 
| Document restrictions | This filter allows greater precision but is more verbose to use. It provides multiple restrictions that filter by _country_ and _document type_ together. | 
| Non latin documents | Yoti can support an array of non latin documents from multiple countries. | 
| Expired documents | By default expired documents will not be accepted, but you are able to enable the use of expired documents. | 
{% /table %}

### Enable non-latin documents

Yoti can support a number of non latin documents from multiple countries. A list can be found below:

{% synced id="non-latin-documents-table" %}
{% /synced %}

Please be aware that these documents do not support manual text extraction. Data can only be obtained using Optical Character Recognition (OCR) only. The API allows you to enable support for all non-latin documents, or selectively choose which ones to process using the filters provided below.

### Enable expired documents

Yoti can support expired documents, the feature simply needs to be enabled.

### Orthogonal restriction

Allow (whitelist) or remove (blacklist) by _country_ and _document type_ independently.

If you create a WHITELIST for one country / document and also a BLACKLIST for the other, then the BLACKLIST will overrule the WHITELIST.

{% code %}
{% tab language="javascript" title="Node.js" %}
const {
    SessionSpecificationBuilder,
    RequiredIdDocumentBuilder,
    OrthogonalRestrictionsFilterBuilder
} = require('yoti');

const filter = new OrthogonalRestrictionsFilterBuilder()
    // Allow from specific countries
    .withWhitelistedCountries(['GBR', 'JPN'])

    // Deny from specific countries
    .withBlacklistedCountries(['FRA'])

    // Allow specific documents
    .withWhitelistedDocumentTypes(['PASSPORT'])

    // Deny certain documents
    .withBlacklistedDocumentTypes(['DRIVING_LICENCE'])

		// Allow non latin documents
		.withAllowNonLatinDocuments(true)
  
    // Allow expired documents
    .withAllowExpiredDocuments(true)
    .build();

const requiredDocument = new RequiredIdDocumentBuilder()
    .withFilter(filter)
    .build();

const sessionSpec = new SessionSpecificationBuilder()
    // New method in addition to existing create session methods
    .withRequiredDocument(requiredDocument)
    .build();
{% /tab %}
{% tab language="java" %}
import com.yoti.api.client.docs.session.create.*;
import com.yoti.api.client.docs.session.create.filters.*;

import java.util.Arrays;
import java.util.Collections;

OrthogonalRestrictionsFilter filter = OrthogonalRestrictionsFilter.builder()
        // Allow from specific countries
        .withWhitelistedCountries(Arrays.asList("GBR", "JPN"))

        // Deny from specific countries
        .withBlacklistedCountries(Collections.singletonList("FRA"))

        // Allow specific documents
        .withWhitelistedDocumentTypes(Collections.singletonList("PASSPORT"))

        // Deny certain documents
        .withBlacklistedDocumentTypes(Collections.singletonList("DRIVING_LICENCE"))
  
        // Allow non latin documents
        .withAllowNonLatinDocuments()
  
        // Allow expired documents
        .withAllowExpiredDocuments()
        .build();

RequiredIdDocument requiredDocument = RequiredIdDocument.builder()
        .withFilter(filter)
        .build();

SessionSpec sessionSpec = SessionSpec.builder()
        // New method in addition to existing create session methods
        .withRequiredDocument(requiredDocument)
        .build();
{% /tab %}
{% tab language="php" %}
<? php
  
use Yoti\DocScan\Session\Create\SessionSpecificationBuilder;
use Yoti\DocScan\Session\Create\Filters\Orthogonal\OrthogonalRestrictionsFilterBuilder;
use Yoti\DocScan\Session\Create\Filters\RequiredIdDocumentBuilder;

$filter = (new OrthogonalRestrictionsFilterBuilder())
    // Allow from specific countries
    ->withWhitelistedCountries(['GBR', 'JPN'])

    // Deny from specific countries
    ->withBlacklistedCountries(['FRA'])

    // Allow specific documents
    ->withWhitelistedDocumentTypes(['PASSPORT'])

    // Deny certain documents
    ->withBlacklistedDocumentTypes(['DRIVING_LICENCE'])
  
    // enable non latin documents
    ->withAllowNonLatinDocuments()
  
    // enable expired documents
    ->withAllowExpiredDocuments()
    ->build();

$requiredDocument = (new RequiredIdDocumentBuilder())
    ->withFilter($filter)
    ->build();

$sessionSpec = (new SessionSpecificationBuilder())
    // New method in addition to existing create session methods
    ->withRequiredDocument($requiredDocument)
    ->build();
{% /tab %}
{% tab language="python" %}
from yoti_python_sdk.doc_scan import (
    SessionSpecBuilder
)

from yoti_python_sdk.doc_scan.session.create.filter import (
    OrthogonalRestrictionsFilterBuilder,
    RequiredIdDocumentBuilder
)

filter = (
    OrthogonalRestrictionsFilterBuilder()
    # Allow from specific countries
    .with_whitelisted_country_codes(['GBR', 'JPN'])

    # Deny from specific countries
    .with_blacklisted_country_codes(['FRA'])

    # Allow specific documents
    .with_whitelisted_document_types(['PASSPORT'])

    # Deny certain documents
    .with_blacklisted_document_types(['DRIVING_LICENCE'])
    .build()
)

required_document = RequiredIdDocumentBuilder().with_filter(filter).build()

session_spec = (
    SessionSpecBuilder()
    # New method in addition to existing create session methods
    .with_required_document(required_document)
    .build()
)
{% /tab %}
{% tab language="csharp" %}
//Coming soon
{% /tab %}
{% tab language="json" %}
{
    "required_documents": [
        {
            "type": "ID_DOCUMENT",
            "filter": {
                "allow_non_latin_documents" true,
                "type": "ORTHOGONAL_RESTRICTIONS",
                "allow_expired_documents": true,
                "country_restriction": {
                    "inclusion": "WHITELIST", // OR BLACKLIST
                    "country_codes": [
                        "GBR",
                        "JPN" // FRA
                    ]
                },
                "type_restriction": {
                    "inclusion": "WHITELIST", // OR BLACKLIST
                    "document_types": [
                        "PASSPORT" // DRIVING_LICENCE
                    ]
                }
            }
        }
    ]
}
{% /tab %}
{% /code %}

### Document restriction

This filter allows greater precision but is more verbose to use. It provides multiple restrictions that filter by _country_ and _document type_ together.

{% code %}
{% tab language="javascript" title="Node.js" %}
const {
    SessionSpecificationBuilder,
    DocumentRestrictionsFilterBuilder,
    DocumentRestrictionBuilder,
    RequiredIdDocumentBuilder
} = require('yoti');

const documentRestriction = new DocumentRestrictionBuilder()
    // Set countries
    .withCountries(['GBR'])

    // Set document types
    .withDocumentTypes(['PASSPORT'])
    .build();

const filter = new DocumentRestrictionsFilterBuilder()
    // Set document restriction
    .withDocumentRestriction(documentRestriction)

    // Specify if this filter is an allowed list, or denied list
    .forWhitelist() // or forBlacklist() if disallowing this filter

    // Allow non latin documents
    .withAllowNonLatinDocuments(true)

    // Allow expired documents
    .withAllowExpiredDocuments(true)
    .build();

const requiredDocument = new RequiredIdDocumentBuilder()
    .withFilter(filter)
    .build();

const sessionSpec = new SessionSpecificationBuilder()
    // New method in addition to existing create session methods
    .withRequiredDocument(requiredDocument)
    .build();
{% /tab %}
{% tab language="java" %}
import com.yoti.api.client.docs.session.create.*;
import com.yoti.api.client.docs.session.create.filters.*;

import java.util.Collections;

DocumentRestriction documentRestriction = DocumentRestriction.builder()
        // Set countries
        .withCountries(Collections.singletonList("GBR"))

        // Set document types
        .withDocumentTypes(Collections.singletonList("PASSPORT"))
        .build();

DocumentRestrictionsFilter filter = DocumentRestrictionsFilter.builder()
        // Set document restriction
        .withDocumentRestriction(documentRestriction)

        // Specify if this filter is an allowed list, or denied list
        .forWhitelist() // or forBlacklist() if disallowing this filter
  
         // Allow non latin documents
        .withAllowNonLatinDocuments()
  
        // Allow expired documents
        .withAllowExpiredDocuments()
        .build();

RequiredIdDocument requiredDocument = RequiredIdDocument.builder()
        .withFilter(filter)
        .build();

SessionSpec sessionSpec = SessionSpec.builder()
        // New method in addition to existing create session methods
        .withRequiredDocument(requiredDocument)
        .build();
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\DocScan\Session\Create\SessionSpecificationBuilder;
use Yoti\DocScan\Session\Create\Filters\Document\DocumentRestrictionBuilder;
use Yoti\DocScan\Session\Create\Filters\Document\DocumentRestrictionsFilterBuilder;
use Yoti\DocScan\Session\Create\Filters\RequiredIdDocumentBuilder;

$documentRestriction = (new DocumentRestrictionBuilder())
    // Set countries
    ->withCountries(['GBR'])

    // Set document types
    ->withDocumentTypes(['PASSPORT'])
    ->build();

$filter = (new DocumentRestrictionsFilterBuilder())
    // Set document restriction
    ->withDocumentRestriction($documentRestriction)
  
    // enable non latin documents
    ->withAllowNonLatinDocuments()
  
    // enable expired documents
    ->withAllowExpiredDocuments()

    // Specify if this filter is an allowed list, or denied list
    ->forWhitelist() // or forBlacklist() if disallowing this filter
    ->build();

$requiredDocument = (new RequiredIdDocumentBuilder())
    ->withFilter($filter)
    ->build();

$sessionSpec = (new SessionSpecificationBuilder())
    // New method in addition to existing create session methods
    ->withRequiredDocument($requiredDocument)
    ->build();
{% /tab %}
{% tab language="python" %}
from yoti_python_sdk.doc_scan import (
    SessionSpecBuilder
)

from yoti_python_sdk.doc_scan.session.create.filter import (
    DocumentRestrictionBuilder,
    DocumentRestrictionsFilterBuilder,
    RequiredIdDocumentBuilder
)

document_restriction = (
    DocumentRestrictionBuilder()
    # Set countries
    .with_country_codes(['GBR'])

    # Set document types
    .with_document_types(['PASSPORT'])
    .build()
)

filter = (
    DocumentRestrictionsFilterBuilder()
    # Set document restriction
    .with_document_restriction(document_restriction)

    # Specify if this filter is an allowed list, or denied list
    .for_whitelist() # or for_blacklist() if disallowing this filter
    .build()
)

required_document = RequiredIdDocumentBuilder().with_filter(filter).build()

session_spec = (
    SessionSpecBuilder()
    # New method in additional to existing create session methods
    .with_required_document(required_document)
    .build()
)
{% /tab %}
{% tab language="csharp" %}
//COMING SOON
{% /tab %}
{% tab language="json" %}
{
    "required_documents": [
        {
            "type": "ID_DOCUMENT",
            "filter": {
                "type": "DOCUMENT_RESTRICTIONS",
                "inclusion": "WHITELIST",
                "documents": [
                    {
                        "country_codes": [
                            "GBR"
                        ],
                        "document_types": [
                            "PASSPORT"
                        ]
                    }
                ]
            }
        }
    ]
}
{% /tab %}
{% /code %}

### Multiple documents and filter

Please see example code for requesting multiple documents with filtering.

{% code %}
{% tab language="javascript" title="Node.js" %}
const {
    SessionSpecificationBuilder,
    DocumentRestrictionsFilterBuilder,
    DocumentRestrictionBuilder,
    RequiredIdDocumentBuilder
} = require('yoti');

const documentRestriction = new DocumentRestrictionBuilder()
    .withCountries(['GBR'])
    .withDocumentTypes(['PASSPORT'])
    .build();

const filter = new DocumentRestrictionsFilterBuilder()
    .withDocumentRestriction(documentRestriction)
    .forWhitelist()
    .build();

const requiredDocument = new RequiredIdDocumentBuilder()
    .withFilter(filter)
    .build();

const anotherDocumentRestriction = new DocumentRestrictionBuilder()
    .withCountries(['GBR'])
    .withDocumentTypes(['DRIVING_LICENCE'])
    .build();

const anotherFilter = new DocumentRestrictionsFilterBuilder()
    .withDocumentRestriction(anotherDocumentRestriction)
    .forWhitelist()
    .build();

const anotherRequiredDocument = new RequiredIdDocumentBuilder()
    .withFilter(anotherFilter)
    .build();

const sessionSpec = new SessionSpecificationBuilder()
    // Additional required document
    .withRequiredDocument(requiredDocument)
    .withRequiredDocument(anotherRequiredDocument)
    .build();
{% /tab %}
{% tab language="java" %}
import com.yoti.api.client.docs.session.create.*;
import com.yoti.api.client.docs.session.create.filters.*;

import java.util.Collections;

DocumentRestriction documentRestriction = DocumentRestriction.builder()
        // Set countries
        .withCountries(Collections.singletonList("GBR"))

        // Set document types
        .withDocumentTypes(Collections.singletonList("PASSPORT"))
        .build();

DocumentRestrictionsFilter filter = DocumentRestrictionsFilter.builder()
        // Set document restriction
        .withDocumentRestriction(documentRestriction)

        // Specify if this filter is an allowed list, or denied list
        .forWhitelist() // or forBlacklist() if disallowing this filter
        .build();

RequiredIdDocument requiredDocument = RequiredIdDocument.builder()
        .withFilter(filter)
        .build();

DocumentRestriction anotherDocumentRestriction = DocumentRestriction.builder()
        // Set countries
        .withCountries(Collections.singletonList("GBR"))

        // Set document types
        .withDocumentTypes(Collections.singletonList("DRIVING_LICENCE"))
        .build();

DocumentRestrictionsFilter anotherFilter = DocumentRestrictionsFilter.builder()
        // Set document restriction
        .withDocumentRestriction(anotherDocumentRestriction)

        // Specify if this filter is an allowed list, or denied list
        .forWhitelist() // or forBlacklist() if disallowing this filter
        .build();

RequiredIdDocument anotherRequiredDocument = RequiredIdDocument.builder()
        .withFilter(anotherFilter)
        .build();

SessionSpec sessionSpec = SessionSpec.builder()
        // Additional required document
        .withRequiredDocument(requiredDocument)
        .withRequiredDocument(anotherRequiredDocument)
        .build();
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\DocScan\Session\Create\SessionSpecificationBuilder;
use Yoti\DocScan\Session\Create\Filters\Document\DocumentRestrictionBuilder;
use Yoti\DocScan\Session\Create\Filters\Document\DocumentRestrictionsFilterBuilder;
use Yoti\DocScan\Session\Create\Filters\RequiredIdDocumentBuilder;

$documentRestriction = (new DocumentRestrictionBuilder())
    ->withCountries(['GBR'])
    ->withDocumentTypes(['PASSPORT'])
    ->build();

$filter = (new DocumentRestrictionsFilterBuilder())
    ->withDocumentRestriction($documentRestriction)
    ->forWhitelist()
    ->build();

$requiredDocument = (new RequiredIdDocumentBuilder())
    ->withFilter($filter)
    ->build();

$anotherDocumentRestriction = (new DocumentRestrictionBuilder())
    ->withCountries(['GBR'])
    ->withDocumentTypes(['DRIVING_LICENCE'])
    ->build();

$anotherFilter = (new DocumentRestrictionsFilterBuilder())
    ->withDocumentRestriction($anotherDocumentRestriction)
    ->forWhitelist()
    ->build();

$anotherRequiredDocument = (new RequiredIdDocumentBuilder())
    ->withFilter($anotherFilter)
    ->build();

$sessionSpec = (new SessionSpecificationBuilder())
    // Additional required document
    ->withRequiredDocument($requiredDocument)
    ->withRequiredDocument($anotherRequiredDocument)
    ->build();
{% /tab %}
{% tab language="python" %}
from yoti_python_sdk.doc_scan import (
    SessionSpecBuilder
)

from yoti_python_sdk.doc_scan.session.create.filter import (
    DocumentRestrictionBuilder,
    DocumentRestrictionsFilterBuilder,
    RequiredIdDocumentBuilder
)

document_restriction = (
    DocumentRestrictionBuilder()
    .with_country_codes(['GBR'])
    .with_document_types(['PASSPORT'])
    .build()
)

filter = (
    DocumentRestrictionsFilterBuilder()
    .with_document_restriction(document_restriction)
    .for_whitelist()
    .build()
)

required_document = RequiredIdDocumentBuilder().with_filter(filter).build()

another_document_restriction = (
    DocumentRestrictionBuilder()
    .with_country_codes(['GBR'])
    .with_document_types(['DRIVING_LICENCE'])
    .build()
)

another_filter = (
    DocumentRestrictionsFilterBuilder()
    .with_document_restriction(another_document_restriction)
    .for_whitelist()
    .build()
)

another_required_document = RequiredIdDocumentBuilder().with_filter(another_filter).build()

session_spec = (
    SessionSpecBuilder()
    # Additional required document
    .with_required_document(required_document)
    .with_required_document(another_required_document)
    .build()
)
{% /tab %}
{% tab language="csharp" %}
// Click to edit code
{% /tab %}
{% tab language="json" %}
{
    "required_documents": [
        {
            "type": "ID_DOCUMENT",
            "filter": {
                "type": "DOCUMENT_RESTRICTIONS",
                "inclusion": "WHITELIST",
                "documents": [
                    {
                        "country_codes": [
                            "GBR"
                        ],
                        "document_types": [
                            "PASSPORT"
                        ]
                    }
                ]
            }
        },
        {
            "type": "ID_DOCUMENT",
            "filter": {
                "type": "DOCUMENT_RESTRICTIONS",
                "inclusion": "WHITELIST",
                "documents": [
                    {
                        "country_codes": [
                            "GBR"
                        ],
                        "document_types": [
                            "DRIVING_LICENCE"
                        ]
                    }
                ]
            }
        }
    ]
}
{% /tab %}
{% /code %}