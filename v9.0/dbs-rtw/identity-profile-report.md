---
type: page
title: Identity profile report
listed: true
slug: identity-profile-report
description: 
index_title: Identity profile report
hidden: 
keywords: 
tags: 
---

The identity profile report JSON object is the following:

{% table widths="249,0,0" %}
| Parameter | Type | Description | Mandatory | 
| ---- | ---- | ---- | ---- | 
| IdentityProfileReport | Object |  | Required | 
| identity_assertion | Object | Identity attributes. | Optional | 
| current_name | Object | Current legal name extracted from identity documents | Required | 
| given_names | String | GivenNames are the given names of the user. Includes first and middle names. | Optional | 
| first_name | String | FirstName is the first name only. | Optional | 
| middle_name | String | MiddleName is the middle name/s only. | Optional | 
| family_name Optional | String | FamilyName is the family name of the user. | Optional | 
| full_name | String | FullName is the full name of the user.\n\n\n\nThis includes all given names and family name. | Required | 
| date_of_birth | String | Date of birth as yyyy-mm-dd. | Required | 
| current_address | Object | Current address, provided or extracted from a document. | Optional | 
| address | Object | See structured postal address definition provided below. | Required | 
| move_in | String | MoveIn is the date from when the user started living at this address.\n\n\n\nIt may not be available.\n\nDate in the form of yyyy-mm-dd. | Required | 
| verification_report | Object | Verification report certifies the achieved verification level for this identity. | Required | 
| report_id | String | Unique identifier for this report. | Required | 
| timestamp | String | Time at which this report was generated. RFC3339 UTC Timestamp e.g.: 2006-01-02T15:04:05Z | Required | 
| subject_id | String | Subject identifier provided by the RP at\n\n\n\nsession creation time. | Optional | 
| address_verification | Object | Defines whether the address was verified and links to verification evidence.\n\n\n\nNot provided if address is not part of the identity assurance. | Optional | 
| current_address_verified | Boolean | Defines whether the current address was verified or not. | Required | 
| evidence_links | []String | Provides the list of evidence supporting this address verification. | Optional | 
| trust_framework | String | Defines under which trust framework\n\nthis identity was verified. As defined at session creation time.\n\nEnum: UK_TFIDA | Required | 
| schemes_compliance | []Object | Defines which schemes (of the requested ones) this identity profile satisfies. | Required | 
| scheme | Object | Scheme defines the identity scheme | Required | 
| requirements_met | Boolean | Asserts whether the identity scheme requirements were met or not. | Required | 
| requirements_not_met_info | String | Provides info on why the scheme requirements were not met. | Optional | 
| requirements_not_met_details | []Object | Provides a list of failure reason details in the event the scheme compliance could not be met\n\n\n\nSee [failure reasons](/dbs-rtw/error-responses) response for additional details | Required | 
| assurance_process | Object | Provides details on how the confidence \n\nfor this identity profile was achieved | Required | 
| level_of_assurance | String | Level of assurance achieved.\n\nExamples: "MEDIUM", "HIGH". | Required | 
| policy | String | Policy defines the rules followed in the assurance process. Example: GPG45. | Required | 
| procedure | String | Defines what procedure, within the policy rules, was followed. Example for GPG45: M1B, H1A. | Optional | 
| assurance | []Object | Assurance provides a breakdown of the assurance. | Optional | 
| type | String | Type defines what type of assurance this is. Possible types of assurance for the\n\nUK Trust Framework: EVIDENCE_STRENGTH, EVIDENCE_VALIDITY, IDENTITY_FRAUD, ACTIVITY_HISTORY, VERIFICATION. | Required | 
| classification | String | Classification defines how much weight this assurance provides for the specific type. | Optional | 
| evidence_links | []String | Provides the list of evidence that this assurance is based upon. | Optional | 
| evidence | Object | Evidence provides the collection of evidence that supports this identity. | Required | 
| face | Object |  | Optional | 
| evidence_id | String | Unique ID identifying this evidence. | Required | 
| initial_liveness | Object | Provides the first passed liveness. | Required | 
| type | String | Defines the type of liveness.\n\nEnum: ZOOM,STATIC,ACTIVE,THREE_WORDS | Required | 
| timestamp | String | Defines the timestamp at which it was approved. | Required | 
| last_matched_liveness | Object | Provides the last passed liveness. The face captured in any subsequent liveness has to match the origin face capture. | Optional (Digital ID only) | 
| type | String | Defines the type of liveness.\n\nEnum: ZOOM,STATIC,ACTIVE,THREE_WORDS | Required | 
| timestamp | String | Defines the timestamp at which it was approved. | Required | 
| verifying_org | String | Organisation responsible for capturing and verifying liveness and the face. | Required | 
| resource_ids | []String | Reference to resource IDs for audit.\n\n\n\nResources provide details and media IDs for the images. | Optional (IDV only) | 
| check_ids | []String | Reference to check IDs for audit. | Optional (IDV only) | 
| user_activity_ids | []String | Reference to user activity records for audit purposes. | Optional (Digital ID only) | 
| selfie_attribute_id | []String | Reference to selfie image attribute.  Only included if the ‘selfie’ of the user is shared | Optional (Digital ID only) | 
| documents | []Object |  | Optional | 
| evidence_id | String | Unique ID identifying this evidence. | Required | 
| timestamp | String | Timestamp of when this document was added. | Required | 
| document_fields | Object | See document fields definition section | Required | 
| passed _checks | []Object | List of passed checks for this document | Required | 
| check | String | Enum: MANUAL_VISUAL_DOCUMENT_AUTHENTICITY, CHIP_DIGITAL_SIGNATURE, ISSUING_AUTHORITY, DOCUMENT_IN_DATE, FRAUD_DOCUMENTS_LIST, MANUAL_FACE_MATCH, AUTOMATED_FACE_MATCH, AUTOMATED_FACE_MATCH_HIGHER_THRESHOLD | Required | 
| verifying_org | String | Organisation responsible for capturing and verifying this document. | Required | 
| resource_ids | []String | Reference to resource IDs for audit.\n\n\n\nResources provide details and media IDs of the images. | Optional (IDV only) | 
| check_ids | []String | Reference to check IDs for audit. | Optional (IDV only) | 
| user_activity_ids | []String | Reference to user activity records for audit purposes. | Optional (Digital ID only) | 
| document_images_attribute_id | String | Reference to the shared attribute that contains document images for this document.  Only included if the images of this document are shared. | Optional (Digital ID only) | 
| electronic_records | []Object |  | Optional | 
| evidence_id | String | Unique ID identifying this evidence. | Required | 
| timestamp | String | Timestamp of when this electronic record was queried. | Required | 
| identity_details | Object | Identity details used in the query. | Required | 
| verifying_org | String | Organisation responsible for capturing and verifying this identity. | Required | 
| provider_org | String | Third party organisation providing the identity check. This could be a CRA or an organisation like CIFAS. | Optional | 
| resource_ids | []String | Reference to resource IDs for audit. | Optional (IDV only) | 
| check_ids | []String | Reference to check IDs for audit. | Optional (IDV only) | 
| user_activity_ids | []String | Reference to user activity records for audit purposes. | Optional (Digital ID only) | 
| authentication_report | Object | Provides the level of authentication reached according to the specified policy. | Optional (Digital ID only) | 
| report_id | String | Unique identifier for this report. | Required | 
| timestamp | String | Time at which this report was generated. RFC3339 UTC Timestamp e.g.: 2006-01-02T15:04:05Z | Required | 
| level | String | Level of authentication reached. Examples: "MEDIUM", "HIGH". | Required | 
| policy | String | Policy defines the rules used to assess \n\nthe level of authentication. Example: "GPG44". | Required | 
| proof | Object | Digital signature to prove that the report is generated by Yoti and to ensure it cannot be tampered with. | Required | 
{% /table %}