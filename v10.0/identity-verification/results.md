---
type: page
title: Retrieve results
listed: true
slug: results
description: 
index_title: Retrieve results
hidden: 
keywords: 
tags: 
---

Each session has a configured 'time to live' (TTL) which must be above 300 seconds (5 minutes). When a session is created, it remains active until it's time to live is reached.
For any active session, you can use the Yoti SDK to retrieve a report on the session (containing all the end-user's uploaded documents and associated metadata).

{% html %}
<div class="alert-know">
    <div class="alert-title" id="know">
        Recommendation
    </div>
    <div class="alert-text">
Yoti strongly recommends you use notifications for each session status.    </div>
    <div class="alert-links"> 
       <a href="https://developers.yoti.com/identity-verification/notifications">Notifications</a>
    </div>
</div>
{% /html %}

This sections explains how to:

- Retrieve the results of the session
- Display checks and results associated to an ID Document in a session

The structure of the full response is shown below:

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1595537494/30910/uyfa3ajl82gqkoeklkzk.jpg" caption="Results hierarchy" mode="full" height="2695" width="1000" %}
{% /image %}

The report includes a  recommendation for each check. Please read this section and then head over to [auto$](/identity-verification/understanding-the-report) for more information.

---

## Result of the session

Session retrieval requires a session ID, this is generated from the create a session endpoint.  Below is a basic example of what retrieving a session looks like:

{% code %}
{% tab language="javascript" title="Node.js" %}
// Returns a session result
idvClient.getSession(sessionId).then(session => {
    // Returns the session state
    const state = session.getState();
    
    // Returns session resources
    const resources = session.getResources();

    // Returns all checks on the session
    const checks = session.getChecks();

    // Return specific check types
    const authenticityChecks = session.getAuthenticityChecks();
    const faceMatchChecks = session.getFaceMatchChecks();
    const textDataChecks = session.getTextDataChecks();
    const livenessChecks = session.getLivenessChecks();
    const watchlistScreeningChecks = session.getWatchlistScreeningChecks();
    const watchlistAdvancedCaChecks = session.getWatchlistAdvancedCaChecks();
  
    // Returns biometric consent timestamp
    const biometricConsent = session.getBiometricConsentTimestamp();
    
}).catch(error => {
    // handle error
})
{% /tab %}
{% tab language="java" %}
// Returns a session result
GetSessionResult sessionResult = docScanClient.getSession(sessionId);

// Returns the session state
String state = sessionResult.getState();

// Returns session resources
ResourceContainer resources = sessionResult.getResources();

// Returns all checks on the session
List<? extends CheckResponse> checks = sessionResult.getChecks();

// Return specific check types
List<AuthenticityCheckResponse> authenticityChecks = sessionResult.getAuthenticityChecks();
List<FaceMatchCheckResponse> faceMatchChecks = sessionResult.getFaceMatchChecks();
List<TextDataCheckResponse> textDataChecks = sessionResult.getTextDataChecks();
List<LivenessCheckResponse> livenessChecks = sessionResult.getLivenessChecks();
List<WatchlistScreeningCheckResponse> watchlistScreeningChecks = getSessionResult.getWatchlistScreeningChecks();
List<WatchlistAdvancedCaCheckResponse> watchlistAdvancedCaChecks = getSessionResult.getWatchlistAdvancedCaChecks();

// Returns biometric consent timestamp
String biometricConsent = sessionResult.getBiometricConsentTimestamp();
{% /tab %}
{% tab language="php" %}
<?php
// Returns a session result
$sessionResult = $docScanClient->getSession($sessionId);

// Returns the session state
$state = $sessionResult->getState();

// Returns session resources
$resources = $sessionResult->getResources();

// Returns all checks on the session
$checks = $sessionResult->getChecks();

// Return specific check types
$authenticityChecks = $sessionResult->getAuthenticityChecks();
$faceMatchChecks = $sessionResult->getFaceMatchChecks();
$textDataChecks = $sessionResult->getTextDataChecks();
$livenessChecks = $sessionResult->getLivenessChecks();
$watchlistScreeningChecks = $sessionResult->getWatchlistScreeningChecks();
$watchlistAdvancedCaChecks = $sessionResult->getWatchlistAdvancedCaChecks();
  

// Returns biometric consent timestamp
$biometricConsent = $sessionResult->getBiometricConsentTimestamp();
{% /tab %}
{% tab language="python" %}
# Returns a session result
session_result = doc_scan_client.get_session(session_id)

# Returns the session state
state = session_result.state

# Returns session resources
resources = session_result.resources

# Returns all checks on the session
checks = session_result.checks

# Return specific check types
authenticity_checks = session_result.authenticity_checks
face_match_checks = session_result.face_match_checks
text_data_checks = session_result.text_data_checks
liveness_checks = session_result.liveness_checks

# Returns biometric consent timestamp
biometric_consent = session_result.biometric_consent_timestamp
{% /tab %}
{% tab language="csharp" %}
// Returns a session result
GetSessionResult sessionResult = docScanClient.GetSession(sessionId);

// Returns the session state
string state = sessionResult.State;

// Returns session resources
ResourceContainer resources = sessionResult.Resources;

// Returns all checks on the session
List<CheckResponse> checks = sessionResult.Checks;

// Return specific check types
List<AuthenticityCheckResponse> authenticityChecks = sessionResult.GetAuthenticityChecks();
List<FaceMatchCheckResponse> faceMatchChecks = sessionResult.GetFaceMatchChecks();
List<TextDataCheckResponse> textDataChecks = sessionResult.GetTextDataChecks();
List<LivenessCheckResponse> livenessChecks = sessionResult.GetLivenessChecks();

// Returns biometric consent timestamp
DateTime biometricConsent = sessionResult.BiometricConsentTimestamp();
{% /tab %}
{% tab language="json" %}
{
  "session_id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "client_session_token_ttl": 599,
  "user_tracking_id": "string",
  "biometric_consent": "2023-04-13T10:58:32.627Z",
  "state": "COMPLETED",
  "client_session_token": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "resources": {
    "id_documents": [
      {
        "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
        "source": {
          "type": "END_USER"
        },
        "document_type": "PASSPORT",
        "issuing_country": "string",
        "pages": [
          {
            "capture_method": "CAMERA",
            "media": {
              "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
              "type": "IMAGE",
              "created": "2021-06-11T11:39:24Z",
              "last_updated": "2021-06-11T11:39:24Z"
            },
            "frames": [
              {
                "media": {
                  "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
                  "type": "IMAGE",
                  "created": "2021-06-11T11:39:24Z",
                  "last_updated": "2021-06-11T11:39:24Z"
                }
              }
            ]
          }
        ],
        "document_fields": {
          "media": {
            "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "type": "JSON",
            "created": "2021-06-11T11:39:24Z",
            "last_updated": "2021-06-11T11:39:24Z"
          }
        },
        "document_id_photo": {
          "media": {
            "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "type": "IMAGE",
            "created": "2021-06-11T11:39:24Z",
            "last_updated": "2021-06-11T11:39:24Z"
          }
        },
        "created_at": "2021-06-11T11:39:24Z",
        "last_updated": "2021-06-11T11:39:24Z",
        "tasks": [
          {
            "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "state": "DONE",
            "created": "2021-06-11T11:39:24Z",
            "last_updated": "2021-06-11T11:39:24Z",
            "generated_media": [
              {
                "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
                "type": "IMAGE"
              }
            ],
            "generated_checks": [
              {
                "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
                "type": "ID_DOCUMENT_TEXT_DATA_CHECK"
              }
            ],
            "type": "ID_DOCUMENT_TEXT_DATA_EXTRACTION"
          }
        ]
      }
    ],
    "liveness_capture": [
      {
        "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
        "source": {
          "type": "END_USER"
        },
        "liveness_type": "STATIC",
        "facemap": {
          "media": {
            "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "type": "IMAGE",
            "created": "2021-06-11T11:39:24Z",
            "last_updated": "2021-06-11T11:39:24Z"
          }
        },
        "frames": [
          {
            "media": {
              "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
              "type": "IMAGE",
              "created": "2021-06-11T11:39:24Z",
              "last_updated": "2021-06-11T11:39:24Z"
            }
          }
        ],
        "created_at": "2021-06-11T11:39:24Z",
        "last_updated": "2021-06-11T11:39:24Z",
        "tasks": [],
        "image": {
          "media": {
            "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "type": "IMAGE",
            "created": "2021-06-11T11:39:24Z",
            "last_updated": "2021-06-11T11:39:24Z"
          }
        }
      }
    ],
    "face_capture": [
      {
        "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
        "source": {
          "type": "END_USER"
        },
        "image": {
          "media": {
            "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "type": "IMAGE",
            "created": "2021-06-11T11:39:24Z",
            "last_updated": "2021-06-11T11:39:24Z"
          }
        },
        "created_at": "2021-06-11T11:39:24Z",
        "last_updated": "2021-06-11T11:39:24Z",
        "tasks": []
      }
    ]
  },
  "checks": [
    {
      "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "type": "ID_DOCUMENT_AUTHENTICITY",
      "state": "CREATED",
      "resources_used": [
        "3fa85f64-5717-4562-b3fc-2c963f66afa6"
      ],
      "generated_media": [
        {
          "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
          "type": "JSON"
        }
      ],
      "report": {
        "recommendation": {
          "value": "APPROVE"
        },
        "breakdown": [
          {
            "sub_check": "string",
            "result": "PASS",
            "details": []
          }
        ]
      },
      "created": "2021-06-11T11:39:24Z",
      "last_updated": "2021-06-11T11:39:24Z"
    },
    {
      "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "type": "ID_DOCUMENT_TEXT_DATA_CHECK",
      "state": "CREATED",
      "resources_used": [
        "3fa85f64-5717-4562-b3fc-2c963f66afa6"
      ],
      "generated_media": [
        {
          "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
          "type": "JSON"
        }
      ],
      "report": {
        "recommendation": {
          "value": "APPROVE"
        },
        "breakdown": [
          {
            "sub_check": "string",
            "result": "PASS",
            "details": []
          }
        ]
      },
      "created": "2021-06-11T11:39:24Z",
      "last_updated": "2021-06-11T11:39:24Z"
    },
    {
      "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "type": "LIVENESS",
      "state": "CREATED",
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
          {
            "sub_check": "string",
            "result": "PASS",
            "details": []
          }
        ]
      },
      "created": "2021-06-11T11:39:24Z",
      "last_updated": "2021-06-11T11:39:24Z"
    },
    {
      "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "type": "ID_DOCUMENT_FACE_MATCH",
      "state": "CREATED",
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
          {
            "sub_check": "string",
            "result": "PASS",
            "details": []
          }
        ]
      },
      "created": "2021-06-11T11:39:24Z",
      "last_updated": "2021-06-11T11:39:24Z"
    },
    {
      "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "type": "WATCHLIST_SCREENING",
      "state": "CREATED",
      "resources_used": [
        "3fa85f64-5717-4562-b3fc-2c963f66afa6"
      ],
      "generated_media": [
        {
          "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
          "type": "JSON"
        }
      ],
      "generated_profile": {
        "media": {
          "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
          "type": "JSON",
          "created": "2021-06-11T11:39:24Z",
          "last_updated": "2021-06-11T11:39:24Z"
        }
      },
      "report": {
        "recommendation": {
          "value": "APPROVE"
        },
        "breakdown": [
          {
            "sub_check": "string",
            "result": "PASS",
            "details": []
          }
        ],
        "watchlist_summary": {
          "total_hits": 0,
          "search_config": {
            "categories": [
              "ADVERSE-MEDIA"
            ]
          },
          "raw_results": {
            "media": {
              "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
              "type": "JSON",
              "created": "2021-06-11T11:39:24Z",
              "last_updated": "2021-06-11T11:39:24Z"
            }
          },
          "associated_country_codes": [
            "GBR",
            "USA"
          ]
        }
      },
      "created": "2021-06-11T11:39:24Z",
      "last_updated": "2021-06-11T11:39:24Z"
    },
    {
      "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "type": "WATCHLIST_ADVANCED_CA",
      "state": "CREATED",
      "resources_used": [
        "3fa85f64-5717-4562-b3fc-2c963f66afa6"
      ],
      "generated_media": [
        {
          "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
          "type": "JSON"
        }
      ],
      "generated_profile": {
        "media": {
          "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
          "type": "JSON",
          "created": "2021-06-11T11:39:24Z",
          "last_updated": "2021-06-11T11:39:24Z"
        }
      },
      "report": {
        "recommendation": {
          "value": "APPROVE"
        },
        "breakdown": [
          {
            "sub_check": "string",
            "result": "PASS",
            "details": []
          }
        ],
        "watchlist_summary": {
          "total_hits": 0,
          "search_config": {
            "categories": [
              "ADVERSE-MEDIA"
            ]
          },
          "raw_results": {
            "media": {
              "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
              "type": "JSON",
              "created": "2021-06-11T11:39:24Z",
              "last_updated": "2021-06-11T11:39:24Z"
            }
          },
          "associated_country_codes": [
            "GBR",
            "USA"
          ]
        }
      },
      "created": "2021-06-11T11:39:24Z",
      "last_updated": "2021-06-11T11:39:24Z"
    }
  ]
}
{% /tab %}
{% /code %}

The following are present in every session result:

{% table widths="" %}
| Value | Description | 
| ---- | ---- | 
| State | The current state of the session. It provides the overall state of the session. \n\nYou can search through session results prior to this being completed, but some checks may not have been processed yet. | 
| Resources | A container of all ID documents and liveness captures for this session. A new resource is created on each attempt at a document or liveness submission. | 
| Checks | A container of all checks performed for this session | 
{% /table %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Jump to..
    </div>
    <div class="alert-text">
       Refresh on the session ID creation or get a deeper dive on the states, resources and checks go to Understanding the report.
    </div>
    <div class="alert-links"> 
              <a href="https://developers.yoti.com/identity-verification/integration-guide">Integration guide</a>

        <a href="https://developers.yoti.com/identity-verification/understanding-the-report">Understanding the report</a>
        
   </div>
</div>
{% /html %}

---

## Results of checks

A basic example of how to get the check type, check recommendation value and reason is shown below. 

A recommendation reason will only be provided if the value isn't 'APPROVE'. The recommended approach for processing a session is to ensure that each check value is APPROVE.

We will use the **check container** to iterate through all of the checks that have been completed as part of the session. The checks object will only contain information once the user has completed all events (apart from Liveness) inside of the iFrame. 

### Liveness

The liveness response is available immediately. The user may have multiple attempts of liveness and It's possible for some of these attempts to be rejected.

{% code %}
{% tab language="javascript" title="Node.js" %}
idvClient.getSession(sessionId).then(session => {  
  	// Returns a collection of liveness checks
  	const livenessChecks = session.getLivenessChecks();
    
    livenessChecks.map(check => {
        // Returns the id of the check
        const id = check.getId();

        // Returns the state of the check
        const state = check.getState();

        // Returns an array of resources used in the check
        const resourcesUsed = check.getResourcesUsed();

        // Returns the report for the check
        const report = check.getReport();
    
        // Returns the recommendation value
        const recommendation = report.getRecommendation().getValue();

        // Returns the report breakdown including sub-checks
        const breakdown = report.getBreakdown();
      
      	breakdown.forEach(function(breakdown) {
          // Returns the sub-check
          const subCheck = breakdown.getSubCheck();
          
          // Returns the sub-check result
          const subCheckResult = breakdown.getResult();
        });
    })
}).catch(error => {
    // handle error
})
{% /tab %}
{% tab language="java" %}
GetSessionResult sessionResult = docScanClient.getSession(sessionId);

// Returns a collection of liveness checks
List<? extends CheckResponse> livenessChecks = sessionResult.getLivenessChecks();

for (CheckResponse check: livenessChecks) {
    // Returns the id of the check
    String id = check.getId();
    
    // Returns the state of the check
    String state = check.getState();
    
    // Returns a list of resources used in the check
    List<String> resourcesUsed = check.getResourcesUsed();

    // Returns the report for the check
    ReportResponse report = check.getReport();

    // Returns the recommendation value, either APPROVE, NOT_AVAILABLE or REJECT
    String recommendationValue = report.getRecommendation().getValue();

    // Returns the report breakdown including sub-checks
    List<? extends BreakdownResponse> breakdown = report.getBreakdown();
  
  	for (BreakdownResponse breakdown: breakdown) {
        // Returns the sub-check
        String subCheck = breakdown.getSubCheck();

        // Returns the sub-check result
        String subCheckResult = breakdown.getResult();
    }
}
{% /tab %}
{% tab language="php" %}
<?php
$sessionResult = $docScanClient->getSession($sessionId);

// Returns a collection of liveness checks
$livenessChecks = $sessionResult->getLivenessChecks();

foreach($checks as $check) {
    // Returns the id of the check
    $id = $check->getId();

    // Returns the state of the check
    $state = $check->getState();

    // Returns an array of resources used in the check
    $resourcesUsed = $check->getResourcesUsed();

    // Returns the report for the check
    $report = $check->getReport();

    // Returns the recommendation value, either APPROVE, NOT_AVAILABLE or REJECT
    $recommendationValue = $report->getRecommendation()->getValue();

    // Returns the report breakdown including sub-checks
    $breakdown = $report->getBreakdown();
  
  	foreach($breakdown as $breakdown) {
        // Returns the sub-check
        $subCheck = $breakdown->getSubCheck();

        // Returns the sub-check result
        $subCheckResult = $breakdown->getResult();
    }
}
{% /tab %}
{% tab language="python" %}
session_result = doc_scan_client.get_session(session_id)

# Returns a collection of checks
livenesschecks = session_result.liveness_checks

for check in checks:
    # Returns the id of the check
    check_id = check.id

    # Returns the state of the check
    check_state = check.state

    # Returns an array of resources used in this check
    resources_used = check.resources_used

    # Returns tje report for the check
    report = check.report

    # Returns the recommendation value, either APPROVE, NOT_AVAILABLE or REJECT
    recommendation_value = report.recommendation.value

    # Returns the report breakdown including sub-checks
    breakdown = report.breakdown
    
    for breakdown in breakdown:
      # Returns the sub-check
      subCheck = breakdown.sub_check

      # Returns the sub-check result
      subCheckResult = breakdown.result
{% /tab %}
{% tab language="csharp" %}
GetSessionResult sessionResult = docScanClient.GetSession(sessionId);

// Returns a collection of checks
List<CheckResponse> livenessChecks = sessionResult.GetLivenessChecks();

foreach (CheckResponse check in livenessChecks)
{
    // Returns the id of the check
    string id = check.Id;

    // Returns the state of the check
    string state = check.State;

    // Returns an array of resources used in this check
    List<String> resourcesUsed = check.ResourcesUsed;

    // Returns the report for the check
    ReportResponse report = check.Report;

    // Returns the recommendation value, either APPROVE, NOT_AVAILABLE or REJECT
    string recommendationValue = report.Recommendation.Value;

    // Returns the report breakdown including sub-checks
    List<BreakdownResponse> breakdown = report.Breakdown;
  
    foreach (BreakdownResponse breakdown in breakdown)
    {
        // Returns the sub-check
        string subCheck = breakdown.SubCheck;

        // Returns the sub-check result
        string subCheckResult = breakdown.Result;
    }
}
{% /tab %}
{% tab language="json" %}
{
  "checks": [
    {
      "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "type": "LIVENESS",
      "state": "CREATED",
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
          {
            "sub_check": "string",
            "result": "PASS",
            "details": []
          }
        ]
      },
      "created": "2021-06-11T11:39:24Z",
      "last_updated": "2021-06-11T11:39:24Z"
    }
  ]
}
{% /tab %}
{% /code %}

### Multiple document resources

Each check returns a list of 'resources used', identifying the ID document, face capture, or supplementary document resources used for that check. These are mapped to the resources container.

A single ID Document or Face capture can have multiple resources. This is because a new resource may be created for each attempt to submit an ID document (for example, if Yoti's in-browser feedback requests another capture or multiple liveness attempts).

{% code %}
{% tab language="javascript" title="Node.js" %}
idvClient.getSession(sessionId).then(session => {
    // Returns a collection of checks
    const checks = session.getChecks();
    
    checks.map(check => {

        // Returns the type of check
        const type = check.getType();

        // Returns the state of the check
        const state = check.getState();

        // Returns an array of resources used in this check
        const resourcesUsed = check.getResourcesUsed();
      
        // Returns a list of generated media for this check
        // For THIRD_PARTY_CHECK this will be the fields used to perform the check
        const generatedMedia = check.getGeneratedMedia();

        // Returns the report for the check
        const report = check.getReport();
    
        // Pull recommendation object
        const recommendation = report.getRecommendation();
        // Obtain the recommendation value, either APPROVE, NOT_AVAILABLE or REJECT
        const recommendationValue = recommendation.getValue();
        // If the check is not APPROVE, obtain the reason
        const reason = recommendation.getReason();

        // Obtains a report breakdown
        const breakdown = report.getBreakdown();
    })
}).catch(error => {
    // handle error
})
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
    
    // Returns a list of resources used in this check
    List<String> resourcesUsed = check.getResourcesUsed();
  
    // Returns a list of generated media for this check
    // For THIRD_PARTY_CHECK this will be the fields used to perform the check
    List<? extends GeneratedMedia> generatedMedia = check.getGeneratedMedia();
    
    // Returns the report for the check
    ReportResponse report = check.getReport();
   
    // Pull recommendation object
    RecommendationResponse recommendation = report.getRecommendation();
    // Obtain the recommendation value, either APPROVE, NOT_AVAILABLE or REJECT
    String recommendationValue = recommendation.getValue();
    // If the check is not APPROVE, obtain the reason
    String reason = recommendation.getReason();
    
    // Obtains a report breakdown
    List<? extends BreakdownResponse> breakdown = report.getBreakdown();
}
{% /tab %}
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

    // Returns an array of resources used in this check
    $resourcesUsed = $check->getResourcesUsed();

    // Returns the report for the check
    $report = $check->getReport();

    // Pull recommendation object
    $recommendation = $report->getRecommendation();
    // Obtain the recommendation value, either APPROVE, NOT_AVAILABLE or REJECT
    $recommendationValue = $recommendation->getValue();
    // If the check is not APPROVE, obtain the reason
    $reason = $recommendation->getReason();

    // Obtains a report breakdown
    $breakdown = $report->getBreakdown();
}
{% /tab %}
{% tab language="python" %}
session_result = doc_scan_client.get_session(session_id)

# Returns a collection of checks
checks = session_result.checks

for check in checks:
    
    # Returns the type of check
    check_type = check.type

    # Returns the state of the check
    check_state = check.state

    # Returns an array of resources used in this check
    resources_used = check.resources_used

    # Returns tje report for the check
    report = check.report

    # Pull recommendation object
    recommendation = report.recommendation
    # Obtain the recommendation value, either APPROVE, NOT_AVAILABLE or REJECT
    recommendation_value = recommendation.value
    # If the check is not APPROVE, obtain the reason
    reason = recommendation.reason

    # Obtains a report breakdown
    breakdown = report.breakdown
{% /tab %}
{% tab language="csharp" %}
GetSessionResult sessionResult = docScanClient.GetSession(sessionId);

// Returns a collection of checks
List<CheckResponse> checks = sessionResult.Checks;

foreach (CheckResponse check in checks)
{
    // Returns the type of check
    string type = check.Type;

    // Returns the state of the check
    string state = check.State;

    // Returns an array of resources used in this check
    List<String> resourcesUsed = check.ResourcesUsed;

    // Returns the report for the check
    ReportResponse report = check.Report;

    // Pull recommendation object
    RecommendationResponse recommendation = report.Recommendation;
    // Obtain the recommendation value, either APPROVE, NOT_AVAILABLE or REJECT
    string recommendationValue = recommendation.Value;
    // If the check is not APPROVE, obtain the reason
    string reason = recommendation.Reason;

    // Obtains a report breakdown
    List<BreakdownResponse> breakdown = report.Breakdown;
}
{% /tab %}
{% tab language="json" %}
{
  "checks": [
    {
      "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "type": "ID_DOCUMENT_AUTHENTICITY",
      "state": "CREATED",
      "resources_used": [
        "3fa85f64-5717-4562-b3fc-2c963f66afa6",
        "42364f8f-0649-44fa-a873-ea5267e9c61b"
      ],
      "generated_media": [
        {
          "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
          "type": "JSON"
        },
        {
          "id": "42364f8f-0649-44fa-a873-ea5267e9c61b",
          "type": "JSON"
        }
      ],
      "report": {
        "recommendation": {
          "value": "APPROVE"
        },
        "breakdown": [
          {
            "sub_check": "string",
            "result": "PASS",
            "details": []
          }
        ]
      },
      "created": "2021-06-11T11:39:24Z",
      "last_updated": "2021-06-11T11:39:24Z"
    }
  ]
}
{% /tab %}
{% /code %}

---

## AML

In addition to the normal report, watchlist checks will also return a WatchlistSummary object:

{% code %}
{% tab language="javascript" title="Node.js" %}
const watchlistScreeningChecks = session.getWatchlistScreeningChecks();
const report = watchlistScreeningChecks[0].getReport();

// Watchlist Screening summary
const watchlistSummary = report.getWatchlistSummary();
const associatedCountryCodes = watchlistSummary.getAssociatedCountryCodes();
const rawResults = watchlistSummary.getRawResults();
const totalHits = watchlistSummary.getTotalHits();

// Search config used
const searchConfig = watchlistSummary.getSearchConfig();
const categories = searchConfig.getCategories();

//Adcvanced checks
const watchlistAdvancedCaChecks = session.getWatchlistAdvancedCaChecks();
const report = watchlistScreeningChecks[0].getReport();
        
// Watchlist summary
const watchlistSummary = report.getWatchlistSummary();
const associatedCountryCodes = watchlistSummary.getAssociatedCountryCodes();
const rawResults = watchlistSummary.getRawResults();
const totalHits = watchlistSummary.getTotalHits();
        
// Search config
const searchConfig = watchlistSummary.getSearchConfig();
const removeDeceased = searchConfig.isRemoveDeceased();
const shareUrl = searchConfig.isShareUrl();
const sources = searchConfig.getSources();
const matchingStrategy = searchConfig.getMatchingStrategy();
{% /tab %}
{% tab language="java" %}
// Click to edit 
List<WatchlistScreeningCheckResponse> watchlistScreeningChecks = getSessionResult.getWatchlistScreeningChecks();
WatchlistScreeningCheckResponse watchlistScreeningCheckResponse = watchlistScreeningChecks.get(0);
WatchlistScreeningReportResponse report = watchlistScreeningCheckResponse.getReport();

// Watchlist Screening summary
WatchlistScreeningSummaryResponse watchlistSummary = report.getWatchlistSummary();
List<String> associatedCountryCodes = watchlistSummary.getAssociatedCountryCodes();
RawResultsResponse rawResults = watchlistSummary.getRawResults();
int totalHits = watchlistSummary.getTotalHits();

// Search config used
WatchlistScreeningSearchConfigResponse searchConfig = watchlistSummary.getSearchConfig();
List<String> categories = searchConfig.getCategories();



//Adcvanced checks
List<WatchlistAdvancedCaCheckResponse> watchlistAdvancedCaChecks = getSessionResult.getWatchlistAdvancedCaChecks();
        WatchlistAdvancedCaCheckResponse watchlistAdvancedCaCheckResponse = watchlistAdvancedCaChecks.get(0);
        WatchlistAdvancedCaReportResponse report = watchlistAdvancedCaCheckResponse.getReport();
        // Watchlist summary
        WatchlistAdvancedCaSummaryResponse watchlistSummary = report.getWatchlistSummary();
        List<String> associatedCountryCodes = watchlistSummary.getAssociatedCountryCodes();
        RawResultsResponse rawResults = watchlistSummary.getRawResults();
        int totalHits = watchlistSummary.getTotalHits();
        // Search config
        WatchlistAdvancedCaSearchConfigResponse searchConfig = watchlistSummary.getSearchConfig();
        boolean removeDeceased = searchConfig.isRemoveDeceased();
        boolean shareUrl = searchConfig.isShareUrl();
        CaSourcesResponse sources = searchConfig.getSources();
        CaMatchingStrategyResponse matchingStrategy = searchConfig.getMatchingStrategy();
        if (searchConfig instanceof CustomAccountWatchlistCaSearchConfigResponse) {
            CustomAccountWatchlistCaSearchConfigResponse customConfigResponse = (CustomAccountWatchlistCaSearchConfigResponse) searchConfig;
            String apiKey = customConfigResponse.getApiKey();
            String clientRef = customConfigResponse.getClientRef();
            Map<String, String> tags = customConfigResponse.getTags();
            boolean monitoring = customConfigResponse.isMonitoring();
        }de
{% /tab %}
{% tab language="php" %}
$watchlistScreeningChecks = $session->getWatchlistScreeningChecks();
$report = $watchlistScreeningChecks[0]->getReport();

// Watchlist Screening summary
$watchlistSummary = $report->getWatchlistSummary();
$associatedCountryCodes = $watchlistSummary->getAssociatedCountryCodes();
$rawResults = $watchlistSummary->getRawResults();
$totalHits = $watchlistSummary->getTotalHits();

// Search config used
$searchConfig = $watchlistSummary->getSearchConfig();
$categories = $searchConfig->getCategories();

//Adcvanced checks
$watchlistAdvancedCaChecks = $session->getWatchlistAdvancedCaChecks();
$report = $watchlistScreeningChecks[0]->getReport();

// Watchlist Screening summary
$watchlistSummary = $report->getWatchlistSummary();
$associatedCountryCodes = $watchlistSummary->getAssociatedCountryCodes();
$rawResults = $watchlistSummary->getRawResults();
$totalHits = $watchlistSummary->getTotalHits();

// Search config used
$searchConfig = $watchlistSummary->getSearchConfig();
$removeDeceased = $searchConfig->isRemoveDeceased();
$shareUrl = $searchConfig->isShareUrl();
$sources = $searchConfig->getSources();
$matchingStrategy = $searchConfig->getMatchingStrategy();
{% /tab %}
{% tab language="python" %}
//COMING SOON
{% /tab %}
{% tab language="csharp" %}
GetSessionResult getSessionResult = docScanClient.GetSession(sessionId);

            List<WatchlistScreeningCheckResponse> watchlistScreeningChecks = getSessionResult.GetWatchlistScreeningChecks();
            ReportResponse reportResponse = watchlistScreeningChecks[0].Report;

            ReportResponseWithSummary reportResponseWithSummary = (ReportResponseWithSummary)reportResponse;
            string recommendationValue = reportResponseWithSummary.Recommendation.Value;
            string recommendationReason = reportResponseWithSummary.Recommendation.Reason;
            List<BreakdownResponse> breakdowns = reportResponseWithSummary.Breakdown;
{% /tab %}
{% tab language="json" %}
{
  "checks": [
    {
      "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "type": "WATCHLIST_SCREENING",
      "state": "CREATED",
      "resources_used": [
        "3fa85f64-5717-4562-b3fc-2c963f66afa6"
      ],
      "generated_media": [
        {
          "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
          "type": "JSON"
        }
      ],
      "generated_profile": {
        "media": {
          "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
          "type": "JSON",
          "created": "2021-06-11T11:39:24Z",
          "last_updated": "2021-06-11T11:39:24Z"
        }
      },
      "report": {
        "recommendation": {
          "value": "APPROVE"
        },
        "breakdown": [
          {
            "sub_check": "string",
            "result": "PASS",
            "details": []
          }
        ],
        "watchlist_summary": {
          "total_hits": 0,
          "search_config": {
            "categories": [
              "ADVERSE-MEDIA"
            ]
          },
          "raw_results": {
            "media": {
              "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
              "type": "JSON",
              "created": "2021-06-11T11:39:24Z",
              "last_updated": "2021-06-11T11:39:24Z"
            }
          },
          "associated_country_codes": [
            "GBR",
            "USA"
          ]
        }
      },
      "created": "2021-06-11T11:39:24Z",
      "last_updated": "2021-06-11T11:39:24Z"
    },
    {
      "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "type": "WATCHLIST_ADVANCED_CA",
      "state": "CREATED",
      "resources_used": [
        "3fa85f64-5717-4562-b3fc-2c963f66afa6"
      ],
      "generated_media": [
        {
          "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
          "type": "JSON"
        }
      ],
      "generated_profile": {
        "media": {
          "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
          "type": "JSON",
          "created": "2021-06-11T11:39:24Z",
          "last_updated": "2021-06-11T11:39:24Z"
        }
      },
      "report": {
        "recommendation": {
          "value": "APPROVE"
        },
        "breakdown": [
          {
            "sub_check": "string",
            "result": "PASS",
            "details": []
          }
        ],
        "watchlist_summary": {
          "total_hits": 0,
          "search_config": {
            "categories": [
              "ADVERSE-MEDIA"
            ]
          },
          "raw_results": {
            "media": {
              "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
              "type": "JSON",
              "created": "2021-06-11T11:39:24Z",
              "last_updated": "2021-06-11T11:39:24Z"
            }
          },
          "associated_country_codes": [
            "GBR",
            "USA"
          ]
        }
      },
      "created": "2021-06-11T11:39:24Z",
      "last_updated": "2021-06-11T11:39:24Z"
    }
  ]
}
{% /tab %}
{% /code %}

### AML raw

You have the ability to extract the raw results from the comply advantage API, as well as a link to a comply advantage page displaying the hits (if any) by using the raw_results ID. 

{% code %}
{% tab language="javascript" title="Node.js" %}
idvClient.getMediaContent(sessionId, rawResultsId).then(media => {
    const content = media.getContent();
    const buffer = content.toBuffer();
    const jsonData = JSON.parse(buffer);
}).catch(error => {
    console.log(error)
    // handle error
})
{% /tab %}
{% tab language="java" %}
Media media = docScanClient.getMediaContent(sessionId, rawResultsId);
{% /tab %}
{% tab language="php" %}
<?php
$media = $docScanClient->getMediaContent($sessionId, $rawResultsId);
$data = json_decode($media->getContent());
{% /tab %}
{% tab language="python" %}
// COMING SOON
{% /tab %}
{% tab language="csharp" %}
// COMING SOON
{% /tab %}
{% tab language="json" %}
[
  {
    "provider": "Comply Advantage",
    "search_types": [
      "sanction",
      "warning",
      "fitness-probity",
      "pep",
      "adverse-media"
    ],
    "search_id": "616943686",
    "search_ref": "1629902969-04sjnJ47",
    "url": "",
    "raw_output": "base64_encoded_string"
  }
]
{% /tab %}
{% /code %}