---
type: page
title: Identity Profile Report
listed: true
slug: identity-profile-report
description: 
index_title: Identity Profile Report
hidden: 
keywords: 
tags: 
---

## Identity Profile Report JSON

The identity profile report JSON object is the following:

## IdentityProfileReport

{% table %}
| Field | Type | Required | Description | 
| ---- | ---- | ---- | ---- | 
| identity_assertion | object | Yes | Identity attributes. | 
| current_name | object | No | Current legal name extracted from identity documents | 
| date_of_birth | string | Yes | Date of birth as yyyy-mm-dd. | 
| current_address | object | No | Current address, provided or extracted from a document. | 
| verification_reports | []object | Yes | List of verification report objects. Returned instead of verification_report when advanced identity profile requirements are requested. | 
| verification_report | object | Yes | Certifies the achieved verification level for this identity. | 
{% /table %}

### current_name

{% table %}
| Field | Type | Required | Description | 
| ---- | ---- | ---- | ---- | 
| given_names | string | Yes | Given names of the user. Includes first and middle names. | 
| first_name | string | No | First name only. | 
| middle_name | string | No | Middle name(s) only. | 
| family_name | string | No | Family name of the user. | 
| full_name | string | No | Full name of the user. Includes all given names and family name. | 
{% /table %}

### current_address

{% table %}
| Field | Type | Required | Description | 
| ---- | ---- | ---- | ---- | 
| address | object | Yes | See structured postal address definition | 
| move_in | string | No | Date from when the user started living at this address. Format: yyyy-mm-dd. | 
{% /table %}

### verification_report

{% table %}
| Field | Type | Required | Description | 
| ---- | ---- | ---- | ---- | 
| report_id | string | Yes | Unique identifier for this report. | 
| timestamp | string | Yes | Time at which this report was generated. RFC3339 UTC Timestamp e.g.: 2006-01-02T15:04:05Z | 
| subject_id | string | No | Subject identifier provided by the RP at session creation time. | 
| address_verification | object | No | Defines whether the address was verified and links to verification evidence. | 
| trust_framework | string | Yes | Defines under which trust framework this identity was verified. Enum: UK_TFIDA, YOTI_GLOBAL | 
| schemes_compliance | []object | Yes | Defines which schemes (of the requested ones) this identity profile satisfies. | 
| assurance_process | object | Yes | Provides details on how the confidence for this identity profile was achieved. | 
| evidence | object | Yes | Provides the collection of evidence that supports this identity. | 
| authentication_reports | []object | No | List of authentication report objects. Returned instead of authentication_report when advanced identity profile requirements are requested. | 
| authentication_report | object | No | Provides the level of authentication reached according to the specified policy. | 
{% /table %}

#### address_verification

{% table %}
| Field | Type | Required | Description | 
| ---- | ---- | ---- | ---- | 
| current_address_verified | boolean | Yes | Defines whether the current address was verified or not. | 
| evidence_links | []string | No | Provides the list of evidence supporting this address verification. | 
{% /table %}

#### schemes_compliance

{% table %}
| Field | Type | Required | Description | 
| ---- | ---- | ---- | ---- | 
| requirements_met | boolean | Yes | Asserts whether the identity scheme requirements were met or not. | 
| requirements_not_met_info | string | No | Provides info on why the scheme requirements were not met. | 
| scheme | object | Yes | Defines the identity scheme. | 
{% /table %}

#### scheme

{% table %}
| Field | Type | Required | Description | 
| ---- | ---- | ---- | ---- | 
| type | string | Yes | Defines which scheme this identity profile should satisfy. | 
| objective | string | No | Defines the specific objective within the scheme. | 
| label | string | No | Label provided at request time to uniquely identify this identity profile. | 
| config | object | No | See config definition provided elsewhere. | 
{% /table %}

#### assurance_process

{% table %}
| Field | Type | Required | Description | 
| ---- | ---- | ---- | ---- | 
| level_of_assurance | string | Yes | Level of assurance achieved. Examples: "MEDIUM", "HIGH". | 
| policy | string | Yes | Policy defines the rules followed in the assurance process. Example: GPG45. | 
| procedure | string | No | Defines what procedure, within the policy rules, was followed. Example for GPG45: M1B, H1A. | 
| assurance | []object | No | Provides a breakdown of the assurance. | 
{% /table %}

#### assurance

{% table %}
| Field | Type | Required | Description | 
| ---- | ---- | ---- | ---- | 
| type | string | Yes | Defines what type of assurance this is. | 
| classification | string | No | Defines how much weight this assurance provides for the specific type. | 
| evidence_links | []string | No | Provides the list of evidence that this assurance is based upon. | 
{% /table %}

#### evidence

{% table %}
| Field | Type | Required | Description | 
| ---- | ---- | ---- | ---- | 
| face | object | No | Face evidence details. | 
| documents | []object | No | Document evidence details. | 
| electronic_records | []object | No | Electronic record evidence details. | 
{% /table %}

#### face

{% table %}
| Field | Type | Required | Description | 
| ---- | ---- | ---- | ---- | 
| evidence_id | string | Yes | Unique ID identifying this evidence. | 
| initial_liveness | object | Yes | Provides the first passed liveness. | 
| last_matched_liveness | object | No | Provides the last passed liveness. | 
| verifying_org | string | Yes | Organisation responsible for capturing and verifying liveness and the face. | 
| media_ids | []string | No | Reference to media IDs. | 
| audit_ids | []string | No | Reference to audit_ids for audit purposes. | 
{% /table %}

#### initial_liveness and last_matched_liveness

{% table %}
| Field | Type | Required | Description | 
| ---- | ---- | ---- | ---- | 
| type | string | Yes | Defines the type of liveness. Enum: ZOOM, STATIC, ACTIVE, THREE_WORDS | 
| timestamp | string | Yes | Defines the timestamp at which it was approved. | 
{% /table %}

#### documents

{% table %}
| Field | Type | Required | Description | 
| ---- | ---- | ---- | ---- | 
| evidence_id | string | Yes | Unique ID identifying this evidence. | 
| timestamp | string | Yes | Timestamp of when this document was added. | 
| document_fields | object | Yes | See document fields definition | 
| passed_checks | []object | Yes | List of passed checks for this document. | 
| verifying_org | string | Yes | Organisation responsible for capturing and verifying this document. | 
| media_ids | []string | No | Reference to media IDs. | 
| audit_ids | []string | No | Reference to audit_ids for audit purposes. | 
{% /table %}

#### passed_checks

{% table %}
| Field | Type | Required | Description | 
| ---- | ---- | ---- | ---- | 
| check | string | Yes | Enum: MANUAL_VISUAL_DOCUMENT_AUTHENTICITY, CHIP_DIGITAL_SIGNATURE, ISSUING_AUTHORITY, DOCUMENT_IN_DATE, FRAUD_DOCUMENTS_LIST, MANUAL_FACE_MATCH, AUTOMATED_FACE_MATCH, AUTOMATED_FACE_MATCH_HIGHER_THRESHOLD | 
{% /table %}

#### electronic_records

{% table %}
| Field | Type | Required | Description | 
| ---- | ---- | ---- | ---- | 
| evidence_id | string | Yes | Unique ID identifying this evidence. | 
| timestamp | string | Yes | Timestamp of when this electronic record was queried. | 
| identity_details | object | Yes | Identity details used in the query. See definition elsewhere. | 
| verifying_org | string | Yes | Organisation responsible for capturing and verifying this identity. | 
| provider_org | string | No | Third party organisation providing the identity check. | 
| media_ids | []string | No | Reference to media IDs. | 
| audit_ids | []string | No | Reference to audit_ids for audit purposes. | 
{% /table %}

## authentication_report

{% table %}
| Field | Type | Required | Description | 
| ---- | ---- | ---- | ---- | 
| report_id | string | Yes | Unique identifier for this report. | 
| timestamp | string | Yes | Time at which this report was generated. RFC3339 UTC Timestamp e.g.: 2006-01-02T15:04:05Z | 
| level | string | Yes | Level of authentication reached. Examples: "MEDIUM", "HIGH". | 
| policy | string | Yes | Policy defines the rules used to assess the level of authentication. Example: "GPG44". | 
| trust_framework | string | Yes | Defines under which trust framework this identity was authenticated. Enum: UK_TFIDA, YOTI_GLOBAL | 
{% /table %}