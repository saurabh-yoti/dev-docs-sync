---
type: page
title: Yoti Attributes Explained
listed: true
slug: yoti-attributes-explained
description: 
index_title: Yoti Attributes Explained
hidden: 
keywords: 
tags: 
---

This section describes all the attributes Yoti supports in more detail. There is a small explanation of each attribute and what the content type is.

### [General attributes](https://developers.yoti.com/yoti-app-integration/yoti-app-integration#general-attributes)

{% table %}
| Name | Content Type | Explanation | 
| ---- | ---- | ---- | 
| date_of_birth | DATE | Date of birth of the user. | 
| email_address | STRING | The user's verified email address. | 
| family_name | STRING | Corresponds to primary name in passport, and surname in English. | 
| full_name | STRING | &lt;p&gt;The user's full name. If family_name/given_names are&nbsp;&lt;span&gt;present, this will be equal to the string ${given_names} + " " + ${family_name}.&lt;/span&gt;&lt;/p&gt; | 
| gender | STRING | Corresponds to the gender in the registered document; will be one of the strings "MALE", "FEMALE", "TRANSGENDER" or "OTHER". | 
| given_names | STRING | Corresponds to secondary names in passport, and first/middle names in English. | 
| nationality | STRING | Corresponds to the nationality in the passport. ISO-3166-1 alpha-3 code with ICAO9303 (passport) extensions. See &lt;a href="https://en.wikipedia.org/wiki/ISO_3166-1_alpha-3"&gt;Wikipedia page for ISO-3166-1 alpha-3 codes&lt;/a&gt;, and see &lt;a href="https://www.icao.int/publications/Documents/9303_p3_cons_en.pdf"&gt;ICAO 9303 part 3&lt;/a&gt; (section 5 part A) for the extended list of codes. | 
| phone_number | STRING | The user's phone number, as verified at registration time. This will be a number in &lt;a href="https://en.wikipedia.org/wiki/E.164#Numbering_formats"&gt;E.164&lt;/a&gt;&nbsp;format (i.e. + for international prefix and no spaces, e.g. "+447777123456"). | 
| selfie | JPEG | Photograph of user, encoded as a JPEG image. | 
| age | INT | Date&nbsp;of birth e.g. 22. | 
| age_over:[1-999] | STRING | Date of birth e.g. over 18. | 
{% /table %}

### [Address attributes](https://developers.yoti.com/yoti-app-integration/yoti-app-integration#address-attributes)

Yoti has two options to show clients addresses:

1) Full address - the address as a string.

2) Structured address - a broken down version of an address.

There is a small explanation of each attribute and what the content type is.

{% table %}
| Name | Expected content type | Explanation | 
| ---- | ---- | ---- | 
| building_number | STRING | The number of the building | 
| building_name | STRING | The name of the building | 
| sub_building_name | STRING&lt;br&gt; | The subtitle of the building | 
| address_line_1 | STRING | The first line of the address | 
| address_line_2 | STRING | The second line of the address | 
| address_line_3 | STRING | The third line of the address | 
| town | STRING | The town of the address | 
| country | STRING | The country of the address | 
| postal_code | STRING | The postcode for the address | 
| postal_address | STRING | The full address | 
| structured_postal_address | JSON | The full address in both machine readable form and human readable form | 
{% /table %}

The below defines the fields of a JSON structure that can be used to define any address. A subset of fields will be present in each case and address_format can be used to ascertain which ones for any given address, the country_iso should not be used for this purpose.

We have four formats shown below:

{% table %}
| Field | Format 1 (UK) | Format 2 (IND) | Format 3 (USA) | Format 4 (ROW) | 
| ---- | ---- | ---- | ---- | ---- | 
| udprn | Optional |  |  |  | 
| care_of |  | Optional |  |  | 
| sub_building | Optional |  |  |  | 
| building_number | Optional |  |  |  | 
| building | Optional | Optional |  |  | 
| street |  | Optional |  |  | 
| landmart |  | Optional |  |  | 
| address_line_1 | Present |  | Present | Present | 
| address_line_2 | Optional | &lt;br&gt; | Optional | Optional | 
| address_line_3 | Optional |  |  | Optional | 
| address_line_4 |  |  |  | Optional | 
| address_linen |  |  |  | Optional | 
| locality | Present | Optional | Present | &lt;br&gt; | 
| town_city |  | Optional |  |  | 
| subdistrict |  | Optional |  |  | 
| district&lt;br&gt; |  | Optional |  |  | 
| state | Optional | Optional | Present | Optional | 
| postal_code | Present | Present | Present |  | 
| post_office |  | Optional |  |  | 
| country_iso | Present | Present | Present | Present | 
| country | Present | Present | Present | Present | 
| formatted_address | Present | Present | Present | Present | 
{% /table %}

### [Format 1 Address attribute](https://developers.yoti.com/yoti-app-integration/yoti-app-integration#format-1-address-attribute)

The UK address format is as shown below with an example:

{% code %}
{% tab language="json" %}
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
{% /code %}

### [Format 2 Address attribute](https://developers.yoti.com/yoti-app-integration/yoti-app-integration#format-2-address-attribute)

The India address format is as shown below with an example:

{% code %}
{% tab language="json" %}
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
{% /code %}

### [Format 3 Address attribute](https://developers.yoti.com/yoti-app-integration/yoti-app-integration#format-3-address-attribute)

The US address format is as shown below with an example:

{% code %}
{% tab language="json" %}
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
{% /code %}

---

## [Source and verifiers](https://developers.yoti.com/yoti-app-integration/yoti-app-integration#source-and-verifiers)

Within the SDKs and in our Yoti Hub we allow you to see the sources and verifiers of each of the attributes the user has shared with your company.

Below represents an explanation of what is shown through our SDKs.

### [Source](https://developers.yoti.com/yoti-app-integration/yoti-app-integration#source)

{% table %}
| Value | Description | 
| ---- | ---- | 
| USER_PROVIDED | UserProvided source indicates that the attribute value to which this anchor is attached was provided by the user. | 
| PASSPORT | &lt;p&gt;Passport source indicates that the attribute value to which this anchor is attached was extracted from a passport.&lt;/p&gt;&lt;p&gt;The two subtypes available are via: OCR or NFC.&lt;/p&gt; | 
| DRIVING_LICENCE | DrivingLicence source indicates that the attribute value to which this anchor is attached was extracted from a driving licence. | 
| NATIONAL_ID | NationalID source with a subtype of Aadhaar indicates that the attribute value to which this anchor is attached was extracted from a Aadhaar card/document. | 
| PASSCARD | CitizenCard source indicates that the attribute value to which this anchor is attached was extracted from a CitizenCard card/document. | 
{% /table %}

### [Verifiers](https://developers.yoti.com/yoti-app-integration/yoti-app-integration#verifiers)

{% table %}
| Value | Description | 
| ---- | ---- | 
| YOTI_ADMIN | YotiAdmin verifier indicates that the attribute value has been verified by the Yoti admin team.&lt;br&gt; | 
| YOTI_IDENTITY&lt;br&gt; | YotiIdentity verifier indicated that the attribute value has been verified with a recognised identity database, or otherwise known as an Identity Verifier (IDV). | 
| YOTI_OTP | OTP verifier indicates that the attribute value has been verified by sending a generated one time passcode to it and checking it has been received. | 
| YOTI_UIDAI&lt;br&gt; | YotiUIDAI verifier indicates that the attribute value has been verified with the Indian UIDAI system. | 
{% /table %}