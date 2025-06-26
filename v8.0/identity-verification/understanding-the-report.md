---
type: page
title: Understanding the report
listed: true
slug: understanding-the-report
description: 
index_title: Understanding the report
hidden: 
keywords: 
tags: 
---

The Identity verification SDK allows you to tailor your report and response. In this section we explain in more detail what each report shows. 

It's really important that you understand our sub checks and look at all the results from the checks.

{% html %}
<div class="alert-SAND">
    <div class="alert-title" id="SAND">
      Sandbox
    </div>
    <div class="alert-text">
       If you have integrated the Sandbox environment, please reference the breakdown through this page.
    </div>
    <div class="alert-links"> 
        <a href="https://developers.yoti.com/identity-verification/sandbox#sandbox-breakdown">Sandbox breakdown</a>
    </div>
</div>
{% /html %}

## Result of the session

An example session result is shown below, with explanation of the objects given underneath.

{% code %}
{% tab language="javascript" %}
const {
IDVClient,
} = require('yoti');
  const idvClient = new IDVClient(
    process.env.YOTI_CLIENT_SDK_ID,
    fs.readFileSync('pem.pem')
  )
  
  idvClient.getSession('your_session_id').then(session => {
    const sessionId = session.getSessionId();
    const clientSessionTokenTtl = session.getClientSessionTokenTtl();
    const state = session.getState();
    const clientSessionToken = session.getClientSessionToken();
    const userTrackingId = session.getUserTrackingId();

    const checks = session.getChecks();
    const authenticityChecks = session.getAuthenticityChecks();
    const faceMatchChecks = session.getFaceMatchChecks();
    const textDataChecks = session.getTextDataChecks();
    const livenessChecks = session.getLivenessChecks();

    const resources = session.getResources();
}).catch(error => {
    // handle error
})
{% /tab %}
{% tab language="java" %}
DocScanClient docScanClient = DocScanClientBuilder.newInstance()
        .withClientSdkId(YOTI_CLIENT_SDK_ID)
        .withKeyPairSource(ClassPathKeySource.fromClasspath(PEM_PATH))
        .build();

GetSessionResult sessionResult = docScanClient.getSession(sessionId);

Long clientSessionTokenttl = sessionResult.getClientSessionTokenTtl();
String state = sessionResult.getState();
String clientSessionToken = sessionResult.getClientSessionToken();
String userTrackingId = sessionResult.getUserTrackingId();

List<? extends CheckResponse> checks = sessionResult.getChecks();
List<AuthenticityCheckResponse> authenticityChecks = sessionResult.getAuthenticityChecks();
List<FaceMatchCheckResponse> faceMatchChecks = sessionResult.getFaceMatchChecks();
List<TextDataCheckResponse> textDataChecks = sessionResult.getTextDataChecks();
List<LivenessCheckResponse> livenessChecks = sessionResult.getLivenessChecks();

ResourceContainer resources = sessionResult.getResources();
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\DocScan\DocScanClient;

$YOTI_CLIENT_SDK_ID = 'YOUR_SDK_ID';
$YOTI_PEM = '/path/to/pem';

// Create Doc Scan Client
$docScanClient = new DocScanClient($YOTI_CLIENT_SDK_ID, $YOTI_PEM);
// Returns a session result
$sessionResult = $docScanClient->getSession('DOC_SCAN_SESSION_ID');
// Returns the session state
$sessionState = $sessionResult->getState();
// Returns the session Id
$sessionId = $sessionResult->getSessionId();
// Returns the user tracking Id
$userTrackingId = $sessionResult->getUserTrackingId();
// Returns the client session token
$clientSessionToken = $sessionResult->getClientSessionToken();
// Returns the client session token ttl
$clientSessionTokenTtl = $sessionResult->getClientSessionTokenTtl();

// Returns all sessions checks
$checks = $sessionResult->getChecks();
// Returns all Document Authenticity Checks
$authenticityChecks = $sessionResult->getAuthenticityChecks();
// Returns all Text Data Checks
$textDataChecks = $sessionResult->getTextDataChecks();
// Returns all Liveness Checks
$livenessChecks = $sessionResult->getLivenessChecks();
// Returns all Face Match Checks
$faceMatchChecks = $sessionResult->getFaceMatchChecks();

// Returns all resources
$resources = $sessionResult->getResources();
{% /tab %}
{% tab language="python" %}
from yoti_python_sdk.doc_scan import (
    DocScanClient
)

YOTI_CLIENT_SDK_ID = 'YOUR_SDK_ID'
YOTI_PEM = '/path/to/pem'

doc_scan_client = DocScanClient(YOTI_CLIENT_SDK_ID, YOTI_PEM)

session_result = doc_scan_client.get_session('your_session_id')

client_session_token_ttl = session_result.client_session_token_ttl
state = session_result.state
client_session_token = session_result.client_session_token
user_tracking_id = session_result.user_tracking_id

checks = session_result.checks
authenticity_checks = session_result.authenticity_checks
face_match_checks = session_result.face_match_checks
text_data_checks = session_result.text_data_checks
liveness_checks = session_result.liveness_checks

resources = session_result.resources
{% /tab %}
{% tab language="csharp" %}
var docScanClient = new DocScanClient(YOTI_CLIENT_SDK_ID, key, new HttpClient());

GetSessionResult sessionResult = docScanClient.GetSession(sessionId);

int clientSessionTokenTtl = sessionResult.ClientSessionTokenTtl;
string state = sessionResult.State;
string clientSessionToken = sessionResult.ClientSessionToken;
string user_tracking_id = sessionResult.UserTrackingId;

List<CheckResponse> checks = sessionResult.Checks;
List<AuthenticityCheckResponse> authenticityChecks = sessionResult.GetAuthenticityChecks();
List<FaceMatchCheckResponse> faceMatchChecks = sessionResult.GetFaceMatchChecks();
List<TextDataCheckResponse> textDataChecks = sessionResult.GetTextDataChecks();
List<LivenessCheckResponse> livenessChecks = sessionResult.GetLivenessChecks();

ResourceContainer resources = sessionResult.Resources;
{% /tab %}
{% tab language="go" %}
sdkId := "YOUR_SDK_ID"
key, _ := ioutil.ReadFile("/path/to/pem")

client, err := docscan.NewClient(sdkId, key)
if err != nil {
	fmt.Println(err)
}

sessionResult, err := client.GetSession("YOUR_SESSION_ID")
if err != nil {
	fmt.Println(err)
}

sessionId := sessionResult.SessionID
clientSessionTokenTtl := sessionResult.ClientSessionTokenTTL
state := sessionResult.State
clientSessionToken := sessionResult.ClientSessionToken
userTrackingId := sessionResult.UserTrackingID

checks := sessionResult.Checks
authenticityChecks := sessionResult.AuthenticityChecks()
faceMatchChecks := sessionResult.FaceMatchChecks()
textDataChecks := sessionResult.TextDataChecks()
livenessChecks := sessionResult.LivenessChecks()

resources := sessionResult.Resources
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
    }
  ]
}
{% /tab %}
{% /code %}

{% table %}
| Parameter | Value | Description | 
| ---- | ---- | ---- | 
| Session ID | uuid | session ID. Each session ID is unique. | 
| Client session token | uuid | Returns the client session token. Used to authenticate the session. | 
| Session state | ONGOING COMPLETED EXPIRED | Yoti is still working on tasks and checks for the user's ID. \n\nYoti has completed checks and tasks.\n\nYoti could not complete the checks and tasks. | 
| Client session token ttl | seconds | Returns the time left in seconds until the the session expires. | 
| User tracking ID | user ID | The user ID you set in your backend | 
| Client session token | uuid | Returns the client session token | 
| Checks | N/A | Returns the results of the checks in an array. | 
| Authenticity checks | See below | Returns all authenticity checks for that session with ID's and state. | 
| Text data checks | See below | Returns all extraction checks for that session with ID's and state. | 
| Liveness checks | See below | Returns all liveness checks for that session with ID's and state. | 
| Face match  checks | See below | Returns all face match checks for that session with ID's and state. | 
{% /table %}

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
        Sessions may contain multiple checks, tasks and resources depending on the requested configuration.
    </div>
</div>
{% /html %}

---

## Retrieve user information

Depending on the configuration of your sessions, you will need to retrieve either ID Document resources, Liveness resources or both.

{% code %}
{% tab language="javascript" %}
// get all the resources
resources = session.getResources();

// get the ID document resources
idDocResources = resources.getIdDocuments();

// get the liveness resources
livenessResources = resources.getLivenessCapture();
{% /tab %}
{% tab language="java" %}
// Get all the resources
ResourceContainer resources = sessionResult.getResources();

// Get the ID document resources
List<? extends  IdDocumentResourceResponse> idDocumentResources = resources.getIdDocuments();

// Get the liveness resources
List<? extends LivenessResourceResponse> livenessResources = resources.getLivenessCapture();
{% /tab %}
{% tab language="php" %}
<?php

// get all the resources
$resources = $session->getResources();

// get the ID document resources
$idDocResources = $resources->getIdDocuments();

// get the liveness resources
$livenessResources = $resources->getLivenessCapture();
{% /tab %}
{% tab language="python" %}
# Returns all resources
resources = session_result.resources

# Returns ID Document resources
id_document_resources = resources.id_documents

# Returns liveness resources
liveness_resources = resources.liveness_capture

# Returns zoom liveness resources
zoom_liveness_resources = resources.zoom_liveness_resources
{% /tab %}
{% tab language="csharp" %}
// Returns all resources
ResourceContainer resources = sessionResult.Resources;

// Returns ID Document resources
List<IdDocumentResourceResponse> idDocumentResources = resources.IdDocuments;

// Returns liveness resources
List<LivenessResourceResponse> livenessResources = resources.LivenessCapture;

// Returns zoom liveness resources
List<ZoomLivenessResourceResponse> zoomLivenessResources = resources.ZoomLivenessResources;
{% /tab %}
{% tab language="json" %}
{
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
    ]
  }
}
{% /tab %}
{% /code %}

### ID Document resources

{% code %}
{% tab language="javascript" %}
idDocResources.forEach((document) => {
  // Get the document id
  id = document.getId();

  // Get the document tasks
  tasks = document.getTasks();

  // Get the document type
  documentType = document.getDocumentType();

  // Get the document issuing country
  issuingCountry = document.getIssuingCountry();

  // Get the document pages
  pages = document.getPages();

  // Get the document fields
  documentFields = document.getDocumentFields();
});
{% /tab %}
{% tab language="java" %}
for (IdDocumentResourceResponse idDocumentResource : idDocumentResources) {

    // Get the document id
    String id = idDocumentResource.getId();

    // Get the document tasks
    List<? extends TaskResponse> tasks = idDocumentResource.getTasks();

    // Get the document type
    String documentType = idDocumentResource.getDocumentType();

    // Get the document issuing country
    String issuingCountry = idDocumentResource.getIssuingCountry();

    // Get the document pages
    List<? extends PageResponse> pages = idDocumentResource.getPages();

    // Get the document fields
    DocumentFieldsResponse documentFields = idDocumentResource.getDocumentFields();
}
{% /tab %}
{% tab language="php" %}
<?php

foreach ($idDocResources as $document) {

  // Get the document id
  $id = $document->getId();

  // Get the document tasks
  $tasks = $document->getTasks();

  // Get the document type
  $documentType = $document->getDocumentType();

  // Get the document issuing country
  $issuingCountry = $document->getIssuingCountry();

  // Get the document pages
  $pages = $document->getPages();

  // Get the document fields
  $documentFields = $document->getDocumentFields();
}
{% /tab %}
{% tab language="python" %}
for id_document_resource in id_document_resources:

    # Returns the Document ID
    id_document_resource_id = id_document_resource.id

    # Returns the document tasks
    tasks = id_document_resource.tasks

    # Returns the document type
    document_type = id_document_resource.document_type

    # Returns the document issuing country
    issuing_country = id_document_resource.issuing_country

    # Returns the document pages
    pages = id_document_resource.pages

    # Returns the document fields
    document_fields = id_document_resource.document_fields
{% /tab %}
{% tab language="csharp" %}
foreach (IdDocumentResourceResponse idDocumentResource in idDocumentResources)
{
    // Returns the document unique id
    string document_uuid = idDocumentResource.Id;

    // Returns the document tasks
    List<TaskResponse> tasks = idDocumentResource.Tasks;

    // Returns the document type
    string documentType = idDocumentResource.DocumentType;

    // Returns the document issuing country
    string issuingCountry = idDocumentResource.IssuingCountry;

    // Returns the document pages
    List<PageResponse> pages = idDocumentResource.Pages;

    // Returns the document fields
    DocumentFieldsResponse documentFields = idDocumentResource.DocumentFields;
}
{% /tab %}
{% tab language="json" %}
{
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
    ]
  }
}
{% /tab %}
{% /code %}

{% table widths="0,186" %}
| Value | Response | Description | 
| ---- | ---- | ---- | 
| id | UUID | ID unique to that resource | 
| tasks | array | any tasks that are performed on the resource | 
| Document Type | eg PASSPORT | The type of document that the user selected before uploading their document images | 
| issuing country | eg GBR | The country the document was issued from (three letter ISO code). | 
| pages | array of media objects | Array of the images taken of the document. Can be retrieved using the getMedia endpoint | 
| Document fields | media object | The extracted text as a JSON object. Can be retrieved using the getMedia endpoint | 
{% /table %}

For the user information and providing examples for each field head over [here](https://developers.yoti.com/identity-verification/data-extraction#data-extracted). 

### Liveness Resources

{% code %}
{% tab language="javascript" %}
livenessResources.forEach((liveness) => {
  // Get the liveness id
  id = liveness.getId();

  // Get the liveness tasks
  tasks = liveness.getTasks();

  // Get the liveness facemap
  facemap = liveness.getFaceMap();

  // Get the liveness frames
  frames = liveness.getFrames();
});
{% /tab %}
{% tab language="java" %}
for (ZoomLivenessResourceResponse livenessResource : livenessResources) {
    // Get the liveness id
    String id = livenessResource.getId();

    // Get the liveness tasks
    List<? extends TaskResponse> tasks = livenessResource.getTasks();

    // Get the liveness facemap
    FaceMapResponse = livenessResource.getFaceMap();
    
    // Get the liveness frames
    List<? extends FrameResponse> frames = livenessResource.getFrames();
}
{% /tab %}
{% tab language="php" %}
<?php

foreach ($livenessResources as $liveness) {
  // Get the liveness id
  $id = $liveness->getId();

  // Get the liveness tasks
  $tasks = $liveness->getTasks();
  
  // Get the liveness type
  $livenessType = $liveness->getLivenessType();
  
  // Get the Zoom liveness resource
  $zoomLiveness = new ZoomLivenessResourceResponse($liveness);
  // Get the Zoom liveness facemap
  $facemap = $zoomLiveness->getFaceMap();
  // Get the Zoom liveness frames
  $frames = $zoomLiveness->getFrames();
  
  // Get the Static liveness resource
  $staticLiveness = new StaticLivenessResourceResponse($liveness);
  // Get the Static liveness imae
  $image = $staticLiveness->getImage();
});
{% /tab %}
{% tab language="python" %}
for liveness_resource in liveness_resources:
    
    # Returns liveness resource id
    liveness_resource_id = liveness_resource.id

    # Returns liveness tasks
    tasks = liveness_resource.tasks

    # Returns liveness facemap
    facemap = liveness_resource.facemap

    # Returns liveness frames
    frames = liveness_resource.frames
{% /tab %}
{% tab language="csharp" %}
foreach (ZoomLivenessResourceResponse livenessResource in livenessResources)
{
    // Returns the liveness id
    string livenessId = livenessResource.Id;

    // Returns the liveness tasks
    List<TaskResponse> tasks = livenessResource.Tasks;

    // Returns the liveness facemap
    FaceMapResponse faceMap = livenessResource.FaceMap;

    // Returns the liveness frames
    List<FrameResponse> frames = livenessResource.Frames;
}
{% /tab %}
{% tab language="json" %}
{
  "resources": {
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
    ]
  }
}
{% /tab %}
{% /code %}

{% table widths="0,154" %}
| Value | Response | Description | 
| ---- | ---- | ---- | 
| id | UUID | ID unique to that resource | 
| tasks | array | Any tasks that are performed on the resource | 
| facemap | media object | A media object containing the 'facemap', which is a biometric signature generated from an image of that person’s face."\n\n\n\nThis can be retrieved using the getMedia endpoint. | 
| frames | array of media objects | Array of the media objects for the Zoom liveness check. Can be used to retrieve images using the getMedia endpoint | 
| image | media object | A media object for the Static liveness check. Can be used to retrieve image using the getMedia endpoint | 
{% /table %}

---

## Result of the checks

Below is an example of the result of each check in more detail. 

{% code %}
{% tab language="javascript" %}
// Can be checks, documentAuthenticityChecks, livenessChecks faceMatchChecks or textDataChecks

checks.forEach((check) => {
  // Get the check type
  type = check.getType();

  // Get the check id
  id = check.getId();

  // Get the state of the check
  state = check.getState();

  // Get the check report
  report = check.getReport();

  // Get the created time
  created = check.getCreated();

  // Get the updated time
  lastUpdated = check.getLastUpdated();

  // Get the resource IDs which have been used when performing this check
  resourcesUsed = check.getResourcesUsed();

  // Get the generated media
  generatedMedia = check.getGeneratedMedia();
});
{% /tab %}
{% tab language="java" %}
// Can be checks, documentAuthenticityChecks, livenessChecks, faceMatchChecks or textDataChecks
for (CheckResponse check : checks) {

    // Get the check type
    String type = check.getType();

    // Get the check id
    String id = check.getId();
    
    // Get the state of the check
    String state = check.getState();
    
    // Get the check report
    ReportResponse report = check.getReport();
    
    // Get the created time
    String created = check.getCreated();
    
    // Get the updated time
    String lastUpdated = check.getLastUpdated();
    
    // Get the resource IDs which have been used when performing this check
    List<String> resourcedUsed = check.getResourcesUsed();
    
    // Get the generated media
    List<? extends GeneratedMedia> generatedMedia = check.getGeneratedMedia();
}
{% /tab %}
{% tab language="php" %}
<?php

// Can be checks, documentAuthenticityChecks, livenessChecks faceMatchChecks or textDataChecks
foreach ($checks as $check) {
    // Get the check type
    $type = $check->getType();

    // Get the check id
    $id = $check->getId();

    // Get the state of the Document Authenticity check
    $state = $check->getState();

    // Get the document authenticity report
    $report = $check->getReport();

    // Get the created time
    $created = $check->getCreated();

    // Get the updated time
    $lastUpdated = $check->getLastUpdated();

    // Get the resource IDs which have been used when performing this check
    $resourcesUsed = $check->getResourcesUsed();

    // Get the generated media
    $generatedMedia = $check->getGeneratedMedia();
}
{% /tab %}
{% tab language="python" %}
# Can be checks, documentAuthenticityChecks, livenessChecks faceMatchChecks or textDataChecks
for check in checks:
    
    # Returns check type
    check_type = check.type

    # Returns check id
    check_id = check.id
    
    # Returns state of check
    state = check.state

    # Returns check report
    report = check.report

    # Returns created time
    created = check.created

    # Returns updated time
    last_updated = check.last_updated

    # Returns resource IDs which have been used when performing this check
    resources_used = check.resources_used

    # Returns generated media
    generated_media = check.generated_media
{% /tab %}
{% tab language="csharp" %}
// Can be checks, documentAuthenticityChecks, livenessChecks faceMatchChecks or textDataChecks
foreach (CheckResponse check in checks)
{
    // Returns check type
    string check_type = check.Type;

    // Returns check id
    string check_id = check.Id;

    // Returns state of check
    string check_state = check.State;

    // Returns check report
    ReportResponse report = check.Report;

    // Returns created time
    DateTime created = check.Created;

    // Returns updated time
    DateTime lastUpdated = check.LastUpdated;

    // Returns the resource IDs which have been used when performing this check
    List<String> resources_used = check.ResourcesUsed;

    // Returns the generated media
    List<GeneratedMedia> generatedMedia = check.GeneratedMedia;
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
    }
  ]
}
{% /tab %}
{% /code %}

{% table %}
| Value | Response | Description | 
| ---- | ---- | ---- | 
| Type | e.g. LivenessCheck | Which type of check was carried out | 
| ID | uuid | The ID of the check | 
| State | e.g. DONE | Status of the check | 
| Report | N/A | Report of the check | 
| Created | Date, Time and Seconds | When the check was created | 
| Last Updated | Date, Time and Seconds | When the check was last updated | 
| Resources used | uuid | The ID of the resources | 
| Generated media | uuid and type | An array of type of medias and their ID's. | 
{% /table %}

---

## Session Recommendation

Below is an example of the report and recommendation of each result.

{% code %}
{% tab language="javascript" %}
// Get the report recommendation
reportRecommendation = report.getRecommendation();
// Get the report recommendation value
reportRecommendationValue = reportRecommendation.getValue();

// Get the report recommendation reason
reportRecommendationReason = reportRecommendation.getReason();

//Get the report recommendation recovery suggestion
reportRecommendationRecoverySuggestion = reportRecommendation.getRecoverySuggestion();

reportBreakdown = report.getBreakdown();
// Get result of each sub check from breakdown

reportBreakdown.forEach((breakdown) => {
  // Get the report breakdown sub check
  subcheck = breakdown.getSubCheck();

  // Get the report breakdown result
  result = breakdown.getResult();

  // Get the report breakdown details
  details = breakdown.getDetails();
});
{% /tab %}
{% tab language="java" %}
// Get the report recommendation
RecommendationResponse reportRecommendation = report.getRecommendation();

// Get the report recommendation value
String reportRecommendationValue = reportRecommendation.getValue();

// Get the report recommendation reason
String reportRecommendationReason = reportRecommendation.getReason();

// Get the report recommendation recovery suggestion
String reportRecommendationRecoverySuggestion = reportRecommendation.getRecoverySuggestion();

List<? extends BreakdownResponse> reportBreakdown = report.getBreakdown();

// Get result of each sub check from breakdown
for (BreakdownResponse breakdown : reportBreakdown) {
    // Get the report breakdown sub check
    String subcheck = breakdown.getSubCheck();
    
    // Get the report breakdown result
    String result = breakdown.getResult();
    
    // Get the report breakdown details
    List<? extends DetailsResponse> details = breakdown.getDetails();
}
{% /tab %}
{% tab language="php" %}
<?php
// Get the report recommendation
$reportRecommendation = $report->getRecommendation();
// Get the report recommendation value
$reportRecommendationValue = $reportRecommendation->getValue();

// Get the report recommendation reason
$reportRecommendationReason = $reportRecommendation->getReason();

//Get the report recommendation recovery suggestion
$reportRecommendationRecoverySuggestion = $reportRecommendation->getRecoverySuggestion();

$reportBreakdown = $report->getBreakdown();
// Get result of each sub check from breakdown
foreach ($reportBreakdown as $breakdown) {

    // Get the report breakdown sub check
    $subcheck = $breakdown->getSubCheck();
  
    // Get the report breakdown result
    $result = $breakdown->getResult();
  
    // Get the report breakdown details
    $details = $breakdown->getDetails();
{% /tab %}
{% tab language="python" %}
# Returns report recommendation
report_recommendation = report.recommendation

# Returns report recommendation value
report_recommendation_value = report_recommendation.value

# Returns report recommendation reason
report_recommendation_reason = report_recommendation.reason

# Returns report recommendation recovery suggestion
report_recommendation_recovery_suggestion = report_recommendation.recovery_suggestion

# Returns report breakdown
report_breakdown = report.breakdown

# Return result of each sub check from breakdown
for breakdown in report_breakdown:
    
    # Returns report breakdown sub check
    subcheck = breakdown.sub_check

    # Returns report breakdown result
    result = breakdown.result

    # Returns report breakdown details
    details = breakdown.details
{% /tab %}
{% tab language="csharp" %}
// Returns the report recommendation
RecommendationResponse reportRecommendation = report.Recommendation;

// Returns the report recommendation value
String reportRecommendationValue = reportRecommendation.Value;

// Returns the report recommendation reason
String reportRecommendationReason = reportRecommendation.Reason;

// Returns the report recommendation recovery suggestion
String reportRecommendationRecoverySuggestion = reportRecommendation.RecoverySuggestion;

List <BreakdownResponse> reportBreakdown = report.Breakdown;

// Returns result of each sub check from breakdown
foreach (BreakdownResponse breakdown in reportBreakdown)
{
    // Returns the report breakdown sub check
    String subcheck = breakdown.SubCheck;

    // Returns the report breakdown result
    String result = breakdown.Result;

    // Returns the report breakdown details
    List <DetailsResponse> details = breakdown.Details;
}
{% /tab %}
{% /code %}

{% table %}
| Object | Response | Description | 
| ---- | ---- | ---- | 
| Report recommendation | N/A | A recommendation value, and recovery suggestion | 
| Report recommendation value | e.g. REJECT | Returns only the recommendation value | 
| Report recommendation reason | e.g. PHOTO_TOO_BLURRY | Returns only the reason of the value. If approved the value will be null. | 
| Report recommendation recovery suggestion | N/A | Returns only the recovery suggestion. If approved the value will be null. | 
| Report breakdown | N/A | A breakdown report on the session that has been completed including, sub-checks, results and details. | 
| Report breakdown sub check | e.g. data_in_correct_position | The sub-check completed | 
| Report breakdown result | e.g PASS | The result of the sub check completed | 
| Report breakdown details | N/A | Extra information on the check if required. | 
{% /table %}

---