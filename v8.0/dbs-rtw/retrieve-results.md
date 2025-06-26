---
type: page
title: Retrieve results
listed: true
slug: retrieve-results
description: 
index_title: Retrieve results
hidden: 
keywords: 
tags: 
---

Each session has a configured 'time to live' (TTL) which must be above 300 seconds (5 minutes). When a session is created, it remains active until its 'time to live' is reached.
For any active session, you can use the Yoti SDK to retrieve a report on the session (containing the end-user's uploaded documents and associated metadata).

{% html %}
<div class="alert-know">
    <div class="alert-title" id="know">
        Recommendation
    </div>
    <div class="alert-text">
Yoti strongly recommends you use notifications for each session status.    </div>
    <div class="alert-links"> 
       <a href="https://developers.yoti.com/dbs-rtw/notifications">Notifications</a>
    </div>
</div>
{% /html %}

This page explains how to:

- Retrieve the results of the session.
- Retrieve the associated media.
- Display the Identity Profile Report for the session.

---

## Result of the session

Session retrieval requires a session ID, this is generated from the create a session endpoint.  Below is a basic example of what retrieving a session looks like:

{% code %}
{% tab language="javascript" %}
// Returns a session result
const sessionResult = await idvClient.getSession(sessionId);

// Returns the session state
const state = sessionResult.getState();

// Returns session resources
const resources = session.getResources();
{% /tab %}
{% tab language="java" %}
// Returns a session result
GetSessionResult sessionResult = docScanClient.getSession(sessionId);

// Returns the session state
String state = sessionResult.getState();

// Returns session resources
ResourceContainer resources = sessionResult.getResources();
{% /tab %}
{% tab language="php" %}
// Returns a session result
$sessionResult = $docScanClient->getSession($sessionId);

// Returns the session state
$state = $sessionResult->getState();

// Returns session resources
$resources = $sessionResult->getResources();
{% /tab %}
{% tab language="csharp" %}
// Returns a session result
GetSessionResult sessionResult = docScanClient.GetSession(sessionId);

// Returns the session state
string state = sessionResult.State;

// Returns session resources
ResourceContainer resources = sessionResult.Resources;
{% /tab %}
{% tab language="go" %}
// Returns a session result
sessionResult, err := client.GetSession(sessionId)
if err != nil {
  	return nil, err
}

// Returns the session state
state = sessionResult.State

// Returns session resources
resources = sessionResult.Resources
{% /tab %}
{% /code %}

The following are present in every session result:

{% table %}
| Value | Description | 
| ---- | ---- | 
| State | The current state of the session. It provides the overall state of the session. \n\n\n\nYou can search through session results prior to this being completed, but some checks may not have been processed yet. | 
| Resources | A container of all ID documents and liveness captures for this session. | 
| Checks | A container of all checks performed for this session. | 
{% /table %}

---

## Retrieve the Media

Document images from the user, text extraction fields and liveness captures for the session are available inside the resources container. These can be retrieved by looking at the relevant media ID inside the documents collection.

{% code %}
{% tab language="javascript" %}
// Returns a collection of ID Documents
const idDocuments = resources.getIdDocuments();

// Returns document fields object
const documentFields = idDocuments[0].getDocumentFields();

const mediaId = documentFields.getMedia().getId();
const media = await idvClient.getMediaContent(sessionId, mediaId);

const buffer = media.getContent();
const base64Content = media.getBase64Content();
const mimeType = media.getMimeType();
{% /tab %}
{% tab language="java" %}
// Returns a collection of ID Documents
List<? extends IdDocumentResourceResponse> idDocuments = resources.getIdDocuments();

String mediaId = idDocuments[0].getDocumentFields()..getMedia().getId();

Media media = docScanClient.getMediaContent(sessionId, mediaId);
{% /tab %}
{% tab language="php" %}
// Returns a collection of ID Documents
$idDocuments = $resources->getIdDocuments();

$mediaId = $idDocuments[0]->getDocumentFields()->getMedia()->getId();

$media = $docScanClient->getMediaContent($sessionId, $mediaId);
$base64Content = $media->getBase64Content();
$contentType = $media->getMimeType();
{% /tab %}
{% tab language="csharp" %}
// Returns a collection of ID Documents
List<IdDocumentResourceResponse> idDocuments = resources.IdDocuments;

string mediaId = idDocuments[0].DocumentFields.Media.Id();

MediaValue media = docScanClient.GetMediaContent(sessionId, mediaId);
{% /tab %}
{% tab language="go" %}
// Returns a collection of ID Documents
idDocuments = resources.IDDocuments

// Returns document fields object
documentFields = idDocuments[0].DocumentFields
mediaID = documentFields.Media.ID

media, err := client.GetMediaContent(sessionId, mediaID)
if err != nil {
  	return nil, err
}

mimeType = media.MIME()
data = media.Data()
{% /tab %}
{% /code %}

---

## Retrieve the Identity Profile

Once the session has reached the state of 'Completed', identity profile can be successfully retrieved.

In case of a successful transaction, once the identity profile is received, the identity profile report JSON will be accessible. This contains the media ID which can then be used to get the full JSON response of the report.

{% code %}
{% tab language="javascript" %}
const identityProfile = sessionResult.getIdentityProfile();
const identityProfileReport = identityProfile.getIdentityProfileReport();

const mediaId = identityProfileReport.getMedia().getId();
const identityProfileReportMedia = await idvClient.getMediaContent(sessionId, mediaId);

const identityProfileReportMediaBuffer = identityProfileReportMedia.getContent();
{% /tab %}
{% tab language="java" %}
IdentityProfile identityProfile = sessionResult.getIdentityProfile();
IdentityProfileReport identityProfileReport = identityProfile.getIdentityProfileReport();

String mediaID = identityProfileReport.getMedia().getId();
Media identityProfileReportMedia = await docScanClient.getMediaContent(sessionId, mediaId);
{% /tab %}
{% tab language="php" %}
$identityProfile = $sessionResult->getIdentityProfile();
$identityProfileReport = $identityProfile->getIdentityProfileReport();

$mediaID = identityProfileReport->getMedia()->getId();

$identityProfileReportMedia = $docScanClient->getMediaContent($sessionId, $mediaId);
$base64Content = $media->getBase64Content();
$contentType = $media->getMimeType();
{% /tab %}
{% tab language="csharp" %}
string mediaId = sessionResult.IdentityProfile.Report["media"]["id"].ToString();
MediaValue mediaValue = docScanClient.GetMediaContent(sessionId, mediaId);

byte[] identityProfileReport = mediaValue.GetContent();
{% /tab %}
{% tab language="go" %}
identityProfile = sessionResult.IdentityProfileResponse
identityProfileReport = identityProfile.IdentityProfileResponse.Report

media, err := identityProfile.Report["media"].(map[string]interface{})
mediaID, err := media["id"].(string)

identityProfileReportMedia, err := client.GetMediaContent(sessionId, mediaID)
{% /tab %}
{% /code %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Jump to..
    </div>
    <div class="alert-text">
        Get a deeper dive on the identity profile and understanding the report.
    </div>
    <div class="alert-links"> 
        <a href="https://developers.yoti.com/dbs-rtw/identity-profile-report">Identity Profile Report</a>        
   </div>
</div>
{% /html %}

---

## Session Result Parameters

The session result contains the session metadata, ID checks, uploaded documents and the identity profile report.

{% table %}
| Parameter | Type | Description | Included | 
| ---- | ---- | ---- | ---- | 
| SessionResult | Object | Complete Session Result | Always | 
| sessionId | String | Unique Session ID | Always | 
| userTrackingId | String | Unique User Tracking ID | Optional | 
| state | String | The current state of the session. \n\nEnum: ONGOING, COMPLETED, EXPIRED | Always | 
| clientSessionToken | String | Token for the user session. | Optional | 
| clientSessionTokenTtl | Integer | Remaining time the user has to complete the session. | Optional | 
| checks | []Object | List of all the checks performed. | Always | 
| resources | Object | Collection of all the resources created. | Always | 
| biometricConsent | String | Collected biometric consent. | Conditional | 
| identityProfile | Object | Complete Identity profile\n\n(Available when the session is completed). | Always | 
| subjectId | String | Subject identifier provided by the RP at session creation time. | Optional | 
| result | String | Final result of the identity verification. \n\n\n\n'Done' means the identity could be verified and the identity profile report provided. 'Aborted' means the user could not be verified and no identity profile report produced, all the resources and checks are still available. \n\n\n\nEnum: DONE, ABORTED | Always | 
| failureReason | Object | In case of _result: ABORTED,_ reason for the failure. | Optional | 
| reasonCode | String | Reason code for the failure. Please see error codes for full list | Conditional | 
| identityProfileReport | Object | The identity profile report media contains the identity attributes and the verification report that certifies the scheme compliance and achieved verification level. | Conditional | 
| trustFramework | String | Defines under which trust framework this identity was verified. As defined at session creation time. \n\n\n\nEnum: UK_TFIDA | Conditional | 
| schemesCompliance | []Object | Defines which schemes (of the requested ones) this identity profile satisfies. | Conditional | 
| scheme | Boolean | Scheme defines the identity scheme. | Conditional | 
| requirementsMet | String | Asserts whether the identity scheme requirements were met or not. | Conditional | 
| requirementsNotMetInfo | Object | Provides info on why the scheme requirements were not met. | Conditional | 
| media | String | Full identity profile report provided as a JSON media. | Conditional | 
| created | String | Uses the ISO8601 standard representation of date times. | Conditional | 
| last_updated | String | Uses the ISO8601 standard representation of date times. | Conditional | 
| id | String | Identifier to be used to fetch this media. | Conditional | 
| type | String | JSON Enum: IMAGE, JSON,BINARY | Conditional | 
{% /table %}

---

## Example JSON Response

{% code %}
{% tab language="json" %}
{
   "client_session_token_ttl":8533,
   "session_id":"4e55f745-d0d4-49ff-b975-765b8c541189",
   "state":"COMPLETED",
   "resources":{
      "id_documents":[
         {
            "id":"c95aaf96-e40d-488e-9d22-b93f738ed3d1",
            "tasks":[
               {
                  "type":"ID_DOCUMENT_TEXT_DATA_EXTRACTION",
                  "id":"fbcebb36-03ee-4d57-8735-a355c7d8cf69",
                  "state":"DONE",
                  "created":"2022-06-08T09:29:38Z",
                  "last_updated":"2022-06-08T09:30:30Z",
                  "generated_checks":[
                     
                  ],
                  "generated_media":[
                     {
                        "id":"5be222ef-f3ec-42cc-8448-0e85d65c550f",
                        "type":"JSON"
                     }
                  ]
               }
            ],
            "source":{
               "type":"END_USER"
            },
            "document_type":"PASSPORT",
            "issuing_country":"GBR",
            "pages":[
               {
                  "capture_method":"CAMERA",
                  "media":{
                     "id":"81d0cb53-5788-491e-8b3a-b8f5f3706c30",
                     "type":"IMAGE",
                     "created":"2022-06-08T09:30:26Z",
                     "last_updated":"2022-06-08T09:30:26Z"
                  },
                  "frames":[
                     {
                        "media":{
                           "id":"7d8c8a39-23bb-4591-aac6-9737678c890b",
                           "type":"IMAGE",
                           "created":"2022-06-08T09:30:27Z",
                           "last_updated":"2022-06-08T09:30:27Z"
                        }
                     },
                     {
                        "media":{
                           "id":"24c0f4ab-b192-4fc2-901a-c6d3d55040ec",
                           "type":"IMAGE",
                           "created":"2022-06-08T09:30:27Z",
                           "last_updated":"2022-06-08T09:30:27Z"
                        }
                     },
                     {
                        "media":{
                           "id":"23965901-ec62-452a-875c-037921b9a90c",
                           "type":"IMAGE",
                           "created":"2022-06-08T09:30:27Z",
                           "last_updated":"2022-06-08T09:30:27Z"
                        }
                     }
                  ]
               }
            ],
            "document_fields":{
               "media":{
                  "id":"5be222ef-f3ec-42cc-8448-0e85d65c550f",
                  "type":"JSON",
                  "created":"2022-06-08T09:30:30Z",
                  "last_updated":"2022-06-08T09:30:30Z"
               }
            },
            "document_id_photo":{
               "media":{
                  "id":"d2aab2b1-5b53-43a5-ab42-3d65cc04e9e5",
                  "type":"IMAGE",
                  "created":"2022-06-08T09:30:30Z",
                  "last_updated":"2022-06-08T09:30:30Z"
               }
            }
         },
         {
            "id":"847bf65c-63ba-4aba-adf3-abff0083d06c",
            "tasks":[
               {
                  "type":"ID_DOCUMENT_TEXT_DATA_EXTRACTION",
                  "id":"3fd07a99-625a-4113-9b66-6904c3ac3283",
                  "state":"DONE",
                  "created":"2022-06-08T09:28:41Z",
                  "last_updated":"2022-06-08T09:29:11Z",
                  "generated_checks":[
                     
                  ],
                  "generated_media":[
                     {
                        "id":"7e7dd1d4-5d78-4f02-9d6b-e026c3bf641e",
                        "type":"JSON"
                     }
                  ]
               }
            ],
            "source":{
               "type":"END_USER"
            },
            "document_type":"DRIVING_LICENCE",
            "issuing_country":"GBR",
            "pages":[
               {
                  "capture_method":"CAMERA",
                  "media":{
                     "id":"04d7fc5c-70a3-4f89-b060-e26c1e6b1953",
                     "type":"IMAGE",
                     "created":"2022-06-08T09:29:07Z",
                     "last_updated":"2022-06-08T09:29:07Z"
                  },
                  "frames":[
                     {
                        "media":{
                           "id":"4198e1c4-e7a1-4489-a13a-70a5b45c9198",
                           "type":"IMAGE",
                           "created":"2022-06-08T09:29:08Z",
                           "last_updated":"2022-06-08T09:29:08Z"
                        }
                     },
                     {
                        "media":{
                           "id":"343ad625-daf6-413f-9969-0bf6da807517",
                           "type":"IMAGE",
                           "created":"2022-06-08T09:29:08Z",
                           "last_updated":"2022-06-08T09:29:08Z"
                        }
                     }
                  ]
               },
               {
                  "capture_method":"CAMERA",
                  "media":{
                     "id":"b1fab41b-08cf-4120-9db8-ea0b3e7d43a7",
                     "type":"IMAGE",
                     "created":"2022-06-08T09:29:07Z",
                     "last_updated":"2022-06-08T09:29:07Z"
                  },
                  "frames":[
                     {
                        "media":{
                           "id":"6638c4e5-50af-4cb7-b02b-9dac8d7fd751",
                           "type":"IMAGE",
                           "created":"2022-06-08T09:29:08Z",
                           "last_updated":"2022-06-08T09:29:08Z"
                        }
                     },
                     {
                        "media":{
                           "id":"c812b3d2-dbf6-4042-a67c-89a25d437639",
                           "type":"IMAGE",
                           "created":"2022-06-08T09:29:08Z",
                           "last_updated":"2022-06-08T09:29:08Z"
                        }
                     }
                  ]
               }
            ],
            "document_fields":{
               "media":{
                  "id":"7e7dd1d4-5d78-4f02-9d6b-e026c3bf641e",
                  "type":"JSON",
                  "created":"2022-06-08T09:29:11Z",
                  "last_updated":"2022-06-08T09:29:11Z"
               }
            },
            "document_id_photo":{
               "media":{
                  "id":"ed0b1657-5fb8-4b7c-ad5b-5971dae20141",
                  "type":"IMAGE",
                  "created":"2022-06-08T09:29:11Z",
                  "last_updated":"2022-06-08T09:29:11Z"
               }
            }
         }
      ],
      "supplementary_documents":[
         
      ],
      "liveness_capture":[
         {
            "id":"c687cc97-466d-49c3-a45e-cba6bca0805f",
            "tasks":[
               
            ],
            "source":{
               "type":"END_USER"
            },
            "frames":[
               {
                  "media":{
                     "id":"eaa25756-921a-4551-bb62-6ed43106751e",
                     "type":"IMAGE",
                     "created":"2022-06-08T09:31:11Z",
                     "last_updated":"2022-06-08T09:31:11Z"
                  }
               },
               {
                  "media":{
                     "id":"f08ba209-1933-429b-af73-91b0c2e90177",
                     "type":"IMAGE",
                     "created":"2022-06-08T09:31:11Z",
                     "last_updated":"2022-06-08T09:31:11Z"
                  }
               },
               {
                  "media":{
                     "id":"a5c52110-0e8e-4689-b4b2-2438e2f150bf",
                     "type":"IMAGE",
                     "created":"2022-06-08T09:31:11Z",
                     "last_updated":"2022-06-08T09:31:11Z"
                  }
               },
               {
                  
               },
               {
                  
               },
               {
                  
               },
               {
                  
               }
            ],
            "liveness_type":"ZOOM",
            "facemap":{
               "media":{
                  "id":"c75e59e0-a7ed-4790-ae7c-36d01fbabd02",
                  "type":"BINARY",
                  "created":"2022-06-08T09:31:12Z",
                  "last_updated":"2022-06-08T09:31:12Z"
               }
            }
         },
         {
            "id":"025fe786-4139-40c2-ad4f-dd05605e499f",
            "tasks":[
               
            ],
            "source":{
               "type":"END_USER"
            },
            "frames":[
               {
                  "media":{
                     "id":"030480d6-8da5-43fa-a0a3-4bc604e860e4",
                     "type":"IMAGE",
                     "created":"2022-06-08T09:30:52Z",
                     "last_updated":"2022-06-08T09:30:52Z"
                  }
               },
               {
                  "media":{
                     "id":"ae9cfe10-80cc-46db-9c1d-ef7a4ca234f8",
                     "type":"IMAGE",
                     "created":"2022-06-08T09:30:52Z",
                     "last_updated":"2022-06-08T09:30:52Z"
                  }
               },
               {
                  "media":{
                     "id":"c937b9e7-929a-4618-94c1-cb36beddc902",
                     "type":"IMAGE",
                     "created":"2022-06-08T09:30:52Z",
                     "last_updated":"2022-06-08T09:30:52Z"
                  }
               },
               {
                  
               },
               {
                  
               },
               {
                  
               },
               {
                  
               }
            ],
            "liveness_type":"ZOOM",
            "facemap":{
               "media":{
                  "id":"34494940-c676-4826-ba7d-d9c1292051b5",
                  "type":"BINARY",
                  "created":"2022-06-08T09:30:53Z",
                  "last_updated":"2022-06-08T09:30:53Z"
               }
            }
         }
      ],
      "face_capture":[
         
      ],
      "applicant_profiles":[
         
      ]
   },
   "checks":[
      {
         "type":"ID_DOCUMENT_AUTHENTICITY",
         "id":"ed5e34bf-4d57-43fc-92e3-1f3f2ff030ea",
         "state":"DONE",
         "resources_used":[
            "c687cc97-466d-49c3-a45e-cba6bca0805f",
            "847bf65c-63ba-4aba-adf3-abff0083d06c"
         ],
         "generated_media":[
            
         ],
         "report":{
            "recommendation":{
               "value":"APPROVE"
            },
            "breakdown":[
               {
                  "sub_check":"doc_number_validation",
                  "result":"PASS",
                  "details":[
                     
                  ]
               },
               {
                  "sub_check":"document_in_date",
                  "result":"PASS",
                  "details":[
                     
                  ]
               },
               {
                  "sub_check":"fraud_list_check",
                  "result":"PASS",
                  "details":[
                     
                  ]
               },
               {
                  "sub_check":"hologram",
                  "result":"PASS",
                  "details":[
                     
                  ]
               },
               {
                  "sub_check":"hologram_movement",
                  "result":"FAIL",
                  "details":[
                     
                  ]
               },
               {
                  "sub_check":"no_sign_of_forgery",
                  "result":"PASS",
                  "details":[
                     
                  ]
               },
               {
                  "sub_check":"no_sign_of_tampering",
                  "result":"PASS",
                  "details":[
                     
                  ]
               },
               {
                  "sub_check":"other_security_features",
                  "result":"PASS",
                  "details":[
                     
                  ]
               },
               {
                  "sub_check":"physical_document_captured",
                  "result":"PASS",
                  "details":[
                     
                  ]
               }
            ]
         },
         "created":"2022-06-08T09:31:16Z",
         "last_updated":"2022-06-08T09:32:22Z"
      },
      {
         "type":"ID_DOCUMENT_AUTHENTICITY",
         "id":"e4c56536-2f90-4f1b-bf8e-7b6093faf343",
         "state":"DONE",
         "resources_used":[
            "c687cc97-466d-49c3-a45e-cba6bca0805f",
            "c95aaf96-e40d-488e-9d22-b93f738ed3d1"
         ],
         "generated_media":[
            
         ],
         "report":{
            "recommendation":{
               "value":"APPROVE"
            },
            "breakdown":[
               {
                  "sub_check":"document_in_date",
                  "result":"PASS",
                  "details":[
                     
                  ]
               },
               {
                  "sub_check":"fraud_list_check",
                  "result":"PASS",
                  "details":[
                     
                  ]
               },
               {
                  "sub_check":"hologram",
                  "result":"PASS",
                  "details":[
                     
                  ]
               },
               {
                  "sub_check":"hologram_movement",
                  "result":"FAIL",
                  "details":[
                     
                  ]
               },
               {
                  "sub_check":"mrz_validation",
                  "result":"PASS",
                  "details":[
                     
                  ]
               },
               {
                  "sub_check":"no_sign_of_forgery",
                  "result":"PASS",
                  "details":[
                     
                  ]
               },
               {
                  "sub_check":"no_sign_of_tampering",
                  "result":"PASS",
                  "details":[
                     
                  ]
               },
               {
                  "sub_check":"ocr_mrz_comparison",
                  "result":"PASS",
                  "details":[
                     
                  ]
               },
               {
                  "sub_check":"other_security_features",
                  "result":"PASS",
                  "details":[
                     
                  ]
               },
               {
                  "sub_check":"physical_document_captured",
                  "result":"PASS",
                  "details":[
                     
                  ]
               }
            ]
         },
         "created":"2022-06-08T09:31:16Z",
         "last_updated":"2022-06-08T09:32:01Z"
      },
      {
         "type":"LIVENESS",
         "id":"81f1c253-03b4-476d-b2b9-8c893c4f3c8c",
         "state":"DONE",
         "resources_used":[
            "c687cc97-466d-49c3-a45e-cba6bca0805f"
         ],
         "generated_media":[
            
         ],
         "report":{
            "recommendation":{
               "value":"APPROVE"
            },
            "breakdown":[
               {
                  "sub_check":"liveness_auth",
                  "result":"PASS",
                  "details":[
                     
                  ]
               }
            ]
         },
         "created":"2022-06-08T09:31:12Z",
         "last_updated":"2022-06-08T09:31:14Z"
      },
      {
         "type":"LIVENESS",
         "id":"ab4d549d-874a-4ed4-9dd5-923204dd55d5",
         "state":"DONE",
         "resources_used":[
            "025fe786-4139-40c2-ad4f-dd05605e499f"
         ],
         "generated_media":[
            
         ],
         "report":{
            "recommendation":{
               "value":"REJECT"
            },
            "breakdown":[
               {
                  "sub_check":"liveness_auth",
                  "result":"FAIL",
                  "details":[
                     
                  ]
               }
            ]
         },
         "created":"2022-06-08T09:30:53Z",
         "last_updated":"2022-06-08T09:30:55Z"
      },
      {
         "type":"ID_DOCUMENT_FACE_MATCH",
         "id":"4215e3be-7cdb-428e-be6a-93e3a8475026",
         "state":"DONE",
         "resources_used":[
            "c687cc97-466d-49c3-a45e-cba6bca0805f",
            "847bf65c-63ba-4aba-adf3-abff0083d06c"
         ],
         "generated_media":[
            
         ],
         "report":{
            "recommendation":{
               "value":"APPROVE"
            },
            "breakdown":[
               {
                  "sub_check":"ai_face_match",
                  "result":"PASS",
                  "details":[
                     {
                        "name":"confidence_score",
                        "value":"0.82"
                     }
                  ]
               }
            ]
         },
         "created":"2022-06-08T09:31:16Z",
         "last_updated":"2022-06-08T09:31:18Z"
      },
      {
         "type":"ID_DOCUMENT_FACE_MATCH",
         "id":"2b19e2cb-31ce-4a35-bf0b-f98e9da252e3",
         "state":"DONE",
         "resources_used":[
            "c687cc97-466d-49c3-a45e-cba6bca0805f",
            "c95aaf96-e40d-488e-9d22-b93f738ed3d1"
         ],
         "generated_media":[
            
         ],
         "report":{
            "recommendation":{
               "value":"APPROVE"
            },
            "breakdown":[
               {
                  "sub_check":"ai_face_match",
                  "result":"PASS",
                  "details":[
                     {
                        "name":"confidence_score",
                        "value":"0.78"
                     }
                  ]
               }
            ]
         },
         "created":"2022-06-08T09:31:16Z",
         "last_updated":"2022-06-08T09:31:18Z"
      },
      {
         "type":"THIRD_PARTY_IDENTITY_FRAUD_1",
         "id":"b4d817e8-8468-41d3-a181-1d110233f9af",
         "state":"DONE",
         "resources_used":[
            
         ],
         "generated_media":[
            {
               "id":"14e843d5-7d26-4527-940e-53f920fdb1c1",
               "type":"JSON"
            }
         ],
         "report":{
            "recommendation":{
               "value":"APPROVE"
            },
            "breakdown":[
               {
                  "sub_check":"check_performed",
                  "result":"PASS",
                  "details":[
                     {
                        "name":"provider_org",
                        "value":"redacted/IDFP_1"
                     }
                  ]
               }
            ]
         },
         "created":"2022-06-08T09:31:15Z",
         "last_updated":"2022-06-08T09:31:16Z",
         "generated_profile":{
            "media":{
               "id":"14e843d5-7d26-4527-940e-53f920fdb1c1",
               "type":"JSON",
               "created":"2022-06-08T09:31:16Z",
               "last_updated":"2022-06-08T09:31:16Z"
            }
         }
      }
   ],
   "biometric_consent":"2022-06-08T09:30:37Z",
   "identity_profile":{
      "result":"DONE",
      "identity_profile_report":{
         "trust_framework":"UK_TFIDA",
         "media":{
            "id":"56fa48e0-ac21-4cf5-a9b2-af3eb6d489e8",
            "type":"JSON",
            "created":"2022-06-08T09:32:23Z",
            "last_updated":"2022-06-08T09:32:23Z"
         },
         "schemes_compliance":[
            {
               "scheme":{
                  "type":"DBS",
                  "objective":"BASIC"
               },
               "requirements_met":true
            }
         ]
      }
   }
}
{% /tab %}
{% /code %}