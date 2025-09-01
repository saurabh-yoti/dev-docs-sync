---
type: page
title: Failure Scenarios
listed: true
slug: failure-scenarios
description: 
index_title: Failure Scenarios
hidden: 
keywords: 
tags: 
---

## Overview

The identity verification process will attempt to exhaust all available options with a user before eventually terminating the verification process. This will happen as early as possible, if there's a strong evidence suggesting that the user will not achieve the relevant identity checking requirements for the requested scheme.

In the event that multiple schemes are requested , the identity verification flow will continue as long as one scheme could still be met.

Failures may include:

- 'Aborted' identity checks: Aborted identity checks are the result of a complete 'dead end' in the journey, meaning an identity profile will not be returned
- Requirements not met: Occurs when an identity profile _can_ be returned, however scheme compliance couldn't be met
    - Requirements not met details: Additional information around the failure, explaining which checks were involved, and why they may have failed

When a journey is incomplete, either entirely  (aborted) or due to not reaching scheme compliance (requirements not met), a reason code will be returned to explain the failure.

These tables list the reason codes, a description of why they may occur, and the integration type in which they may be returned.

Since some failures can be triggered for multiple reasons, there is a priority for which overall reason code will be used. Details of all failed checks would be available in the failure details.

## Retrieving the Profile

The Identity Profile and any failures returned can be retrieved through the Yoti SDKs

{% code %}
{% tab language="javascript" title="Node.js" %}
IDVClient.getSession(sessionId)
  .then((session) => {
    const advancedIdentityProfile = session.getAdvancedIdentityProfile();

    const result = advancedIdentityProfile.getResult();

    const failureReason = advancedIdentityProfile.getFailureReason();

    const failureCode = failureReason.getReasonCode();

    const requirementsNotMetDetails =
      failureReason.getRequirementsNotMetDetails();

    // Check if there are any requirements not met details
    // This may be empty
    // There may be multiple details provided
    if (requirementsNotMetDetails.length === 0) {
      console.log("No requirements not met details found.");
    } else {
      const failureType = requirementsNotMetDetails[0].getFailureType();

      const documentType = requirementsNotMetDetails[0].getDocumentType();

      const countryCode = requirementsNotMetDetails[0].getDocumentCountryIsoCode();

      const auditId = requirementsNotMetDetails[0].getAuditId();

      const details = requirementsNotMetDetails[0].getDetails();
    }
  })
  .catch((error) => {
    console.log(error);
  });
{% /tab %}
{% tab language="csharp" title=".NET" %}
try
{
    var session = await idvClient.GetSession(sessionId);

    var advancedIdentityProfile = session.AdvancedIdentityProfile;

    var result = advancedIdentityProfile.Result;

    var failureReason = advancedIdentityProfile.FailureReason;

    var failureCode = failureReason.ReasonCode;

    var requirementsNotMetDetails = failureReason.RequirementsNotMetDetails;

    // Check if there are any requirements not met details
    // This may be empty
    // There may be multiple details provided
    if (requirementsNotMetDetails == null || requirementsNotMetDetails.Count == 0)
    {
        Console.WriteLine("No requirements not met details found.");
    }
    else
    {
        var failureType = requirementsNotMetDetails[0].FailureType;

        var documentType = requirementsNotMetDetails[0].DocumentType;

        var countryCode = requirementsNotMetDetails[0].DocumentCountryIsoCode;

        var auditId = requirementsNotMetDetails[0].AuditId;

        var details = requirementsNotMetDetails[0].Details;
    }
}
catch (Exception ex)
{
    Console.WriteLine(ex);
}
{% /tab %}
{% tab language="php" %}
// Coming soon
{% /tab %}
{% tab language="java" %}
try {
    Object session = idvClient.getSession(sessionId);

    Object advancedIdentityProfile = session.getAdvancedIdentityProfile();

    Object result = advancedIdentityProfile.getResult();

    Object failureReason = advancedIdentityProfile.getFailureReason();

    String failureCode = failureReason.getReasonCode();

    List<Object> requirementsNotMetDetails = 	failureReason.getRequirementsNotMetDetails();

    // Check if there are any requirements not met details
    // This may be empty
    // There may be multiple details provided
    if (requirementsNotMetDetails == null || requirementsNotMetDetails.isEmpty()) {
        System.out.println("No requirements not met details found.");
    } else {
        String failureType = requirementsNotMetDetails.get(0).getFailureType();

        String documentType = requirementsNotMetDetails.get(0).getDocumentType();

        String countryCode = requirementsNotMetDetails.get(0).getDocumentCountryIsoCode();

        String auditId = requirementsNotMetDetails.get(0).getAuditId();

        String details = requirementsNotMetDetails.get(0).getDetails();
    }
} catch (Exception e) {
    System.out.println(e);
}
{% /tab %}
{% tab language="go" %}
sessionResult, err := client.GetSession(sessionId)

    advancedIdentityProfile := sessionResult.GetAdvancedIdentityProfile()

    result := advancedIdentityProfile.GetResult()

    failureReason := advancedIdentityProfile.GetFailureReason()

    failureCode := failureReason.GetReasonCode()

    requirementsNotMetDetails := failureReason.GetRequirementsNotMetDetails()

    // Check if there are any requirements not met details
    // This may be empty
    // There may be multiple details provided
    if len(requirementsNotMetDetails) == 0 {
        fmt.Println("No requirements not met details found.")
    } else {
        failureType := requirementsNotMetDetails[0].GetFailureType()

        documentType := requirementsNotMetDetails[0].GetDocumentType()

        countryCode := requirementsNotMetDetails[0].GetDocumentCountryIsoCode()

        auditId := requirementsNotMetDetails[0].GetAuditId()

        details := requirementsNotMetDetails[0].GetDetails()
    }
{% /tab %}
{% /code %}

## Example Failure

{% code %}
{% tab language="json" title="Liveness Fail" %}
"advanced_identity_profile": {
        "result": "ABORTED",
        "failure_reason": {
            "reason_code": "MISSING_LIVENESS",
            "requirements_not_met_details": [
                {
                    "failure_type": "LIVENESS",
                    "details": "USER_FAILED_LIVENESS"
                }
            ]
        }
    }
{% /tab %}
{% tab language="json" title="Document Failure" %}
"advanced_identity_profile": {
        "result": "ABORTED",
        "failure_reason": {
            "reason_code": "UNABLE_TO_VALIDATE_DOCUMENT",
            "requirements_not_met_details": [
                {
                    "failure_type": "ID_DOCUMENT_AUTHENTICITY",
                    "document_type": "PASSPORT",
                    "document_country_iso_code": "GBR",
                    "audit_id": "2e8317cf-d8c6-428d-86e3-14cb4ea8cfc9",
                    "details": "PARTIAL_PHOTO"
                }
            ]
        }
    }
{% /tab %}
{% tab language="json" title="Document not Provided" %}
"advanced_identity_profile": {
        "result": "ABORTED",
        "failure_reason": {
            "reason_code": "MANDATORY_DOCUMENT_NOT_PROVIDED",
            "requirements_not_met_details": []
        }
    }
{% /tab %}
{% tab language="json" title="Fraud" %}
"advanced_identity_profile": {
        "result": "ABORTED",
        "failure_reason": {
            "reason_code": "FRAUD_DETECTED",
            "requirements_not_met_details": [
                {
                    "failure_type": "ID_DOCUMENT_FACE_MATCH",
                    "document_type": "PASSPORT",
                    "document_country_iso_code": "GBR",
                    "audit_id": "f175ba48-8ada-4776-98b9-a84bc703ffe9",
                    "details": "DIFFERENT_PERSON"
                }
            ]
        }
    }
{% /tab %}
{% /code %}

### Requirements not Met

{% table widths="" %}
| Code | Description | 
| ---- | ---- | 
| MANDATORY_DOCUMENT_NOT_PROVIDED | The user does not have sufficient documents to reach the target level of identity verification.\n\n\n\n*This may be returned as an aborted reason, or a requirements not met reason. | 
| LEVEL_OF_ASSURANCE_NOT_SUFFICIENT | Some documents were supplied, but scheme compliance could not be reached. | 
| UNABLE_TO_VERIFY_ADDRESS | Identity profile has been generated but candidates address was not verified. | 
{% /table %}

### Aborted

{% table widths="18,0" %}
| Reason | Description | 
| ---- | ---- | 
| MANDATORY_DOCUMENT_NOT_PROVIDED* | The user does not have sufficient documents to reach the target level of identity verification.\n\n\n\n*This may be returned as an aborted reason, or a requirements not met reason. | 
| FRAUD_DETECTED | Suspected fraud for the given identity therefore unable to reach the required identity profile. This should be reviewed. | 
| UNABLE_TO_VALIDATE_DOCUMENT | We have not been able to successfully validate a required document (for reasons other than suspected fraud, e.g. capture error) | 
| MISSING_LIVENESS | Returned if the session does not have a passed liveness check. | 
| IDENTITY_CHECK_FAILED | Additional checks on a user’s identity, required to meet the level of confidence, have not been successful. | 
| UNABLE_TO_COMPLETE_CHECKS | Required checks could not be completed. | 
| COULD_NOT_VERIFY_ADDRESS | Could occur if the address was not verified for any reason _after_ the applicant leaves the session. | 
| FACE_MATCH_VERIFICATION_FAILED | The face match check could not be performed. | 
| FACE_MATCH_HIGHER_THRESHOLD_\n\nVERIFICATION_FAILED | In some circumstances, a higher level of confidence in the face match is required, such as if the presented identity is at higher risk of identity fraud. This reason code is returned if such a higher threshold could not be met. | 
| IDENTITY_FRAUD_SCORE_INSUFFICIENT | The profile has not reached the identity fraud score for the specified scheme. | 
| ABANDONED | Expired sessions will eventually be set to ABANDONED, there is approximately a two hour delay between this aborted reason appearing from expiry. | 
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