---
type: page
title: Data extraction
listed: true
slug: data-extraction
description: 
index_title: Data extraction
hidden: 
keywords: 
tags: 
---

If you wish to request the document details from the user this section will provide you context on what this check entails. Yoti will extract data from thousands of ID documents from 200+ countries using Optical Character Recognition (OCR), with the option of a fallback to a manual data entry process in the event OCR is not successful.

This section will describe:

- What a data extraction check is.
- Outcome report with recovery suggestions.

The below checks are related to data extraction checks available at Yoti:

{% table widths="0,0,242" %}
| Name | Description | Resources | Manual check available | 
| ---- | ---- | ---- | ---- | 
| Text extraction | A request to obtain the data printed visually on a document, in structured form. | 1x Document Resource | ✅ | 
{% /table %}

If machine data extraction is not successful, at session creation there is an option to fallback to manual data extraction. This generates a ‘text data check’ automatically, and the document is reviewed by one of our document processing experts. The automated check is instantaneous. 

Yoti will attempt to extract as much as data as possible depending on the document type.

## Enhance your check

Add these features to enhance your check for a stronger verification.

{% table widths="0,0,242" %}
| Name | Description | Resources | Manual check available | 
| ---- | ---- | ---- | ---- | 
| Mobile hand off | Start your session in web and allow the user to smoothly move to mobile. | N/A | N/A | 
| NFC | Enable Near Field Communication (NFC) for native integrations. | 1x Document Resource | ❌ | 
{% /table %}

---

## Data extracted

See below for data that Yoti will attempt to extract. Please note every document has different fields, Yoti will extract what we can. 

{% table %}
| Field name | Type | Description | Example | 
| ---- | ---- | ---- | ---- | 
| full_name | string | FullName contains given names and family name. | “Jon Jim Fred Foo” | 
| date_of_birth | string | DateOfBirth is the date of birth in the form yyyy-mm-dd, or yyyy-mm or yyyy. \n\n\nA small percentage of documents do not provide the full DoB, if available in the visual zone or barcode data Yoti will always return the full DoB. | "2000-12-01" | 
| nationality | string | Nationality is the nationality expressed as an ISO/ICAO alpha-3 country code. \n\n\nNot all documents provide this. | "GBR" | 
| given_names | string | GivenNames contains first and middle names.\n\n\n\nNot all documents provide split given names and family name, in those cases only the full name field will be returned. | "Jon Jim Fred" | 
| first_name | string | FirstName is the first name only.\n\n\n\nOnly for those documents that provide first name and middle name split | “Jon” | 
| middle_name | string | MiddleName contains the middle names only.\n\n\n\nOnly for those documents that provide first name and middle names split. | “Jim Fred” | 
| family_name | string | FamilyName is the family name.\n\n\n\nNot all documents provide split given names and family name, in those cases only the full name field will be returned. | “Foo” | 
| place_of_birth | string | PlaceOfBirth is the place of birth, it may contain a country name or a city name or both.\n\n\n\nNot all documents provide this. | "London" | 
| country_of_birth | string | CountryOfBirth is the country of birth, as an ISO/ICAO alpha-3 country code.\n\n\nNot all documents provide this. | "GBR" | 
| gender | string | Gender is the gender and can be any of the following values: "MALE", "FEMALE", "TRANSGENDER" or "OTHER". | "MALE" | 
| name_prefix | string | NamePrefix is the name prefix, for example a title.\n\n\n\nOnly certain documents provide this. | “Dr” | 
| name_suffix | string | NameSuffix is the name suffix.\n\n\n\nOnly certain documents provide this. | “Jr” | 
| first_name_alias | string | FirstNameAlias is the alias for the first name.\n\n\n\nOnly certain documents provide this. |  | 
| middle_name_alias | string | MiddleNameAlias is the alias for the middle name.\n\n\n\nOnly certain documents provide this. |  | 
| family_name_alias | string | FamilyNameAlias is the alias for the family name.\n\n\n\nOnly certain documents provide this. |  | 
| weight | string | Weight is the weight as displayed on the document. Should contain weight and the unit.\n\n\n\nOnly certain documents provide this. |  | 
| height | string | Height is the height as displayed on the document. Should contain height and the unit.\n\n\n\nOnly certain documents provide this. |  | 
| eye_color | string | EyeColor is the eye color as displayed on the document.\n\n\n\nOnly certain documents provide this. |  | 
| structured_postal_address | object | StructuredPostalAddress is the postal address with the breakdown in address lines, post code and so on as well as the formatted address all in one line.\n\n\n\nSee details for `structured_postal_address` JSON properties below. |  | 
| document_type | string | DocumentType specifies the type of document. | “DRIVING_LICENCE” | 
| issuing_country | string | IssuingCountry is the country the document was issued in. Defined as an ISO/ICAO alpha-3 country code. | "GBR" | 
| document_number | string | DocumentNumber is the document number. | "EF1523467" | 
| expiration_date | string | ExpirationDate defines the date of expiry of the document in the form yyyy-mm-dd.\n\n\nNote: Few ID documents do not contain a visible expiration date. In these cases, the date may be returned as either `LIFETIME`, `NOT_PRESENT`, or omitted from the fields. | "2030-12-01"\n\n\n"LIFETIME"\n\n\n\n"NOT_PRESENT"\n\n\n\nnull | 
| date_of_issue | string | DateOfIssue is the date of issue of the document in the form yyyy-mm-dd. | "2001-12-01" | 
| issuing_authority | string | IssuingAuthority is the authority that issued the document. | "DVLA" | 
| mrz | object | MRZ provides the content of the machine readable zone, as displayed on the document. |  | 
| mrz.type | number | Type is type of MRZ, 2 lines or 3 lines.\n\n\n\n1=TD1\n\n2=TD3 |  | 
| mrz.line1 | string | MRZ line 1. |  | 
| mrz.line2 | string | MRZ line 2. |  | 
| mrz.line3 | string | MRZ line 3. |  | 
| organisation | string | Used primarily for Supplementary documents. | "Thames Water" | 
| personal_identification_number | string | Identification number of the document holder |  | 
| place_of_issue | string | If present, the place the ID document was issued |  | 
| document_template | string | Contains the fields of `front_page_name` and `back_page_name` listing the detected document template.\n\n\n\nThe relevant field will only appear if available/detected. |  | 
{% /table %}

## Address extraction

{% synced id="structuredpostaladdress" %}
{% /synced %}

{% code %}
{% tab language="json" title="Format 1" %}
{
    "address_format": 1,
    "building_number": "15a",
    "address_line1": "15a North Street",
    "town_city": "CARSHALTON",
    "postal_code": "SM5 2HW",
    "country_iso": "GBR"
    "country": "UK",
    "formatted_address": "15a North Street\nCARSHALTON\nSM5 2HW\nUK"
}
{% /tab %}
{% tab language="json" title="Format 2" %}
{
    "address_format": 2,
    "care_of": "S/O: Vipen Kumar Aggarwal",
    "building": "House No.86-A",
    "street": "Rajguru Nagar",
    "town_city": "Rajguru Nagar",
    "subdistrict": "Ludhiana",
    "district": "Ludhiana",
    "state": "Punjab",
    "postal_code": "141012",
    "post_office": "Rajguru Nagar",
    "country_iso": "IND",
    "country": "India",
    "formatted_address": "S/O: Vipen Kumar Aggarwal\nHouse No.86-A\nRajguru Nagar\nLudhiana\nPunjab\n141012\nIndia"
}
{% /tab %}
{% tab language="json" title="Format 3" %}
{
    "address_format": 3,
    "address_line1": "1512 Ferry Street",
    "town_city": "Anniston",
    "state": "AL",
    "postal_code": "36201",
    "country_iso": "USA",
    "country": "USA",
    "formatted_address": "1512 Ferry Street\nAnniston AL 36201\nUSA"
}
{% /tab %}
{% tab language="json" title="Format 4" %}
{
    "address_format": 4,
    "address_line1": "910 GOVERNMENT ST VICTORIA BC V8W 3Y8",
    "country_iso": "CAN",
    "country": "Canada",
    "formatted_address": "910 GOVERNMENT ST VICTORIA BC V8W 3Y8"
}
{% /tab %}
{% /code %}