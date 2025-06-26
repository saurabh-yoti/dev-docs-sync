---
type: page
title: Retrieve user data
listed: true
slug: retrieve-userdata
description: 
index_title: Retrieve user data
hidden: 
keywords: 
tags: 
---

To view all submitted user information related to a session use the **resources** container.

{% code %}
{% tab language="javascript" %}
idvClient.getSession(sessionId).then(session => {
    // Returns all resources in the session
    const resources = session.getResources();

    // Returns a collection of ID Documents
    const idDocuments = resources.getIdDocuments();

    idDocuments.map((idDocument) => {

        // Gets the UUID of the document resource
        const id = idDocument.getId();

        // Returns the ID Document Type
        const documentType = idDocument.getDocumentType();

        // Returns the ID Document country
        const issuingCountry = idDocument.getIssuingCountry();

        // Returns pages of an ID Document
        const pages = idDocument.getPages();
        // Get pages media ids
        const pageMediaIds = pages.map(page => {
            if (page.getMedia() && page.getMedia().getId()) {
                return page.getMedia().getId();
            }
            return null;
        });
      
        //return document id photo media id
        const documentPhoto = idDocument.getDocumentIdPhoto().getMedia().getId();

        // Returns document fields object
        const documentFields = idDocument.getDocumentFields();
        // Get document fields media id
        let documentFieldsMediaId = null;
        if (documentFields) {
            documentFieldsMediaId = documentFields.getMedia().getId();
        }
    });

    // Returns a collection of liveness capture resources
    const livenessCapture = resources.getLivenessCapture();
    const zoomLiveness = resources.getZoomLivenessResources();
    
}).catch(error => {
    console.log(error)
    // handle error
})
{% /tab %}
{% tab language="java" %}
GetSessionResult sessionResult = docScanClient.getSession(sessionId);

// Returns all resources in the session
ResourceContainer resources = sessionResult.getResources();

// Returns a collection of ID Documents
List<? extends IdDocumentResourceResponse> idDocuments = resources.getIdDocuments();

for (IdDocumentResourceResponse idDocument: idDocuments) {

    // Gets the UUID of the document resource
    String id = idDocument.getId();

    // Returns the ID Document Type
    String documentType = idDocument.getDocumentType();

    // Returns the ID Document country
    String issuingCountry = idDocument.getIssuingCountry();

    // Returns the pages of an ID Document
    List<? extends PageResponse> pages = idDocument.getPages();
    // Get the page media ids
    ArrayList<String> pageMediaIds = new ArrayList<>();
    for (PageResponse page: pages) {
        if (page.getMedia() != null && page.getMedia().getId() != null) {
            pageMediaIds.add(page.getMedia().getId());
        }
    }
  
    // Get Id docmunent photo media id
    String documentPhotoMediaId = idDocument.getDocumentIdPhoto().getMedia().getId();
  
    // Returns document fields object
    DocumentFieldsResponse documentFields = idDocument.getDocumentFields();
    // Get document fields media id
    String documentFieldsMediaId = null;
    if (documentFields != null) {
        documentFieldsMediaId = documentFields.getMedia().getId();
    }
    
}

// Returns a collection of liveness capture resources
List<? extends LivenessResourceResponse> livenessCapture = resources.getLivenessCapture();
List<? extends ZoomLivenessResourceResponse> zoomLiveness = resources.getZoomLivenessResources();

// Returns a collection of face capture resources
List<? extends FaceCaptureResourceResponse> faceCapture = resources.getFaceCapture();
{% /tab %}
{% tab language="php" %}
<?php
$sessionResult = $docScanClient->getSession($sessionId);

// Returns all resources in the session
$resources = $sessionResult->getResources();

// Returns a collection of ID Documents
$idDocuments = $resources->getIdDocuments();

foreach ($idDocuments as $idDocument) {
    
    // Gets the UUID of the document resource
    $id = $idDocument->getId();

    // Returns the ID Document Type
    $documentType = $idDocument->getDocumentType();

    // Returns the ID Document country
    $issuingCountry = $idDocument->getIssuingCountry();

    // Returns the pages of an ID Document
    $pages = $idDocument->getPages();
    // Get pages media ids
    $pageMediaIds = [];
    foreach ($pages as $page) {
        if ($page->getMedia() && $page->getMedia()->getId()) {
            array_push($pageMediaIds, $page->getMedia()->getId());
        }
    }
  
    // Get Id document photo media id
    $documentPhotoId = $idDocument->getDocumentIdPhoto()->getMedia()->getId();
    
    // Returns document fields object
    $documentFields = $idDocument->getDocumentFields();
    // Get document fields media id
    $documentFieldsMediaId;
    if ($documentFields) {
        $documentFieldsMediaId = $documentFields->getMedia()->getId();
    }
}

// Returns a collection of liveness capture resources
$livenessCapture = $resources->getLivenessCapture();
$staticLiveness = $resources->getStaticLivenessResources();
$zoomLiveness = $resources->getZoomLivenessResources();

// Returns a collection of face capture resources
$faceCapture = $resources->getFaceCapture();
{% /tab %}
{% tab language="python" %}
session_result = doc_scan_client.get_session(session_id)

# Returns all resources in the session
resources = session_result.resources

# Returns a collection of ID Documents
id_documents = resources.id_documents

for id_document in id_documents:
    
    # Gets the UUID of the document resource
    id = id_document.id

    # Returns the ID Document Type
    document_type = id_document.document_type

    # Returns the ID Document country
    issuing_country = id_document.issuing_country

    # Returns the pages of an ID Document
    pages = id_document.pages
    # Get pages media ids
    page_media_ids = []
    for page in pages:
        if page.media and page.media.id:
            page_media_ids.append(page.media.id)
            
    # Get Id document photo media id
    document_photo_media_id = id_document.document_photo.media.id
    
    # Returns document fields object
    document_fields = id_document.document_fields
    # Get document fields media id
    document_fields_media_id = None
    if document_fields:
        document_fields_media_id = document_fields.media.id

# Returns a collection of liveness capture resources
liveness_capture = resources.liveness_capture
zoom_liveness = resources.zoom_liveness_resources
{% /tab %}
{% tab language="csharp" %}
GetSessionResult sessionResult = docScanClient.GetSession(sessionId);

// Returns all resources in the session
ResourceContainer resources = sessionResult.Resources;

// Returns a collection of ID Documents
List<IdDocumentResourceResponse> idDocuments = resources.IdDocuments;

foreach (IdDocumentResourceResponse idDocument in idDocuments)
{
    // Gets the UUID of the document resource
    string id = idDocument.Id;

    // Returns the ID Document Type
    string documentType = idDocument.DocumentType;

    // Returns the ID Document country
    string issuingCountry = idDocument.IssuingCountry;

    // Returns the pages of an ID Document
    List<PageResponse> pages = idDocument.Pages;
    // Get the page media ids
    ArrayList pageMediaIds = new ArrayList();
    foreach (PageResponse page in pages)
    {
        if (page.Media != null && page.Media.Id != null)
        {
            pageMediaIds.Add(page.Media.Id);
        }
    }
  
    // Get Id document photo media id
    string documentPhotoMediaId = idDocument.DocumentPhoto.Media.Id;

    // Returns document fields object
    DocumentFieldsResponse documentFields = idDocument.DocumentFields;
    //Get document fields media id
    string documentFieldsMediaId = null;
    if (documentFields != null)
    {
        documentFieldsMediaId = documentFields.Media.Id;
    }
}

// Returns a collection of liveness capture resources
List<LivenessResourceResponse> livenessCapture = resources.LivenessCapture;
List<ZoomLivenessResourceResponse> zoomLivenesses = resources.ZoomLivenessResources;

// Returns a collection of face capture resources
List<FaceCaptureResourceResponse> faceCapture = resources.FaceCapture;
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
    "supplementary_documents": [
      {
        "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
        "source": {
          "type": "END_USER"
        },
        "document_type": "UTILITY_BILL",
        "issuing_country": "string",
        "file": {
          "media": {
            "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "type": "IMAGE",
            "created": "2021-06-11T11:39:24Z",
            "last_updated": "2021-06-11T11:39:24Z"
          }
        },
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
            "type": "SUPPLEMENTARY_DOCUMENT_TEXT_DATA_EXTRACTION"
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

---

## Retrieve user information

This is the full JSON version of the user's profile using document fields. An explanation of the address format can be found in this section: [auto$](/digital-id/yoti-attributes).

The document_fields media id should be used when an OCR or manual data entry result is successful. The media ID will be updated to the latest result, if you get OCR data back it will relate to the server side extraction. If the data entry goes for a manual check and data is extracted successfully the media ID will also be updated accordingly and point to generated media from a text data check. 

The absence of the document fields object would indicate that data did not get extracted from the ID document.

{% code %}
{% tab language="javascript" %}
idvClient.getMediaContent(sessionId, documentFieldsMediaId).then(media => {
  	const buffer = media.getContent();
    const jsonData = JSON.parse(buffer);
    // handle jsonData here
}).catch(error => {
    // handle error
})
{% /tab %}
{% tab language="java" %}
Media media = docScanClient.getMediaContent(sessionId, documentFieldsMediaId);
{% /tab %}
{% tab language="php" %}
<?php
$media = $docScanClient->getMediaContent($sessionId, $documentFieldsMediaId);
$data = json_decode($media->getContent());
{% /tab %}
{% tab language="python" %}
media = doc_scan_client.get_media_content(session_id, documentFieldsMediaId)
data = json.loads(media.content)
{% /tab %}
{% tab language="csharp" %}
MediaValue media = docScanClient.GetMediaContent(sessionId, documentFieldsMediaId);
{% /tab %}
{% /code %}

#### Example Extractions

{% code %}
{% tab language="json" title="GBR Passport" %}
{
    "full_name": "ANGELA ZOE UK SPECIMEN",
    "date_of_birth": "1988-12-04",
    "nationality": "GBR",
    "given_names": "ANGELA ZOE",
    "family_name": "UK SPECIMEN",
    "place_of_birth": "CROYDON",
    "gender": "FEMALE",
    "document_type": "PASSPORT",
    "issuing_country": "GBR",
    "document_number": "533028754",
    "expiration_date": "2025-09-28",
    "date_of_issue": "2015-09-28",
    "issuing_authority": "HMPO",
    "mrz": {
        "type": 2,
        "line1": "P<GBRUK<SPECIMEN<<ANGELA<ZOE<<<<<<<<<<<<<<<<",
        "line2": "5330287549GBR8812049F2509286<<<<<<<<<<<<<<02"
    },
    "document_template": {
        "front_page_name": "United Kingdom - ePassport (2015)"
    }
}
{% /tab %}
{% tab language="json" title="GBR DL" %}
{
    "full_name": "STEVONNE ANNA MITCHELITE",
    "date_of_birth": "1992-02-22",
    "given_names": "STEVONNE ANNA",
    "family_name": "MITCHELITE",
    "place_of_birth": "UNITED KINGDOM",
    "gender": "FEMALE",
    "structured_postal_address": {
        "address_format": 1,
        "building_number": "244",
        "address_line1": "244 MANNER ROAD",
        "address_line2": "SONYMANE",
        "address_line3": "SWANSEA",
        "town_city": "SWANSEA",
        "postal_code": "SA8 8JA",
        "country_iso": "GBR",
        "country": "United Kingdom",
        "formatted_address": "244 MANNER ROAD, SONYMANE, SWANSEA,\nSA8 8JA"
    },
    "document_type": "DRIVING_LICENCE",
    "issuing_country": "GBR",
    "document_number": "MITCH952222SA8KK22",
    "expiration_date": "2028-11-01",
    "date_of_issue": "2021-11-02",
    "issuing_authority": "DVLA",
    "driving_licence_class": "AM/A/B1/B//p/q",
    "driving_licence_restriction_code": "115",
    "document_template": {
        "front_page_name": "United Kingdom - Driving License (2021) #2",
        "back_page_name": "United Kingdom - Driving License (2014-2021) Side B"
    }
}
{% /tab %}
{% tab language="json" title="GBR Residence Permit" %}
{
  "full_name": "TECH REFRESH ICTHREEMALE",
  "date_of_birth": "1990-08-01",
  "nationality": "KEN",
  "given_names": "TECH REFRESH",
  "family_name": "ICTHREEMALE",
  "place_of_birth": "NAIROBI",
  "gender": "MALE",
  "document_type": "RESIDENCE_PERMIT",
  "issuing_country": "GBR",
  "document_number": "RF9082242",
  "expiration_date": "2015-11-11",
  "date_of_issue": "2015-05-19",
  "mrz": {
    "type": 1,
    "line1": "IRGBRRF90822427<<<<<<<<<<<<<<<",
    "line2": "9008010M1511114KEN<<<<<<<<<<<8",
    "line3": "ICTHREEMALE<<TECH<REFRESH<<<<<"
  },
  "place_of_issue": "UK"
}
{% /tab %}
{% tab language="json" title="DEU DL" %}
{
    "full_name": "Erika - Mustermann",
    "date_of_birth": "1964-08-12",
    "given_names": "Erika -",
    "family_name": "Mustermann",
    "place_of_birth": "Berlin",
    "document_type": "DRIVING_LICENCE",
    "issuing_country": "DEU",
    "document_number": "Z021AB37X13",
    "expiration_date": "2036-03-19",
    "date_of_issue": "2021-03-20",
    "place_of_issue": "Landratsamt\nMu sterhausen amSee"
}
{% /tab %}
{% tab language="json" title="ESP Passport" %}
{
    "full_name": "CARMEN ESPANOLA ESPANOLA",
    "date_of_birth": "1980-01-01",
    "nationality": "ESP",
    "given_names": "CARMEN",
    "family_name": "ESPANOLA ESPANOLA",
    "place_of_birth": "MADRID (MADRID)",
    "gender": "FEMALE",
    "document_type": "PASSPORT",
    "issuing_country": "ESP",
    "document_number": "ZAB000254",
    "expiration_date": "2025-01-01",
    "date_of_issue": "2015-01-01",
    "issuing_authority": "DGP -28391A6PK",
    "mrz": {
        "type": 2,
        "line1": "P<ESPESPANOLA<ESPANOLA<<CARMEN<<<<<<<<<<<<<<",
        "line2": "ZAB0002549ESP8001014F2501017A9999999900<<<44"
    },
    "personal_identification_number": "A9999999900"
}
{% /tab %}
{% /code %}

---

## Retrieve supplementary documents

Supplementary documents will be similarly available as part of the JSON if they have been successfully parsed by either OCR or manual data entry. When retrieving supplementary documents, any document images will appear as 'pages' objects in the JSON whilst uploaded pdfs will be 'file' objects.

{% code %}
{% tab language="javascript" %}
idvClient.getMediaContent(sessionId, documentFieldsMediaId).then(media => {
  	const buffer = media.getContent();
    const jsonData = JSON.parse(buffer);
    // handle jsonData here
}).catch(error => {
    // handle error
})
{% /tab %}
{% tab language="java" %}
Media media = docScanClient.getMediaContent(sessionId, documentFieldsMediaId);
{% /tab %}
{% tab language="php" %}
<?php
$media = $docScanClient->getMediaContent($sessionId, $documentFieldsMediaId);
$data = json_decode($media->getContent());
{% /tab %}
{% tab language="python" %}
media = doc_scan_client.get_media_content(session_id, documentFieldsMediaId)
data = json.loads(media.content)
{% /tab %}
{% tab language="csharp" %}
MediaValue media = docScanClient.GetMediaContent(sessionId, documentFieldsMediaId);
{% /tab %}
{% /code %}

If you have enabled non latin characters Yoti will do its best to provide the latin characters where possible.

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Jump to..
    </div>
    <div class="alert-text">
       Get a deeper dive on the user information, go to Understanding the report.
    </div>
    <div class="alert-links"> 

        <a href="https://developers.yoti.com/identity-verification/understanding-the-report">Understanding the report</a>
        
   </div>
</div>
{% /html %}