---
type: page
title: Expanded Document Fields
listed: true
slug: expanded-document-fields
description: 
index_title: Expanded Document Fields
hidden: 
keywords: 
tags: 
---

When data is extracted from an ID document through OCR, data is returned within a document fields object as detailed [here](https://developers.yoti.com/identity-verification/data-extraction).

In addition to document fields, an expanded set of fields can be returned, providing a full list of each extracted field, the source of the extraction, and any corresponding transliterated values.

The following transliterations are currently supported:

- Cyrillic and Arabic families of languages
- Chinese
- Korean
- Vietnamese
- Turkish languages

## Configure Expanded Document Fields

Expanded fields are not returned by default. This must be added to the ID Document Text Extraction task. 

For non-latin documents you must enable them separately, see [here](https://developers.yoti.com/identity-verification/document-checking#enable-non-latin-documents) for guidance 

{% code %}
{% tab language="javascript" title="Node.js" %}
new RequestedTextExtractionTaskBuilder()
.withCreateExpandedDocumentFields(true) // default is false
.build()
{% /tab %}
{% tab language="java" %}
import com.yoti.api.client.ClassPathKeySource;
import com.yoti.api.client.docs.DocScanClient;
import com.yoti.api.client.docs.DocScanException;
import com.yoti.api.client.docs.session.create.CreateSessionResult;
import com.yoti.api.client.docs.session.create.SessionSpec;
import com.yoti.api.client.docs.session.create.task.RequestedIdDocTextExtractionTask;

...
DocScanClient docScanClient = DocScanClient.builder()
        .withClientSdkId("YOTI_CLIENT_SDK_ID")
        .withKeyPairSource(ClassPathKeySource.fromClasspath("/path/to/pem"))
        .build();

RequestedIdDocTextExtractionTask idDocTextExtractionTask = RequestedIdDocTextExtractionTask.builder()
    .withManualCheckFallback()
  	.withCreateExpandedDocumentFields(true) 
    .build();

SessionSpec sessionSpec = SessionSpec.builder()
        .withRequestedTask(idDocTextExtractionTask)
        .build();

        //Create session
CreateSessionResult sessionResult = docScanClient.createSession(sessionSpec);
{% /tab %}
{% tab language="http" title="JSON" %}
POST /sessions

{
  "client_session_token_ttl": 9000,
  "requested_tasks": [
    {
      "type": "ID_DOCUMENT_TEXT_DATA_EXTRACTION",
      "config": {
        "manual_check": "NEVER",
        "create_expanded_document_fields": true
      }
    }
  ],
  "sdk_config": {
    "allowed_capture_methods": "CAMERA_AND_UPLOAD",
    "success_url": "https://www.yoti.com/",
    "error_url": "https://www.yoti.com/error",
    "allow_handoff": true
  }
}
{% /tab %}
{% /code %}

## Retrieving Expanded Document Fields

The expanded document fields object will not always be present. Expanded fields will only be available within the session when a document has been captured and the OCR (Optical character recognition) has been successful.

Data which is keyed in manually will not be returned in the expanded fields section, this will continue to be returned only within the standard document fields payload.

{% code %}
{% tab language="javascript" title="Node.js" highlightLines="" %}
//Retrieve Expanded Document Fields Media ID, 
idvClient.getSession(sessionId)
  .then((session) => {

    // Returns all resources in the session
    const resources = session.getResources();

    // Returns a collection of ID Documents
    const idDocuments = resources.getIdDocuments();

    idDocuments.map((idDocument) => {
     
		const expandedFields = document.getExpandedDocumentFields()
		const expandedFieldsMediaId = expandedFields.getMedia().getId();
      
		});
});
      
 // Retrieve data      
      
idvClient.getMediaContent(sessionId, expandedFieldsMediaId).then(media => {
  	const buffer = media.getContent();
    const jsonData = JSON.parse(buffer);
    // handle jsonData here
}).catch(error => {
    // handle error
})
{% /tab %}
{% tab language="java" %}
GetSessionResult sessionResult = docScanClient.getSession(sessionId);

// Returns all resources in the session
ResourceContainer resources = sessionResult.getResources();

// Returns a collection of ID Documents
List<? extends IdDocumentResourceResponse> idDocuments = resources.getIdDocuments();

for (IdDocumentResourceResponse idDocument: idDocuments) {

    // Gets the UUID of the document resource
    String id = idDocument.getId();

    // Returns document fields object
    ExpandedDocumentFieldsResponse expandedDocumentFields = idDocument.getExpandedDocumentFields();
    // Get document fields media id
      String expandedDocumentFieldsMediaId = null;
    if (documentFields != null) {
        expandedDocumentFieldsMediaId = expandedDocumentFields.getMedia().getId();
    }
    

  Media media = docScanClient.getMediaContent(sessionId, expandedDocumentFieldsMediaId);
}
{% /tab %}
{% tab language="http" title="JSON" %}
GET /sessions/<session_id>
{% /tab %}
{% /code %}

### Response

A JSON object will be returned when retrieving the expanded document fields media. Some documents will have multiple sources, eg a VIZ and a barcode. Fields that are in both sources will be returned separately with the source available in the response. 

{% code %}
{% tab language="json" %}
{
    "fields": [
        {
            "name": "date_of_birth", //the name of the field
            "value": "1970-01-01", //the contents of the field 
            "locale": "la", //the language/script the field is in on the document
            "source": "VIZ" //where this field has been extracted from // VIZ || BARCODE || MRZ
            "is_non_latin": true // if the field includes non-latin characters
            "is_transliteration": true // if field is transliterated into latin script
        },
        {
            "name": "full_name",
            "value": "MELISSA PETERSON",
            "locale": "la",
            "source": "MRZ"
        },
      ...
    ]
}
{% /tab %}
{% /code %}

#### Values

{% table widths="" %}
| Field | Description | Always present | 
| ---- | ---- | ---- | 
| name | The name of the field. A full list is available [here](https://developers.yoti.com/identity-verification/data-extraction) | ✅ | 
| value | The data from the document field | ✅ | 
| locale | The locale of the field - for any latin script fields this will be "la", for non-latin script this will return the detailed locale eg "ja-JP" for Japan | ✅ | 
| source | Where on the document this field has been returned, this can be VIZ, MRZ or BARCODE | ✅ | 
| is_non_latin | This will be present and true if the field is in a non-latin script | ❌ | 
| is_transliteration | We can transliterate some non-latin fields. This will return the values of the field into latin script | ❌ | 
{% /table %}

### Examples Document Extractions

See the below code blocks for examples of the Expanded Document Fields. The Document Fields JSON is also available at the bottom to compare.

You may use the following keyboard shortcuts to expand or collapse:

Expand: Ctrl + I

Collapse: Ctrl + Y

{% code %}
{% tab language="json" title="UK Passport" %}
expandedDocumentFields
{
    "fields": [
        {
            "name": "date_of_birth",
            "value": "1970-01-01",
            "locale": "la",
            "source": "VIZ"
        },
        {
            "name": "issuing_country",
            "value": "GBR",
            "locale": "la",
            "source": "VIZ"
        },
        {
            "name": "date_of_issue",
            "value": "2025-01-01",
            "locale": "la",
            "source": "VIZ"
        },
        {
            "name": "given_names",
            "value": "MELISSA",
            "locale": "la",
            "source": "VIZ"
        },
        {
            "name": "document_number",
            "value": "533028754",
            "locale": "la",
            "source": "VIZ"
        },
        {
            "name": "family_name",
            "value": "PETERSON",
            "locale": "la",
            "source": "VIZ"
        },
        {
            "name": "gender",
            "value": "FEMALE",
            "locale": "la",
            "source": "VIZ"
        },
        {
            "name": "issuing_authority",
            "value": "HMPO",
            "locale": "la",
            "source": "VIZ"
        },
        {
            "name": "place_of_birth",
            "value": "LONDON",
            "locale": "la",
            "source": "VIZ"
        },
        {
            "name": "expiration_date",
            "value": "2035-01-01",
            "locale": "la",
            "source": "VIZ"
        },
        {
            "name": "full_name",
            "value": "MELISSA PETERSON",
            "locale": "la",
            "source": "VIZ"
        },
        {
            "name": "expiration_date",
            "value": "2025-01-01",
            "locale": "la",
            "source": "MRZ"
        },
        {
            "name": "full_name",
            "value": "MELISSA PETERSON",
            "locale": "la",
            "source": "MRZ"
        },
        {
            "name": "document_number",
            "value": "533028754",
            "locale": "la",
            "source": "MRZ"
        },
        {
            "name": "nationality",
            "value": "GBR",
            "locale": "la",
            "source": "MRZ"
        },
        {
            "name": "given_names",
            "value": "MELISSA",
            "locale": "la",
            "source": "MRZ"
        },
        {
            "name": "issuing_country",
            "value": "GBR",
            "locale": "la",
            "source": "MRZ"
        },
        {
            "name": "date_of_birth",
            "value": "1970-01-01",
            "locale": "la",
            "source": "MRZ"
        },
        {
            "name": "family_name",
            "value": "PETERSON",
            "locale": "la",
            "source": "MRZ"
        },
        {
            "name": "gender",
            "value": "FEMALE",
            "locale": "la",
            "source": "MRZ"
        }
    ]
}


documentFields:
{
    "full_name": "MELISSA PETERSON",
    "date_of_birth": "1970-01-01",
    "nationality": "GBR",
    "given_names": "MELISSA",
    "family_name": "PETERSON",
    "place_of_birth": "LONDON",
    "gender": "FEMALE",
    "document_type": "PASSPORT",
    "issuing_country": "GBR",
    "document_number": "533028754",
    "expiration_date": "2035-01-01",
    "date_of_issue": "2025-01-01",
    "issuing_authority": "HMPO",
    "mrz": {
        "type": 2,
        "line1": "P<GBRPETERSON<<MELISSA<<<<<<<<<<<<<<<<<<<<<<",
        "line2": "5330287549GBR7001014F3501018<<<<<<<<<<<<<<04"
    },
    "document_template": {
        "front_page_name": "United Kingdom - ePassport (2015)"
    }
}
{% /tab %}
{% tab language="json" title="Canada Driving Licence" %}
expandedDocumentFields:
{
    "fields": [
        {
            "name": "height",
            "value": "168 cm",
            "locale": "la",
            "source": "VIZ"
        },
        {
            "name": "given_names",
            "value": "NOEMIE",
            "locale": "la",
            "source": "VIZ"
        },
        {
            "name": "gender",
            "value": "FEMALE",
            "locale": "la",
            "source": "VIZ"
        },
        {
            "name": "family_name",
            "value": "LEGENDRE",
            "locale": "la",
            "source": "VIZ"
        },
        {
            "name": "postal_address",
            "value": "333,BOULEVARD JEAN-LESAGE\nAPP. 432\nQUEBEC (QC) G1K 8J6",
            "locale": "la",
            "source": "VIZ"
        },
        {
            "name": "date_of_birth",
            "value": "1998-12-17",
            "locale": "la",
            "source": "VIZ"
        },
        {
            "name": "driving_licence_class",
            "value": "5",
            "locale": "la",
            "source": "VIZ"
        },
        {
            "name": "issuing_country",
            "value": "CAN",
            "locale": "la",
            "source": "VIZ"
        },
        {
            "name": "driving_licence_restriction_code",
            "value": "A",
            "locale": "la",
            "source": "VIZ"
        },
        {
            "name": "issuing_authority",
            "value": "Quebec",
            "locale": "la",
            "source": "VIZ"
        },
        {
            "name": "document_number",
            "value": "L153117129806",
            "locale": "la",
            "source": "VIZ"
        },
        {
            "name": "full_name",
            "value": "NOEMIE LEGENDRE",
            "locale": "la",
            "source": "VIZ"
        },
        {
            "name": "expiration_date",
            "value": "2017-02-21",
            "locale": "la",
            "source": "VIZ"
        },
        {
            "name": "date_of_issue",
            "value": "2015-08-21",
            "locale": "la",
            "source": "VIZ"
        },
        {
            "name": "issuing_authority",
            "value": "Quebec",
            "locale": "fr-CA",
            "source": "VIZ"
        },
        {
            "name": "eye_color",
            "value": "BLEU",
            "locale": "fr-CA",
            "source": "VIZ"
        },
        {
            "name": "issuing_authority",
            "value": "Quebec",
            "locale": "la",
            "source": "BARCODE"
        },
        {
            "name": "document_number",
            "value": "L153117129806",
            "locale": "la",
            "source": "BARCODE"
        }
    ]
}


documentFields: 
{
    "full_name": "NOEMIE LEGENDRE",
    "date_of_birth": "1998-12-17",
    "given_names": "NOEMIE",
    "family_name": "LEGENDRE",
    "gender": "FEMALE",
    "height": "168 cm",
    "eye_color": "BLEU",
    "structured_postal_address": {
        "address_format": 3,
        "address_line1": "333,BOULEVARD JEAN-LESAGE",
        "address_line2": "APP. 432",
        "town_city": "QUEBEC",
        "state": "QC",
        "postal_code": "G1K 8J6",
        "country_iso": "CAN",
        "country": "Canada",
        "formatted_address": "333,BOULEVARD JEAN-LESAGE\nAPP. 432\nQUEBEC (QC) G1K 8J6"
    },
    "document_type": "DRIVING_LICENCE",
    "issuing_country": "CAN",
    "document_number": "L153117129806",
    "expiration_date": "2017-02-21",
    "date_of_issue": "2015-08-21",
    "issuing_authority": "Quebec",
    "driving_licence_class": "5",
    "driving_licence_restriction_code": "A",
    "document_template": {
        "front_page_name": "Canada - Quebec Learner Driving License (2015)",
        "back_page_name": "Canada - Quebec Driving License (2015) Side B"
    }
}
{% /tab %}
{% tab language="json" title="Japan Driving Licence" %}
expandedDocumentFields:
{
    "fields": [
        {
            "name": "expiration_date",
            "value": "平成25 04 10",
            "locale": "ja-JP",
            "source": "VIZ",
            "is_non_latin": true
        },
        {
            "name": "date_of_issue",
            "value": "平成22 03 10",
            "locale": "ja-JP",
            "source": "VIZ",
            "is_non_latin": true
        },
        {
            "name": "postal_address",
            "value": "東京都千代田区ヶ関2-1-2",
            "locale": "ja-JP",
            "source": "VIZ",
            "is_non_latin": true
        },
        {
            "name": "full_name",
            "value": "日本花子",
            "locale": "ja-JP",
            "source": "VIZ",
            "is_non_latin": true
        },
        {
            "name": "date_of_birth",
            "value": "昭和40 3 10",
            "locale": "ja-JP",
            "source": "VIZ",
            "is_non_latin": true
        },
        {
            "name": "date_of_birth",
            "value": "1965-03-10",
            "locale": "la",
            "source": "VIZ"
        },
        {
            "name": "issuing_country",
            "value": "JPN",
            "locale": "la",
            "source": "VIZ"
        },
        {
            "name": "date_of_issue",
            "value": "2010-03-10",
            "locale": "la",
            "source": "VIZ"
        },
        {
            "name": "document_number",
            "value": "123456789000",
            "locale": "la",
            "source": "VIZ"
        },
        {
            "name": "expiration_date",
            "value": "2013-04-10",
            "locale": "la",
            "source": "VIZ"
        }
    ]
}


documentFields:
{
    "full_name": "日本花子",
    "date_of_birth": "1965-03-10",
    "structured_postal_address": {
        "address_format": 4,
        "address_line1": "東京都千代田区ヶ関2-1-2",
        "country_iso": "JPN",
        "country": "Japan",
        "formatted_address": "東京都千代田区ヶ関2-1-2"
    },
    "document_type": "DRIVING_LICENCE",
    "issuing_country": "JPN",
    "document_number": "123456789000",
    "expiration_date": "2013-04-10",
    "date_of_issue": "2010-03-10"
}
{% /tab %}
{% tab language="json" title="China Driving Licence" %}
expandedDocumentFields
{
    "fields": [
        {
            "name": "document_number",
            "value": "320524197809086414",
            "locale": "la",
            "source": "VIZ"
        },
        {
            "name": "date_of_issue",
            "value": "2004-06-17",
            "locale": "la",
            "source": "VIZ"
        },
        {
            "name": "issuing_country",
            "value": "CHN",
            "locale": "la",
            "source": "VIZ"
        },
        {
            "name": "gender",
            "value": "MALE",
            "locale": "la",
            "source": "VIZ"
        },
        {
            "name": "date_of_birth",
            "value": "1978-09-08",
            "locale": "la",
            "source": "VIZ"
        },
        {
            "name": "driving_licence_class",
            "value": "M",
            "locale": "la",
            "source": "VIZ"
        },
        {
            "name": "gender",
            "value": "男",
            "locale": "zh-CN",
            "source": "VIZ",
            "is_non_latin": true
        },
        {
            "name": "full_name",
            "value": "峰",
            "locale": "zh-CN",
            "source": "VIZ",
            "is_non_latin": true
        },
        {
            "name": "postal_address",
            "value": "江苏省苏州市吳中区镇镇市桥村第七组",
            "locale": "zh-CN",
            "source": "VIZ",
            "is_non_latin": true
        },
        {
            "name": "full_name",
            "value": "FENG",
            "locale": "la",
            "source": "VIZ",
            "is_transliteration": true
        }
    ]
}


documentFields
{
    "full_name": "峰",
    "date_of_birth": "1978-09-08",
    "gender": "MALE",
    "structured_postal_address": {
        "address_format": 4,
        "address_line1": "江苏省苏州市吳中区镇镇市桥村第七组",
        "country_iso": "CHN",
        "country": "China",
        "formatted_address": "江苏省苏州市吳中区镇镇市桥村第七组"
    },
    "document_type": "DRIVING_LICENCE",
    "issuing_country": "CHN",
    "document_number": "320524197809086414",
    "date_of_issue": "2004-06-17",
    "driving_licence_class": "M"
}
{% /tab %}
{% /code %}