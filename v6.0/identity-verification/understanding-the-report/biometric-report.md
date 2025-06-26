---
type: page
title: Biometric report
listed: false
slug: biometric-report
description: 
index_title: Biometric report
hidden: 
keywords: 
tags: 
---

## Liveness report

Liveness checks can sometimes be difficult for users to perform correctly, as they need to position themselves in front of the camera and move in a particular way. For this reason, you can configure an Identity verification session to allow a limited number of retries before rejection. Each attempt will generate a new check in the response.

{% table %}
| Response | Description | 
| ---- | ---- | 
| APPROVE | The user has passed the liveness test | 
| REJECT | Our result suggests it's likely that the user is an automated program (a 'bot'), or somebody holding a photograph, mask or other disguise in front of the camera. Ensure you have reviewed the document response, if this is approved you can ask your users to try a new session. | 
{% /table %}

As part of the liveness check, Yoti performs the following sub check on the face capture explained below which will either PASS or FAIL.

{% table %}
| Sub check | Description | 
| ---- | ---- | 
| liveness_auth | If FAIL, the check will recommend REJECT with no reason given. | 
{% /table %}

---

## Face match report

Yoti performs an automated initial check to confirm the user's face matches the face on their ID document. If the automated check is not successful, at session creation there is an option to fallback to manual face match whereby the image is reviewed by one of our processing experts. The face match check will give a recommendation based on these as either APPROVE or REJECT.

If an automated AI face match is performed, a pass/fail result is returned, along with a confidence score (between 0 and 1) depending on how successful the match is.

{% table %}
| Recommendation | Explained | 
| ---- | ---- | 
| APPROVE | The facial image of the user captured on camera matches the face on their submitted document. | 
| REJECT | The facial image of the user captured on camera does not match the face on their submitted document. | 
| NOT_AVAILABLE | The facial image of the user captured on camera was unable to complete the match on the face on their submitted document.\n\nThis will only be returned for a manual check. | 
{% /table %}

For the list of recommendation suggestions please see below which will allow you to provide to give the user a correction attempt.

### Reject result

{% table %}
| Yoti reason | Description | Recovery suggestion | 
| ---- | ---- | ---- | 
| FACE_NOT_GENUINE | The user may be trying to spoof the face match. | You may want to flag this user. | 
| LARGE_AGE_GAP | The user looks to be a considerably different age compared with what's stated on their ID document. | You may want to flag this user. | 
| PHOTO_OF_MASK | The user is wearing a mask. | You may want to flag this user. | 
| PHOTO_OF_PHOTO | The image of the user is a photo. Not the user doing the liveness. | You may want to explain to the user how to complete the process. | 
| DIFFERENT_PERSON | Different person is detected from ID. | You may want to flag this user. | 
{% /table %}

### Not available result

{% table %}
| Yoti Response | Description | Recovery suggestion | 
| ---- | ---- | ---- | 
| PHOTO_OVEREXPOSED | The photo is overexposed. | Ask the user to try again ensuring no excessive light is on the document. | 
| PHOTO_TOO_DARK | There is not enough ambient light. The user needs to move into a lighter frame. | Ask the user to try again and move into a lighter area. | 
| PHOTO_TOO_BLURRY | The camera was not held steady or the lens is dirty. | Ask the user to try again with the ID document on a flat surface, or to use their mobile. | 
| FACE_NOT_FOUND | There was no face detected in the face match process. | Ask the user to try again. | 
| GLARE_OBSTRUCTION | There is a glare on the image of the user's face. | Ask the user to try again. | 
| OBJECT_OBSTRUCTION | There is an object in the way, for example the user's thumb is on their ID. | Ask the user to try again and ensure you can see the ID fully. | 
| DOCUMENT_NOT_FOUND | No document was detected to compare the face match too. | Ask the user to try again and to upload a document. | 
| PARTIAL_PHOTO | Only part of the photo was shown. | Ask the user to try again and ensure you can see the ID fully. | 
| FACE_PHOTO_LOW_RESOLUTION | The image resolution of the photo is too low. Ask the user to try on their mobile. | Ask the user to try again and to use their mobile. | 
| MISUSE | The photo is misused. | Ask the user to try again with a different document. | 
| INVALID | The photo is invalid. | Ask the user to try again with a different document. | 
{% /table %}