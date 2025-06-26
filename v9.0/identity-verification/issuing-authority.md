---
type: page
title: Issuing Authority Checks
listed: true
slug: issuing-authority
description: 
index_title: Issuing Authority Checks
hidden: 
keywords: 
tags: 
---

This sub-check checks the supplied document information against an Issuing Authorities records. It is part of the document authenticity check

Our current list of Authority checkers:

- AAMVA - USA
- PAN DB - India
- DVS - Australia
- Citizencard - UK

Please note that some of these checks have additional charges, please contact us here if you have questions: [https://support.yoti.com/yotisupport/s/contactsupport](https://support.yoti.com/yotisupport/s/contactsupport)

### Required documents

The Issuing Authority check can only be run on certain documents. These are detailed below. If the check is requested and an unsupported document (eg document type - or restricted US state) is submitted by the user, we will not run this check and it will be omitted from the results

{% table %}
| Country | Documents | Details | 
| ---- | ---- | ---- | 
| USA | Driving Licence, State ID, Residence Permit | This must be opted in and comes at an additional cost | 
| India | PAN card | This is enabled by default and comes at no cost | 
| Australia | Passport, Driving Licence | This must be opted in and comes at an additional cost | 
| UK | Citizencard | This is enabled by default and comes at no cost | 
{% /table %}

#### AAMVA States

Some states do not participate or do not allow AAMVA calls and so we cannot perform the checks on these documents. See the below table for confirmation of each State

{% table %}
| State | Driving Licence supported | State ID supported | 
| ---- | ---- | ---- | 
| Alaska | No | No | 
| Alabama | Yes | No | 
| Arkansas | Yes | Yes | 
| Arizona | Yes | Yes | 
| California | No | No | 
| Colarado | Yes | Yes | 
| Connecticut | Yes | Yes | 
| District of Columbia | Yes | Yes | 
| Delaware | Yes | No | 
| Florida | Yes | Yes | 
| Georgia | Yes | No | 
| Hawaii | Yes | Yes | 
| Iowa | Yes | Yes | 
| Idaho | Yes | Yes | 
| Illinois | No | No | 
| Indiana | Yes | Yes | 
| Kansas | Yes | Yes | 
| Kentucky | Yes | Yes | 
| Louisiana | No | No | 
| Massachusetts | Yes | Yes | 
| Maryland | Yes | Yes | 
| Maine | Yes | Yes | 
| Michigan | Yes | Yes | 
| Minnesota | No | No | 
| Missouri | Yes | Yes | 
| Mississippi | Yes | Yes | 
| Montana | Yes | No | 
| North Carolina | Yes | Yes | 
| North Dakota | Yes | Yes | 
| Nebraska | Yes | Yes | 
| New Hampshire | No | No | 
| New Jersey | Yes | Yes | 
| New Mexico | Yes | Yes | 
| Nevada | Yes | No | 
| New York | No | No | 
| Ohio | Yes | No | 
| Oklahoma | No | No | 
| Oregon | Yes | Yes | 
| Pennsylvania | No | No | 
| Rhode Island | Yes | Yes | 
| South Carolina | Yes | Yes | 
| South Dakota | Yes | Yes | 
| Tennessee | Yes | Yes | 
| Texas | Yes | Yes | 
| Utah | No | No | 
| Virginia | Yes | Yes | 
| Vermont | Yes | Yes | 
| Washington | Yes | Yes | 
| Wisconsin | Yes | No | 
| West Virginia | Yes | Yes | 
| Wyoming | Yes | No | 
| State Dept. (Diplomatic) | No | No | 
{% /table %}

### Configuration

For some documents, this subcheck needs to be enabled in the Document Authenticity check

{% code %}
{% tab language="json" %}
{
  ...
  "requested_checks": [
    {
      "type": "ID_DOCUMENT_AUTHENTICITY",
      "config": {
        "manual_check": "FALLBACK",
        "issuing_authority_sub_check": {
          "requested": true,
          "filter": {
            "type": "ORTHOGONAL_RESTRICTIONS",
            "documents": [
              {
                "country_codes": [
                  "USA" //AUS
                ]
              }
            ]
          }
        }
      }
    }
  ]
}
{% /tab %}
{% tab language="php" %}
<? php
  
use Yoti\DocScan\Session\Create\SessionSpecificationBuilder;
use Yoti\DocScan\Session\Create\Check\RequestedDocumentAuthenticityCheckBuilder;
use Yoti\DocScan\Session\Create\Filters\Orthogonal\OrthogonalRestrictionsFilterBuilder;

		 $documentFilter = (new OrthogonalRestrictionsFilterBuilder())
   			 	 ->withWhitelistedCountries(['USA', 'AUS'])
   				 ->build();

     $documentAuthenticityCheck = (new RequestedDocumentAuthenticityCheckBuilder())
           ->withIssuingAuthoritySubCheckAndDocumentFilter($documentFilter)
           ->build();

	 	 $sessionSpec = (new SessionSpecificationBuilder())
  			   ->withRequestedCheck($documentAuthenticityCheck)
       ...
{% /tab %}
{% tab language="csharp" title=".NET" %}
using Yoti.Auth.DocScan.Session.Create;

var documentFilter = new OrthogonalRestrictionsFilterBuilder()
  	.WithIncludedCountries(['USA', 'AUS'])

var documentAuthenticityCheck = new RequestedDocumentAuthenticityCheckBuilder()
    .WithIssuingAuthoritySubCheck(documentFilter)
    .Build();

var sessionSpec = new SessionSpecificationBuilder()
    .WithRequestedCheck(documentAuthenticityCheck)
{% /tab %}
{% tab language="java" %}
OrthogonalRestrictionsFilter documentFilter = OrthogonalRestrictionsFilter.builder()
        .withWhitelistedCountries(Arrays.asList("USA", "AUS"))
  
  RequestedDocumentAuthenticityCheck documentAuthenticityCheck =
     RequestedDocumentAuthenticityCheck.builder()
       .withIssuingAuthoritySubCheck(documentFilter)
       .build();


  SessionSpec sessionSpec = SessionSpec.builder()
      .withRequestedCheck(documentAuthenticityCheck)
{% /tab %}
{% tab language="python" %}
doc_scan_client = DocScanClient(YOTI_CLIENT_SDK_ID, YOTI_KEY_FILE_PATH)

session_spec = (
    SessionSpecBuilder()
    .with_client_session_token_ttl(600)
    .with_resources_ttl(90000)
    .with_requested_check(
      {
      "type": "ID_DOCUMENT_AUTHENTICITY",
      "config": {
        "manual_check": "FALLBACK",
        "issuing_authority_sub_check": {
          "requested": true,
          "filter": {
            "type": "ORTHOGONAL_RESTRICTIONS",
            "documents": [
              {
                "country_codes": [
                  "USA" //AUS
                ]
              }
            ]
          }
        }
      }
    }
   )
{% /tab %}
{% /code %}

### Retrieving the results

The results of the subcheck will appear in the report breakdown of the Document Authenticity check

The address match will return but will not affect the subcheck result. If the primary fields match does not pass then this will fail the subcheck.

If the subcheck fails, the overall recommendation will be REJECT, with rejection reason: ISSUING_AUTHORITY_ INVALID

{% code %}
{% tab language="php" %}
<?php
$sessionResult = $docScanClient->getSession($sessionId);

// Returns a collection of checks
$checks = $sessionResult->getChecks();

foreach($checks as $check) {

    // Returns the type of check
    $type = $check->getType();

    // Returns the state of the check
    $state = $check->getState();

    // Returns the report for the check
    $report = $check->getReport();

    // Pull recommendation object
    $recommendation = $report->getRecommendation();
    // Obtain the recommendation value, either APPROVE, NOT_AVAILABLE or REJECT
    $recommendationValue = $recommendation->getValue();
    // If the check is not APPROVE, obtain the reason
    $reason = $recommendation->getReason();

    // Obtains a report breakdown - the Issuing Authority subcheck will be detailed here
    $breakdown = $report->getBreakdown();
}
{% /tab %}
{% tab language="csharp" title=".NET" %}
GetSessionResult sessionResult = docScanClient.GetSession(sessionId);

// Returns a collection of checks
List<CheckResponse> checks = sessionResult.Checks;

foreach (CheckResponse check in checks)
{
    // Returns the type of check
    string type = check.Type;

    // Returns the state of the check
    string state = check.State;

    // Returns the report for the check
    ReportResponse report = check.Report;

    // Pull recommendation object
    RecommendationResponse recommendation = report.Recommendation;
    // Obtain the recommendation value, either APPROVE, NOT_AVAILABLE or REJECT
    string recommendationValue = recommendation.Value;
    // If the check is not APPROVE, obtain the reason
    string reason = recommendation.Reason;

    // Obtains a report breakdown - the Issuing Authority subcheck will be detailed here
    List<BreakdownResponse> breakdown = report.Breakdown;
}
{% /tab %}
{% tab language="java" %}
GetSessionResult sessionResult = docScanClient.getSession(sessionId);

// Returns a collection of checks
List<? extends CheckResponse> checks = sessionResult.getChecks();

for (CheckResponse check: checks) {
    
    // Returns the type of check
    String type = check.getType();
    
    // Returns the state of the check
    String state = check.getState();

    // Returns the report for the check
    ReportResponse report = check.getReport();
   
    // Pull recommendation object
    RecommendationResponse recommendation = report.getRecommendation();
    // Obtain the recommendation value, either APPROVE, NOT_AVAILABLE or REJECT
    String recommendationValue = recommendation.getValue();
    // If the check is not APPROVE, obtain the reason
    String reason = recommendation.getReason();
    
    // Obtains a report breakdown - the Issuing Authority subcheck will be detailed here
    List<? extends BreakdownResponse> breakdown = report.getBreakdown();
}
{% /tab %}
{% /code %}

#### Example response

{% code %}
{% tab language="json" %}
{
  "checks": [
    {
      "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "type": "ID_DOCUMENT_AUTHENTICITY",
      "state": "DONE",
      "resources_used": [
        "3fa85f64-5717-4562-b3fc-2c963f66afa6"
      ],
      "generated_media": [
        {
          "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
          "type": "IMAGE"
        }
      ],
      "report": {
        "recommendation": {
          "value": "APPROVE"
        },
        "breakdown": [
          ...
          {
            "sub_check": "issuing_authority",
            "result": "PASS",
            "details": [
              {
                "name": "address_match",
                "value": "false"
              },
              {
                "name": "primary_fields_match",
                "value": "true"
              },
              {
                "name": "issuing_authority",
                "value": "AAMVA"
              },
              {
                "name": "verifying_org",
                "value": "AAMVA"
              }
            ],
            "process": "AUTOMATED"
          }
        ]
        ...
      },
      "created": "2024-01-01T00:00:00Z",
      "last_updated": "2024-01-01T00:00:00Z"
    }
  ]
}
{% /tab %}
{% /code %}