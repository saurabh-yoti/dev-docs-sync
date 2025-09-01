---
type: page
title: Document fields
listed: true
slug: document-fields
description: 
index_title: Document fields
hidden: 
keywords: 
tags: 
---

## DocumentFields JSON properties

{% table %}
| Field name | Type | Description | Example | 
| ---- | ---- | ---- | ---- | 
| full_name | String | FullName contains given names and family name. | “Jon Jim Fred Foo” | 
| date_of_birth | String | DateOfBirth is the date of birth in the form _yyyy-mm-dd_, or _yyyy-mm_ or _yyyy_.\nA small percentage of documents do not provide the full DoB, if available in the visual zone or barcode data Yoti will always return the full DoB. | "2000-12-01" | 
| nationality | String | Nationality is the nationality expressed as an ISO/ICAO alpha-3 country code. \n\n\nNot all documents provide this. | "GBR" | 
| given_names | String | GivenNames contains first and middle names.\n\nNot all documents provide split given names and family name, in those cases only the full name field will be returned. | "Jon Jim Fred" | 
| first_name | String | FirstName is the first name only.\n\nOnly for those documents that provide first name and middle name split | "Jon" | 
| middle_name | String | MiddleName contains the middle names only.\n\nOnly for those documents that provide first name and middle names split. | "Jim Fred" | 
| family_name | String | FamilyName is the family name.\n\nNot all documents provide split given names and family name, in those cases only the full name field will be returned. | "Foo" | 
| place_of_birth | String | PlaceOfBirth is the place of birth, it may contain a country name or a city name or both.\n\nNot all documents provide this. | "London" | 
| country_of_birth | String | CountryOfBirth is the country of birth, as an ISO/ICAO alpha-3 country code.\n\n\nNot all documents provide this. | "GBR" | 
| gender | String | Gender is the gender and can be any of the following values:  "MALE", "FEMALE", "TRANSGENDER" or "OTHER". | "MALE" | 
| name_prefix | String | NamePrefix is the name prefix, for example a title.\n\nOnly certain documents provide this. | “Dr” | 
| name_suffix | String | NameSuffix is the name suffix.\n\nOnly certain documents provide this. | "Jr" | 
| first_name_alias | String | FirstNameAlias is the alias for the first name.\n\nOnly certain documents provide this. |  | 
| middle_name_alias | String | MiddleNameAlias is the alias for the middle name.\n\nOnly certain documents provide this. |  | 
| family_name_alias | String | FamilyNameAlias is the alias for the family name.\n\nOnly certain documents provide this. |  | 
| weight | String | Weight is the weight as displayed on the document. Should contain weight and the unit.\n\nOnly certain documents provide this. |  | 
| height | String | Height is the height as displayed on the document. Should contain height and the unit.\n\nOnly certain documents provide this. |  | 
| eye_color | String | EyeColor is the eye color as displayed on the document.\n\nOnly certain documents provide this. |  | 
| structured_postal_address | Object | StructuredPostalAddress is the postal address with the breakdown in address lines, post code and so on as well as the formatted address all in one line.\n\nSee details for structured_postal_address JSON properties below. |  | 
| document_type | String | DocumentType specifies the type of document. | “DRIVING_LICENCE” | 
| issuing_country | String | IssuingCountry is the country the document was issued in.\n\nDefined as an ISO/ICAO alpha-3 country code. | "GBR" | 
| document_number | String | DocumentNumber is the document number. | "EF1523467" | 
| expiration_date | String | ExpirationDate defines the date of expiry of the document in the form _yyyy-mm-dd_. | "2030-12-01" | 
| date_of_issue | String | DateOfIssue is the date of issue of the document in the form _yyyy-mm-dd_. | "2001-12-01" | 
| issuing_authority | String | IssuingAuthority is the authority that issued the document. | "DVLA" | 
| mrz | Object | MRZ provides the content of the machine readable zone, as displayed on the document. |  | 
| mrz.type | Number | Type is type of MRZ, 2 lines or 3 lines.\n\n1=TD1\n\n2=TD3 |  | 
| mrz.line1 | String | MRZ line 1. |  | 
| mrz.line2 | String | MRZ line 2. |  | 
| mrz.line3 | String | MRZ line 3. |  | 
| organisation | String | Organisation is the company that issued the document.\n\nThis will apply more to non-government backed documents such as utility bills |  | 
| personal_identification_number | String | PersonalIdentificationNumber the identification number of the document holder. |  | 
| parent_name | String | ParentName is the full parent's name (either mother or father). |  | 
{% /table %}

## IdentityDetails JSON properties

{% table widths="0,86,312" %}
| Field name | Type | Description | Example | 
| ---- | ---- | ---- | ---- | 
| full_name | String | FullName contains given names and family name. | “Jon Jim Fred Foo” | 
| date_of_birth | String | DateOfBirth is the date of birth in the form _yyyy-mm-dd_, or _yyyy-mm_ or _yyyy_.\nA small percentage of documents do not provide the full DoB, if available in the visual zone or barcode data Yoti will always return the full DoB. | "2000-12-01" | 
| given_names | String | GivenNames contains first and middle names.\n\nNot all documents provide split given names and family name, in those cases only the full name field will be returned. | "Jon Jim Fred" | 
| first_name | String | FirstName is the first name only.\n\nOnly for those documents that provide first name and middle name split | "Jon" | 
| middle_name | String | MiddleName contains the middle names only.\n\nOnly for those documents that provide first name and middle names split. | "Jim Fred" | 
| family_name | String | FamilyName is the family name.\n\nNot all documents provide split given names and family name, in those cases only the full name field will be returned. | "Foo" | 
| current_address | Object | CurrentAddress is the postal address with the breakdown in address lines, post code and so on as well as the formatted address all in one line.\n\nSee details for the Structured Postal Address JSON properties below. |  | 
{% /table %}

## StructuredPostalAddress JSON properties

{% table %}
| Name | Expected content type | Explanation | 
| ---- | ---- | ---- | 
| address_format | Number | AddressFormat is used to identify which fields may be present in the JSON object.\n\nSee table below that defines what format is used for each country. | 
| udprn | String | Udprn is the Unique Delivery Point Reference Number that identifies a property throughout its lifecycle. | 
| care_of | String | CareOf identifies the owner of the premises. | 
| building_number | String | The number of the building. | 
| building | String | The name of the building. | 
| street | String | Street is the name/number of the street the building is on. | 
| landmark | String | Landmark is a description used to describe the location of the building. | 
| address_line_1 | String | The first line of the address. | 
| address_line_2 | String | The second line of the address. | 
| address_line_3 | String | The third line of the address. | 
| address_line_4 | String | The fourth line of the address. | 
| address_line_5 | String | The fifth line of the address. | 
| address_line_6 | String | The sixth line of the address. | 
| locality | String | Locality is the area the building is in. | 
| town_city | String | TownCity is the town/city/village/hamlet/community/etc. that the building is in. | 
| subdistrict | String | Subdistrict is the sub-district the building is in. | 
| district | String | District is the district the building is in. | 
| state | String | State is the state/county the building is in. | 
| country | String | The country of the address. | 
| country_iso | String | CountryIso is the country the building is in. In ISO-3166-1 alpha-3 format. | 
| post_office | String | PostOffice is the post office that serves the area the building is in. | 
| postal_code | String | PostalCode is a code used by the country's postal service to aid in sorting and delivering mail (e.g. postcode, zipcode, pincode). | 
| formatted_address | String | FormattedAddress is the full address in a single human readable string in a format that is suitable for printing onto an envelope. | 
{% /table %}

The below defines the fields of a JSON structure that can be used to define any address. A subset of fields will be present in each case and address_format can be used to ascertain which ones for any given address. The country iso should not be used for this purpose..

We have four formats shown below:

{% table %}
| Field | Format 1 (UK) | Format 2 (INDIA) | Format 3 (USA) | Format 4 (ROW) | 
| ---- | ---- | ---- | ---- | ---- | 
| Countries that use these formats | GBR, JEY, IMN | IND | USA, AUS | All other countries | 
| address_format | 1 | 2 | 3 | 4 | 
| udprn | Optional |  |  |  | 
| care_of |  | Optional |  |  | 
| sub_building | Optional |  |  |  | 
| building_number | Optional |  |  |  | 
| building | Optional | Optional |  |  | 
| street |  | Optional |  |  | 
| landmark |  | Optional |  |  | 
| address_line_1 | Present |  | Present | Present | 
| address_line_2 | Optional |  | Optional | Optional | 
| address_line_3 | Optional |  |  | Optional | 
| address_line_4 |  |  |  | Optional | 
| address_line_n* |  |  |  | Optional | 
| locality | Present | Optional | Present |  | 
| town_city |  | Optional |  |  | 
| subdistrict |  | Optional |  |  | 
| district |  | Optional |  |  | 
| state | Optional | Optional | Present | Optional | 
| postal_code | Present | Present | Present |  | 
| post_office |  | Optional |  |  | 
| country_iso | Present | Present | Present | Present | 
| country | Present | Present | Present | Present | 
| formatted_address | Present | Present | Present | Present | 
{% /table %}