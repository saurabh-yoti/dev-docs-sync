---
type: page
title: Error responses
listed: true
slug: error-responses
description: 
index_title: Error responses
hidden: 
keywords: 
tags: 
---

## Overview

The identity verification process will attempt to exhaust all available options with a user before eventually terminating the verification process. This will happen as early as possible, if there's a strong evidence suggesting that the user will not achieve the relevant identity checking requirements for the requested scheme.

In the event that a combination scheme is requested (DBS & RTW), the identity verification flow will continue as long as one scheme could still be met.

Failures may include:

- 'Aborted' identity checks: Aborted identity checks are the result of a complete 'dead end' in the journey, meaning an identity profile will not be returned
- Requirements not met: Occurs when an identity profile _can_ be returned, however scheme compliance couldn't be met
- Requirements not met details: Additional information around the failure, explaining which checks were involved, and why they may have failed

{% badge type="info" text="Info" /%} When Right to Work is solely requested for a check. The result will only be `requirements_met`: `true`, or `ABORTED`. 

A DBS only scheme may return `requirements_met`: `false`, in the event the candidate identity was verified, but the current address could not be verified. In this scenario scheme compliance has not been reached, as DBS scheme compliance is made up of Identity & Verified Current Address.

For combination scenarios (DBS & RTW), an individual result is returned for each scheme. However it's important to note that:

- `ABORTED` will be returned when the identity verification fails for both DBS & RTW. In this case a reason code is shared for the failure
- Passing one scheme does not guarantee a pass in both. For example a user may complete the DBS scheme but not meet the RTW requirements if a UK or Irish Passport/Passport Card was not used in the journey. For such reason, RTW can return requirements not met and a reason code in the combo journey, even if the identity was verified, as opposed to fully aborting the check.
- It is entirely possible to receive an identity profile report but have a `requirements_met`: `false` for each scheme.

---

## Reason Codes

When a journey is aborted, either entirely or due to not reaching scheme compliance, a reason code will be returned to explain the failure.

These tables list the reason codes, a description of why they may occur, and the integration type in which they may be returned.

Since some failures can be triggered for multiple reasons, there is a priority for which overall reason code will be used. Details of all failed checks would be available in the failure details.

The priority is as follows:

1. `FRAUD_DETECTED` 
2. `UNABLE_TO_VALIDATE_DOCUMENT`
3. `FACE_MATCH_HIGHER_THRESHOLD_VERIFICATION_FAILED`
4. `FACE_MATCH_VERIFICATION_FAILED`
5. `MANDATORY_DOCUMENT_NOT_PROVIDED`

### Requirements not met info

{% table widths="0,0,30" %}
| Reason | Description | Digital ID | Embedded IDV | 
| ---- | ---- | ---- | ---- | 
| MANDATORY_DOCUMENT_NOT_PROVIDED* | The user does not have sufficient documents to reach the target level of identity verification.\n\n\n\n*This may be returned as an aborted reason, or a requirements not met reason. | ✅ | ✅ | 
| LEVEL_OF_ASSURANCE_NOT_SUFFICIENT* | Level of assurance for the scheme has not been reached. This is specific to combination routes and would occur if the identity has reached a Medium LoC, but not a High if requesting a Standard or Enhanced identity check.\n\n\n\n*This will only be returned as a requirements not met reason. | ✅ | ✅ | 
| UNABLE_TO_VERIFY_ADDRESS* | Identity profile has been generated but candidates address was not verified.\n\n\n\n*This will only be returned as a requirements not met reason. | ✅ | ✅ | 
{% /table %}

### Aborted

{% table widths="18,0,0" %}
| Reason | Description | Digital ID | Embedded IDV | 
| ---- | ---- | ---- | ---- | 
| MANDATORY_DOCUMENT_NOT_PROVIDED* | The user does not have sufficient documents to reach the target level of identity verification.\n\n\n\n*This may be returned as an aborted reason, or a requirements not met reason. | ✅ | ✅ | 
| FRAUD_DETECTED | Suspected fraud for the given identity therefore unable to reach the required identity profile. This should be reviewed. | ✅ | ✅ | 
| UNABLE_TO_VALIDATE_DOCUMENT | We have not been able to successfully validate a required document (for reasons other than suspected fraud, e.g. capture error) | ✅ | ✅ | 
| MISSING_LIVENESS | Returned if the session does not have a passed liveness check. | ❌ | ✅ | 
| IDENTITY_CHECK_FAILED | Additional checks on a user’s identity, required to meet the level of confidence, have not been successful. | ✅ | ✅ | 
| UNABLE_TO_COMPLETE_CHECKS | Required checks could not be completed. | ✅ | ✅ | 
| COULD_NOT_VERIFY_ADDRESS | Could occur if the address was not verified for any reason _after_ the applicant leaves the session. | ❌ | ✅ | 
| FACE_MATCH_VERIFICATION_FAILED | The face match check could not be performed. | ✅ | ✅ | 
| FACE_MATCH_HIGHER_THRESHOLD_\n\nVERIFICATION_FAILED | In some circumstances, a higher level of confidence in the face match is required, such as if the presented identity is at higher risk of identity fraud. This reason code is returned if such a higher threshold could not be met. | ✅ | ✅ | 
| ACTIVITY_HISTORY_SCORE_INSUFFICIENT | The profile has not reached the required activity history score for the specified scheme. | ❌ | ✅ | 
| IDENTITY_FRAUD_SCORE_INSUFFICIENT | The profile has not reached the identity fraud score for the specified scheme. | ❌ | ✅ | 
| IDENTITY_FRAUD_AND_ACTIVITY_\n\nHISTORY_SCORES_INSUFFICIENT | The profile has not reached both the identity fraud activity history scores for the specified scheme. | ❌ | ✅ | 
| MISSING_FRAUD_LIST_CHECK | This error can arise if a technical problem occurs while checking the identity against a fraud list. | ❌ | ✅ | 
| ABANDONED | Expired sessions will eventually be set to ABANDONED, there is approximately a two hour delay between this aborted reason appearing from expiry. | ❌ | ✅ | 
{% /table %}

### Requirements not met details

The requirements not met details structure is a list of objects which contains information to supplement the overall returned reason code. This surfaces information around the specific check, or multiple checks, which may have led to the failure.

The following fields are returned per each object in the structure:

- `failure_type`
- `document_type`
- `document_country_iso_code`
- `audit_id` 
- `details` 

{% badge type="info" text="Info" /%} Documents where an end user has select that they are unable to provide it, or do not have it, will not appear in the failure details, therefore it is possible to have an aborted session with no failure details (for example mandatory document not provide without any attempt by the user).

{% table widths="257" %}
| Failure Type | Associated Reason Code(s) | 
| ---- | ---- | 
| ID_DOCUMENT_EXTRACTION | MANDATORY_DOCUMENT_NOT_PROVIDED | 
| ID_DOCUMENT_AUTHENTICITY | UNABLE_TO_VALIDATE_DOCUMENT \n\n\n\nMISSING_FRAUD_LIST_CHECK\n\n\n\nFRAUD_DETECTED\n\n\n\nThe failure reason details will be populated with the check report recommendation. The list can be found [here](/identity-verification/document-report) | 
| ID_DOCUMENT_COUNTRY | MANDATORY_DOCUMENT_NOT_PROVIDED | 
| ID_DOCUMENT_FACE_MATCH | FACE_MATCH_VERIFICATION_FAILED\n\n\n\nFACE_MATCH_VERIFICATION_HIGHER_THRESHOLD_FAILED\n\n\n\nFRAUD_DETECTED\n\n\n\nThe failure reason details will be populated with the check report recommendation. The list can be found [here](/identity-verification/face-match-report) | 
| ID_DOCUMENT_ADDRESS_VERIFICATION | See ID Check table below | 
| IDENTITY_CHECK | See ID Check table below | 
| LIVENESS | MISSING_LIVENESS | 
| UNLINKED_DOCUMENT_EVIDENCE | MANDATORY_DOCUMENT_NOT_PROVIDED\n\n\n\nDocumentary evidence may be 'unlinked' if either the name, dob, or both do not match to additional document evidence in the requested scheme. | 
{% /table %}

### ID Check

This table lists the failure details codes that can be returned alongside the failure type of `IDENTITY_CHECK`.

{% table widths="300,181,193" %}
| Provider | Details | Reason code | Description | 
| ---- | ---- | ---- | ---- | 
| Third party identity | ERROR_WHEN_PERFORMING_CHECK | UNABLE_TO_COMPLETE_CHECKS | Something went wrong when calling the third party identity check server | 
| Third party identity | SUSPECTED_FRAUD | FRAUD_DETECTED | The third party identity check returns a suspected fraudulent check on the provided identity details | 
| Synectics | SYNECTICS_INDICATED_FRAUD | FRAUD_DETECTED | Synectics scored user 0 in identity fraud | 
| Synectics | FAILED_TO_REACH_REQUIRED_\n\n\n\nIDENTITY_FRAUD_SCORE_2 | IDENTITY_FRAUD_SCORE_\n\n\n\nINSUFFICIENT\n\n\n\nIDENTITY_FRAUD_AND_\n\n\n\nACTIVITY_HISTORY_SCORES_\n\n\n\nINSUFFICIENT | When attempting H2A, we failed to obtain an identity fraud score of at least 2 | 
| Synectics | FAILED_TO_REACH_REQUIRED_\n\n\n\nACTIVITY_HISTORY_SCORE_3 | IDENTITY_FRAUD_SCORE_\n\n\n\nINSUFFICIENT\n\n\n\nIDENTITY_FRAUD_AND_\n\n\n\nACTIVITY_HISTORY_SCORES_\n\n\n\nINSUFFICIENT | When attempting H2A, we failed to obtain an activity history score of at least 3 | 
| CRA | ERROR_WHEN_PERFORMING_CHECK | UNABLE_TO_COMPLETE_CHECKS | Something when wrong when calling the TransUnion server | 
| CRA | PEP_WARNING | IDENTITY_CHECK_FAILED | CRA check flagged the user as PEP or the check was not performed (i.e. the user's current address is claimed to be outside of the UK). If flagged as PEP, additional verification checks failed. | 
| CRA | DECEASED_WARNING | IDENTITY_CHECK_FAILED | CRA check flagged the user as deceased  or the check was not performed (i.e. the user's current address is claimed to be outside of the UK) | 
| CRA | UNABLE_TO_VERIFY_ADDRESS |  | For DBS basic: When the address could not be verified | 
| CRA | UNABLE_TO_VERIFY_ADDRESS | IDENTITY_CHECK_FAILED | For DBS standard/enhanced: When the address could not be verified | 
| CRA | UNABLE_TO_VERIFY_IDENTITY | IDENTITY_CHECK_FAILED | When the CRA check failed to find a match for the name or DOB | 
{% /table %}

### ID Doc Extraction

This table lists the failure details codes that can be returned alongside the failure type of `ID_DOCUMENT_EXTRACTION`.

{% table widths="" %}
| Details | Description | 
| ---- | ---- | 
| POOR_FOCUS | The image is too blurry to read the document details | 
| POOR_LIGHT | The provided document image was not taken in adequate light | 
| TOO_LIGHT | The provided document image has too much light or glare | 
| POOR_DOC | The image is too blurry to read the document details | 
| PARTIAL_SIDE_DOC | Parts of the document are missing from the image (i.e. missing side) | 
| PARTIAL_PHOTO | Parts of the document side are missing from the image | 
| DOCUMENT_COPY | The document has not been presented in its original form | 
| BLACK_AND_WHITE_IMAGE | The document image provided is not in colour | 
| NO_DOCUMENT | We could not detect a document in the captured image | 
| TEMPLATE | All parts of the document template could not be detected | 
| USER_DOES_NOT_HAVE_REQUESTED_DOCUMENTS | If the user did not provide all, or any of the documents required for the scheme, and there is no other failure reason | 
{% /table %}

---

## Examples

The below shows an example structure for the whole error object.

{% code %}
{% tab language="json" %}
"identity_profile": {
    "result": "ABORTED",
    "failure_reason": {
        "reason_code": "UNABLE_TO_VALIDATE_DOCUMENT",
        "requirements_not_met_details": [
            {
                "failure_type": "ID_DOCUMENT_FACE_MATCH",
                "document_type": "PASSPORT",
                "document_country_iso_code": "GBR",
                "audit_id": "",
                "details": "PARTIAL_PHOTO"
            },
            {
                "failure_type": "ID_DOCUMENT_AUTHENTICITY",
                "document_type": "PASSPORT",
                "document_country_iso_code": "GBR",
                "audit_id": "",
                "details": "OBJECT_OBSTRUCTION"
            }
        ]
    }
}
{% /tab %}
{% tab language="json" %}
"identity_profile": {
        "result": "ABORTED",
        "failure_reason": {
            "reason_code": "MISSING_LIVENESS",
            "requirements_not_met_details": [
                {
                    "failure_type": "LIVENESS",
                    "document_type": "",
                    "document_country_iso_code": "",
                    "audit_id": "",
                    "details": "USER_FAILED_LIVENESS"
                }
            ]
        }
    }
{% /tab %}
{% /code %}