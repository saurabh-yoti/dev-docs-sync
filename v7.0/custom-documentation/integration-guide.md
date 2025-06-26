---
type: page
title: Integration guide
listed: true
slug: integration-guide
description: 
index_title: Integration guide
hidden: 
keywords: 
tags: 
---

Here you will be show how to:

1. Create a session
2. Fetch the session config
3. Set instructions
4. Get instructions

---

## Step 1: Session creation

You will need to collect from your users:

- A list of documentation the user will need to provide.

{% code %}
{% tab language="json" %}
{
    "session_deadline": "2022-09-11T23:59:59Z",
    "resources_ttl": "21040000",
    "ibv_options": {
        "support": "MANDATORY"
    },
    "user_tracking_id": "some_id",
    "notifications": {
        "endpoint": "https://some-domain.example",
        "topics": [
            "SESSION_COMPLETION"
        ]
    },
    "requested_checks": [
        {
            "type": "IBV_VISUAL_REVIEW_CHECK",
            "config": {
                "manual_check": "IBV"
            }
        },
        {
            "type": "PROFILE_DOCUMENT_MATCH",
            "config": {
                "manual_check": "IBV"
            }
        },
        {
            "type": "DOCUMENT_SCHEME_VALIDITY_CHECK",
            "config": {
                "manual_check": "IBV",
                "scheme": "UK_DBS"
            }
        }
    ],
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
        },
        {
            "type": "SUPPLEMENTARY_DOCUMENT",
            "document_types": [
                "UTILITY_BILL"
            ],
            "country_codes": [
                "GBR"
            ],
            "objective": {
                "type": "UK_DBS"
            }
        }
    ],
    "resources": {
        "applicant_profile": {
            "full_name": "John Doe",
            "date_of_birth": "1988-11-02",
            "name_prefix": "Mr",
            "structured_postal_address": {
                "address_format": 1,
                "building_number": "74",
                "address_line1": "AddressLine1",
                "town_city": "CityName",
                "postal_code": "E143RN",
                "country_iso": "GBR",
                "country": "United Kingdom",
                "formatted_address": "74\nAddressLine1\nAddressLine2\nAddressLine3\nCityName\nStateName\nE143RN\nGBR"
            }
        }
    }
}
{% /tab %}
{% /code %}

{% table widths="146" %}
| Parameter | Description | 
| ---- | ---- | 
| session_deadline | This is in a date format. \n\nThe user has up until this date to complete the session. \n\nNote: we also have client_session_token_ttl (seconds) to set your session expiry. | 
| resources_ttl | This is in seconds. \n\nThis sets how long any media is held by Yoti. It has to be at least 24 hours more than the session deadline or token. | 
| ibv_options | To enable IBV services. | 
| user_tracking_id | This is a string format. \n\nThis allows the relying business backend to track the same user across multiple sessions. **Note:** This should not contain any personal identifiable information. | 
| notifications | This service optionally posts an update notification every time the session state changes, based on the selected subscription topic. We recommend you use SESSION_COMPLETION.  This is triggered when all tasks and all checks inside of a given session have been completed. | 
{% /table %}

### Request checks

This service provides three checks, please see below for features available for you to configure within your session.

{% table widths="310,0,204" %}
| Check Name | Description | Resources | In person check | 
| ---- | ---- | ---- | ---- | 
| PROFILE_DOCUMENT_MATCH | Visual check of the documents the applicant brought with them matches the submitted applicant profile. | 3x Document Resource | ✅ | 
| DOCUMENT_SCHEME_VALIDITY_CHECK | Checks the documents themselves fit within the standards of that scheme. E.g. validity of certain documents. | 3x Document Resource | ✅ | 
| IBV_VISUAL_REVIEW_CHECK | A visual review of the document. | 3x Document Resource | ✅ | 
{% /table %}

For a full extended list of all the checks and services available please check our or[ In branch verification documentation](https://developers.yoti.com/identity-verification/in-branch-overview) and our [Identity verification documentation.](https://developers.yoti.com/identity-verification/overview#feature-list)

### Required documents

In the example below and above, three documents are being set for the applicant (each document is one object in the list). 

{% code %}
{% tab language="json" %}
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
        },
        {
            "type": "SUPPLEMENTARY_DOCUMENT",
            "document_types": [
                "UTILITY_BILL"
            ],
            "country_codes": [
                "GBR"
            ],
            "objective": {
                "type": "UK_DBS"
            }
        }
    ],
{% /tab %}
{% /code %}

{% table %}
| Parameter | Description | 
| ---- | ---- | 
| type | See table below. | 
| country_code | Country code of document country | 
| document_type | Document types explained in table below. | 
| objective | **UK_DBS** must be set. | 
{% /table %}

If this was sent to our API, then the user would need to bring these documents:

- UK Passport
- UK Driving Licence
- UK Utility Bill

{% table widths="254,196" %}
| Document | API Mapping | API Type | 
| ---- | ---- | ---- | 
| Passport | PASSPORT | ID_DOCUMENT | 
| Driving license | DRIVING_LICENCE | ID_DOCUMENT | 
| National ID | NATIONAL_ID | ID_DOCUMENT | 
| British residence permit | RESIDENCE_PERMIT | ID_DOCUMENT | 
| Irish Passport card | NATIONAL_ID | ID_DOCUMENT | 
| Utility bill | UTILITY_BILL | SUPPLEMENTARY_DOCUMENT | 
| Bank statement | BANK_STATEMENT | SUPPLEMENTARY_DOCUMENT | 
| Council tax bill | COUNCIL_TAX_BILL | SUPPLEMENTARY_DOCUMENT | 
| Phone bill | PHONE_BILL | SUPPLEMENTARY_DOCUMENT | 
| HM Forces ID Card | MILITARY_CARD | SUPPLEMENTARY_DOCUMENT | 
| PASS Card | SUPPLEMENTARY_PASS_CARD | SUPPLEMENTARY_DOCUMENT | 
| Firearms Licence | FIREARMS_LICENCE | SUPPLEMENTARY_DOCUMENT | 
| Birth Certificate (within 12 months of DOB) | BIRTH_CERTIFICATE_ISSUED_WITHIN_12_MONTHS_OF_BIRTH | SUPPLEMENTARY_DOCUMENT | 
| Birth Certificate (issued after 12 months from DOB) | BIRTH_CERTIFICATE | SUPPLEMENTARY_DOCUMENT | 
| Adoption Certificate | ADOPTION_CERTIFICATE | SUPPLEMENTARY_DOCUMENT | 
| Paper Driving Licence | PAPER_DRIVING_LICENCE | SUPPLEMENTARY_DOCUMENT | 
| Marriage/Civil Partnership Certificate | MARRIAGE_CERTIFICATE | SUPPLEMENTARY_DOCUMENT | 
| Bank Opening Letter | ACCOUNT_OPENING_LETTER | SUPPLEMENTARY_DOCUMENT | 
| Benefit Statement | BENEFIT_STATEMENT | SUPPLEMENTARY_DOCUMENT | 
| Mortgage Statement | MORTGAGE_STATEMENT | SUPPLEMENTARY_DOCUMENT | 
| Financial Statement | FINANCIAL_STATEMENT | SUPPLEMENTARY_DOCUMENT | 
| P45 or P60 Statement | EMPLOYEE_TAX_FORM | SUPPLEMENTARY_DOCUMENT | 
| Employment Sponsorship Letter | EMPLOYMENT_SPONSORSHIP_LETTER | SUPPLEMENTARY_DOCUMENT | 
| Immigration Document/Visa/Work Permit | IMMIGRATION_DOCUMENT | SUPPLEMENTARY_DOCUMENT | 
| Education letter | EDUCATION_LETTER | SUPPLEMENTARY_DOCUMENT | 
| DVLA V5 or V5C/2 | DVLA_FORM | SUPPLEMENTARY_DOCUMENT | 
{% /table %}

### Applicant profile

This is nested inside of the **resources** object. The applicant profile is made up of the below fields. 

{% table %}
| Field name | Type | Description | Example | Optional | 
| ---- | ---- | ---- | ---- | ---- | 
| name_prefix | string | Prefix | “Mr” / “Ms” / … |  | 
| full_name | string | Full name of user | Jon Jim Foo |  | 
| date_of_birth | string | DateOfBirth is the date of birth in the form yyyy-mm-dd. | 2000-12-01 |  | 
| given_names | string | Given names of user | Jon Jim | ✅ | 
| first_name | string | First name of user | Jon | ✅ | 
| middle_name | string | Middle name of user | Jim | ✅ | 
| family_name | string | Family name of user | Foo | ✅ | 
| structured_postal_address | object | StructuredPostalAddress is the postal address with the breakdown in address lines, post code and so on as well as the formatted address all in one line.\n\nSee details for structured_postal_address JSON properties below. | See below |  | 
{% /table %}

#### Structured postal address

{% table widths="136,0" %}
| Field | Type | Description | 
| ---- | ---- | ---- | 
| address_format | number | AddressFormat is used to identify which fields may be present in the JSON object.\n\nSee table below that defines what format is used for each country. | 
| udprn | string | Udprn is the Unique Delivery Point Reference Number that identifies a property throughout its lifecycle | 
| care_of | string | CareOf identifies the owner of the premises. | 
| sub_building | string | SubBuilding is used when the building is divided into smaller units (e.g. a block of flats) to identify the sub unit. | 
| building_number | string | BuildingNumber is the number of the building. | 
| building | string | Building is the name/number of the building. | 
| street | string | Street is the name/number of the street the building is on. | 
| landmart | string | Landmark is a description used to describe the location of the building. | 
| address_line_1 | string | AddressLine1 is the first line of the address. | 
| address_line_2 | string | AddressLine2 is the first line of the address. | 
| address_line_3 | string | AddressLine3 is the first line of the address. | 
| address_line_4 | string | AddressLine4 is the first line of the address. | 
| address_linen | string | AddressLineN is the first line of the address. | 
| locality | string | Locality is the area the building is in. | 
| town_city | string | TownCity is the town/city/village/hamlet/community/etc. that the building is in. | 
| subdistrict | string | Subdistrict is the sub-district the building is in. | 
| district | string | District is the district the building is in. | 
| state | string | State is the state/county the building is in. | 
| postal_code | string | PostalCode is a code used by the country's postal service to aid in sorting and delivering mail (e.g. postcode, zipcode, pincode). | 
| post_office | string | PostOffice is the post office that serves the area the building is in. | 
| country_iso | string | CountryIso is the country the building is in. In ISO-3166-1 alpha-3 format. | 
| country | string | Country is the country the building is in. Localised. | 
| formatted_address | string | FormattedAddress is the full address in a single human readable string in a format that is suitable for printing onto an envelope. | 
{% /table %}

The below defines the fields of a JSON structure that can be used to define any address. A subset of fields will be present in each case and address_format can be used to ascertain which ones for any given address. The country iso should not be used for this purpose.

We have four formats shown below:

{% table %}
| Field | Format 1 (UK) | Format 2 (INDIA) | Format 3 (USA) | Format 4 (ROW) | 
| ---- | ---- | ---- | ---- | ---- | 
| udprn | Optional |  |  |  | 
| care_of |  | Optional |  |  | 
| sub_building | Optional |  |  |  | 
| building_number | Optional |  |  |  | 
| building | Optional | Optional |  |  | 
| street |  | Optional |  |  | 
| landmart |  | Optional |  |  | 
| address_line_1 | Present |  | Present | Present | 
| address_line_2 | Optional |  | Optional | Optional | 
| address_line_3 | Optional |  |  | Optional | 
| address_line_4 |  |  |  | Optional | 
| address_linen |  |  |  | Optional | 
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

**Note:**At least one building, sub_building or building_number of these must be present for type 1

### Example response

If the request is successful and a session is generated the API will send a response in the form:

{% code %}
{% tab language="json" %}
{
  "client_session_token_ttl": 599,
  "client_session_token": "<uuid>",
  "session_id": "<uuid>"
}
{% /tab %}
{% /code %}

---

## Step 2: Fetch session config

This endpoint will retrieve the session configuration, and also provide some resources.  Please take note of the **id** of each **required_resources**.

{% code %}
{% tab language="http" %}
GET https://api.yoti.com/sessions/{sessionId}/configuration
{% /tab %}
{% /code %}

{% code %}
{% tab language="json" %}
{
    "session_id": "27af32df-b9fb-44f9-8387-00b1a5afc276",
    "client_session_token_ttl": 18700689,
    "requested_checks": [
        "IBV_VISUAL_REVIEW_CHECK",
        "DOCUMENT_SCHEME_VALIDITY_CHECK",
        "PROFILE_DOCUMENT_MATCH"
    ],
    "applicant_profile": {
        "media": {
            "id": "01dfb19d-98f0-4908-8738-1a131461ad2e",
            "type": "JSON",
            "created": "2022-02-07T12:57:29Z",
            "last_updated": "2022-02-07T12:57:29Z"
        }
    },
    "capture": {
        "required_resources": [
            {
                "type": "ID_DOCUMENT",
                "id": "f9c70bd6-43a1-4655-9676-083aafb09df7",
                "state": "REQUIRED",
                "allowed_sources": [
                    {
                        "type": "IBV"
                    }
                ],
                "requested_tasks": [],
                "ibv_client_assessments": [
                    {
                        "type": "IBV_VISUAL_REVIEW_CHECK",
                        "state": "REQUIRED"
                    },
                    {
                        "type": "DOCUMENT_SCHEME_VALIDITY_CHECK",
                        "state": "REQUIRED",
                        "scheme": "UK_DBS"
                    },
                    {
                        "type": "PROFILE_DOCUMENT_MATCH",
                        "state": "REQUIRED"
                    }
                ],
                "supported_countries": [
                    {
                        "code": "GBR",
                        "supported_documents": [
                            {
                                "type": "PASSPORT",
                                "is_strictly_latin": true
                            }
                        ]
                    }
                ],
                "allowed_capture_methods": "CAMERA",
                "attempts_remaining": {
                    "RECLASSIFICATION": 2,
                    "GENERIC": 2
                }
            },
            {
                "type": "ID_DOCUMENT",
                "id": "b4e62309-3ed7-4de8-b85c-918a07df9e22",
                "state": "REQUIRED",
                "allowed_sources": [
                    {
                        "type": "IBV"
                    }
                ],
                "requested_tasks": [],
                "ibv_client_assessments": [
                    {
                        "type": "IBV_VISUAL_REVIEW_CHECK",
                        "state": "REQUIRED"
                    },
                    {
                        "type": "DOCUMENT_SCHEME_VALIDITY_CHECK",
                        "state": "REQUIRED",
                        "scheme": "UK_DBS"
                    },
                    {
                        "type": "PROFILE_DOCUMENT_MATCH",
                        "state": "REQUIRED"
                    }
                ],
                "supported_countries": [
                    {
                        "code": "GBR",
                        "supported_documents": [
                            {
                                "type": "DRIVING_LICENCE",
                                "is_strictly_latin": true
                            }
                        ]
                    }
                ],
                "allowed_capture_methods": "CAMERA",
                "attempts_remaining": {
                    "RECLASSIFICATION": 2,
                    "GENERIC": 2
                }
            },
            {
                "type": "SUPPLEMENTARY_DOCUMENT",
                "id": "63f444c9-5a2a-48f7-acc9-26153032491f",
                "state": "REQUIRED",
                "allowed_sources": [
                    {
                        "type": "IBV"
                    }
                ],
                "requested_tasks": [],
                "ibv_client_assessments": [
                    {
                        "type": "IBV_VISUAL_REVIEW_CHECK",
                        "state": "REQUIRED"
                    },
                    {
                        "type": "DOCUMENT_SCHEME_VALIDITY_CHECK",
                        "state": "REQUIRED",
                        "scheme": "UK_DBS"
                    },
                    {
                        "type": "PROFILE_DOCUMENT_MATCH",
                        "state": "REQUIRED"
                    }
                ],
                "document_types": [
                    "UTILITY_BILL"
                ],
                "country_codes": [
                    "GBR"
                ],
                "objective": {
                    "type": "UK_DBS"
                }
            }
        ],
        "biometric_consent": "NOT_REQUIRED"
    },
    "sdk_config": {
        "primary_colour": "#D71440",
        "locale": "en-GB",
        "hide_logo": false,
        "allow_handoff": false
    },
    "track_ip_address": true
}
{% /tab %}
{% /code %}

---

## Step 3: Set instructions

e're using the **id** from step 2 to populate the **requirement_id** field in each document object. You should also use the same type, document type and country code as set in the create session.

{% code %}
{% tab language="http" %}
PUT https://api.yoti.com/sessions/{sessionId}/instructions
{% /tab %}
{% /code %}

{% code %}
{% tab language="json" %}
{
    "documents": [
        {
            "requirement_id": "f9c70bd6-43a1-4655-9676-083aafb09df7",
            "document": {
                "type": "ID_DOCUMENT",
                "country_code": "GBR",
                "document_type": "PASSPORT"
            }
        },
        {
            "requirement_id": "b4e62309-3ed7-4de8-b85c-918a07df9e22",
            "document": {
                "type": "ID_DOCUMENT",
                "country_code": "GBR",
                "document_type": "DRIVING_LICENCE"
            }
        },
        {
            "requirement_id": "63f444c9-5a2a-48f7-acc9-26153032491f",
            "document": {
                "type": "SUPPLEMENTARY_DOCUMENT",
                "country_code": "GBR",
                "document_type": "UTILITY_BILL"
            }
        }
    ],
    "branch": {
        "type": "UK_POST_OFFICE",
        "fad_code": "1010034",
        "name": "Moorgate",
        "address": "45 London Wall, London, Greater London",
        "post_code": "EC2M 5TE",
        "location": {
            "latitude": "51.51706",
            "longitude": "-0.08797"
        }
    },
    "contact_profile": {
        "first_name": "John",
        "last_name": "Doe",
        "email": "john.doe@example.com"
    }
}
{% /tab %}
{% /code %}

---

## Step 4: Get instructions

This will allow you to retrieve the instructions as a PDF once set. See PDF example below.

{% code %}
{% tab language="http" %}
GET https://api.yoti.com/sessions/{sessionId}/instructions/pdf
{% /tab %}
{% /code %}

#### PDF example

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1644259411/v2_2762/ehbjvbyy77qoqzhzimt6.png" caption="PDF example" mode="responsive" height="1372" width="958" %}
{% /image %}