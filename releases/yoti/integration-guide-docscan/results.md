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

To retrieve the results of a session Yoti will provide an extensive report and recommendation via the SDK as long as your session ttl is active. If you wish to be notified on the progress of the session please use **notifications**. 

This sections explains how to:

- Retrieve the [results of the session](https://developers.yoti.com/yoti/results#result-of-the-session)
- Retrieve ID [document images and user information](https://developers.yoti.com/yoti/results#retrieve-id-document-information)
- Display [checks and results](https://developers.yoti.com/yoti/results#results-of-checks) associated to an ID Document in a session
- [Retrieve captured user images](https://developers.yoti.com/yoti/results#retrieve-images)
- [Delete all sessions](https://developers.yoti.com/yoti/results#delete-session) details or media

The structure of the full response is shown below:

{% image url="https://image-archive.developerhub.io/image/upload/30910/uyfa3ajl82gqkoeklkzk/1595537494.jpg" caption="Results hierarchy" mode="full" height="2695" width="3516" %}
{% /image %}

Yoti will provide you a recommendation for each check. Please read this section and then head over to [understanding the report](https://developers.yoti.com/yoti/understanding-the-report) for more information.

---

## Result of the session

Session retrieval requires a session ID, this is generated from the create a session endpoint.  Below is a basic example of what retrieving a session looks like:

{% code %}
{% tab language="javascript" %}
// Returns a session result
docScanClient.getSession(sessionId).then(session => {
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
{% /tab %}
{% /code %}

Common values inside of the session result are:

{% table %}
| Value | Description | 
| ---- | ---- | 
| State | The current state of the session. It provides the overall state of the session. \n\nYou can search through session results prior to this being completed, but some checks may not have been processed yet. | 
| Resources | A container of all ID documents and liveness captures for this session. | 
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
              <a href="https://developers.yoti.com/yoti/generating-a-session">Create a session</a>

        <a href="https://developers.yoti.com/yoti/understanding-the-report#result-of-the-session">Understanding the report</a>
        
   </div>
</div>
{% /html %}

---

## Retrieve ID document information

To view all submitted user information related to a session use the **resources** container. Below is an example of document authenticity:

{% code %}
{% tab language="javascript" %}
docScanClient.getSession(sessionId).then(session => {
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
$zoomLiveness = $resources->getZoomLivenessResources();
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
{% /tab %}
{% /code %}

### Retrieve user information

This is the full JSON version of the users profile using document fields. An explanation of the address format can be found [here](/yoti/knowledge-base-hub#address-attributes).

{% code %}
{% tab language="javascript" %}
docScanClient.getMediaContent(sessionId, documentFieldsMediaId).then(media => {
    const content = media.getContent();
    const buffer = content.toBuffer();
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

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Jump to..
    </div>
    <div class="alert-text">
       Get a deeper dive on the user information, go to Understanding the report.
    </div>
    <div class="alert-links"> 

        <a href="https://developers.yoti.com/yoti/understanding-the-report#retrieve-user-information">Understanding the report</a>
        
   </div>
</div>
{% /html %}

---

## Results of checks

A basic example of how to get the check type, check [recommendation](https://developers.yoti.com/yoti/understanding-the-report#session-recommendation) value and reason is shown below. A recommendation reason will only be provided if the value isn't 'APPROVE'. The recommended approach to process a session is to check if each check value is APPROVE. For more information on each check and the recommendations please head over to 'Understanding the report'.

- [Document authenticity report](https://developers.yoti.com/yoti/understanding-the-report#document-authenticity-report)
- [Liveness report](https://developers.yoti.com/yoti/understanding-the-report#liveness-report)
- [Face match report](https://developers.yoti.com/yoti/understanding-the-report#face-match-report)
- [Text data extraction report](https://developers.yoti.com/yoti/understanding-the-report#text-extraction-report)

We will use the **check container** to iterate through all of the checks that have been completed as part of the session. The checks object will only contain information once the user has completed all events (apart from Liveness) inside of the iFrame. 

**Liveness**

The liveness response is immediate as it uses automation software. The user may attempt multiple attempts of liveness. It's possible that some of these attempts were rejected.

**Multiple documents**

If you are collecting multiple documents from your users please note each check contains a resourcesUsed object which will identify which check is related to which ID document instead of the resources container. 

{% code %}
{% tab language="javascript" %}
docScanClient.getSession(sessionId).then(session => {
    // Returns a collection of checks
    const checks = session.getChecks();
    
    checks.map(check => {

        // Returns the type of check
        const type = check.getType();

        // Returns the state of the check
        const state = check.getState();

        // Returns an array of resources used in this check
        const resourcesUsed = check.getResourcesUsed();

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
    
    // Returns an array of resources used in this check
    List<String> resourcesUsed = check.getResourcesUsed();
    
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
{% /code %}

---

## Retrieve Images

In order to retrieve document images from the **resources** container we'll want to look for the relevant media ID inside of the id document pages.

For security reasons, Yoti does not include personally identifiable information within the standard response to a session retrieval request. Yoti will provide ID's to media associated with the session, which can be stored and can be retrieved separately.

{% code %}
{% tab language="javascript" %}
docScanClient.getMediaContent(sessionId, pageMediaId).then(media => {
    const content = media.getContent();
    const buffer = content.toBuffer();
    const base64Content = media.getBase64Content();
    const mimeType = media.getMimeType();
    // handle base64content or buffer
}).catch(error => {
    console.log(error)
    // handle error
})
{% /tab %}
{% tab language="java" %}
Media media = docScanClient.getMediaContent(sessionId, pageMediaId);
{% /tab %}
{% tab language="php" %}
<?php
$media = $docScanClient->getMediaContent($sessionId, $pageMediaId);
$base64Content = $media->getBase64Content();
$contentType = $media->getMimeType();
{% /tab %}
{% tab language="python" %}
media = doc_scan_client.get_media_content(session_id, pageMediaId)
base64_content = media.base64_content
content_type = media.mime_type
{% /tab %}
{% tab language="csharp" %}
MediaValue media = docScanClient.GetMediaContent(sessionId, pageMediaId);
{% /tab %}
{% /code %}

---

## Delete Session

It is possible to delete a session or image (media) before the defined retention period (ttl) is over. This can only be done **once the session is completed.**

Deleting the session will also delete all media from that session. Deleting a media object will delete only that specific object, leaving the rest of the session untouched.

{% code %}
{% tab language="javascript" %}
// Deleting the session
docScanClient.deleteSession(sessionId).then(() => {
  // Session has been deleted
}).catch(error => {
  // Error occured
})

// Deleting the media
docScanClient.deleteMediaContent(sessionId, mediaId).then(() => {
  // Media has been deleted
}).catch(error => {
  // Error occured
})
{% /tab %}
{% tab language="java" %}
// Deleting the session
docScanClient.deleteSession(sessionId);

// Deleting the media
docScanClient.deleteMediaContent(sessionId, mediaId);
{% /tab %}
{% tab language="php" %}
<?php
// Deleting the session
$docScanClient->deleteSession($sessionId);

// Deleting the media
$docScanClient->deleteMediaContent($sessionId, $mediaId);
{% /tab %}
{% tab language="python" %}
# Deleting the session
doc_scan_client->delete_session(session_id);

# Deleting the media
doc_scan_client->delete_media_content(session_id, media_id);
{% /tab %}
{% tab language="csharp" %}
// Deleting the session
docScanClient.DeleteSession(sessionId);

// Deleting the media
docScanClient.DeleteMediaContent(sessionId, mediaId);
{% /tab %}
{% /code %}