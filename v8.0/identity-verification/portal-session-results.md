---
type: page
title: Session results
listed: true
slug: portal-session-results
description: 
index_title: Session results
hidden: 
keywords: 
tags: 
---

Once the session has been started, the state of this session will be 'in progress'. The state will be shown at the top banner. Below are the different states:

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/slz7dofehnsmf2yjqhzn/1623412501.png" caption="Session details" mode="responsive" height="700" width="2100" %}
{% /image %}

{% table %}
| Value | Description | 
| ---- | ---- | 
| IN PROGRESS | Yoti is still working on tasks and checks for the user's ID. | 
| COMPLETED | Yoti has completed the checks and tasks. | 
| EXPIRED | Yoti could not complete the checks and tasks. | 
{% /table %}

Yoti will respond with a recommendation for each check. For example:

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/ikqjsvkwa3xayh60xoif/1623412583.png" caption="Session results" mode="responsive" height="648" width="2094" %}
{% /image %}

To understand responses and reports from Identity verification, please head over to the appropriate section:

- [Document report](https://developers.yoti.com/identity-verification/document)
- [Address report](https://developers.yoti.com/identity-verification/address)
- [AML report](https://developers.yoti.com/identity-verification/aml)
- [Biometric report](https://developers.yoti.com/identity-verification/liveness)

---

## Session details

This is a log of the session. Yoti will provide details on:

- Name and email address of the user the session was sent to.
- A log of who created the session and when. 
- The Session ID. This is a unique identifier per session.
- Tracking ID. This is a unique identifier per user.

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/tl32tvmi4uiv96ubkpwj/1623412643.png" caption="Session details" mode="responsive" height="522" width="2100" %}
{% /image %}

---

## Document report

If text data extraction task is selected, in your results you will see all the media and document details in the Text extraction tab. 

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/piabhb3ktzdptxmpxofh/1623411742.png" caption="Document check result" mode="responsive" height="720" width="1474" %}
{% /image %}

You can click the left and right arrows to see front and back of the document. You should see 3 images of the front and 3 images of the back. 

If the user uploaded their image rather than taking a photo, you will see one image only. 

Other functionality is:

- Flip photo
- Zoom in or out
- Make the photo brighter or darker
- Delete the image.

If we couldn't extract the data you will see the following:-

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/ypo2om8rsv5dmwiiiz2l/1623411963.png" caption="Document check result" mode="responsive" height="814" width="1958" %}
{% /image %}

Yoti suggests you ask the user to try again here. 

If the user has been unsuccessful in their session and Yoti was unable to complete a check, you will see the following response for a document:

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/ut74wo8stcsp7t83kidd/1623412080.png" caption="Document check result -&gt; Not available" mode="responsive" height="482" width="1192" %}
{% /image %}

If the user has been unsuccessful in their session and Yoti has rejected the check, you will see the following response for a document:

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/trimyzlzwp4ca4x2hvjd/1623412220.png" caption="Document check result -&gt; Rejected" mode="responsive" height="936" width="2234" %}
{% /image %}

If you have more than one document and you complete a document comparison check, the first document will be compared with the rest. An example result is shown below:

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/jhze1xqrinbgmpul9gyc/1623417224.png" caption="Example of document comparison check" mode="300" height="428" width="548" %}
{% /image %}

A full list of the rejection reasons are located at [Document report](/yoti-developer-documentation/v6.0/identity-verification/document) with recommended next steps. 

---

## Address report

A **successful** text data extraction of the name, address and date of birth. If we are unable to extract the data the check will not be performed. A new bar will appear with the address check results, an example shown below is if we have responded back with CONSIDER.

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/htisxyp5cyjoezkwba7v/1623417077.png" caption="Address check result -&gt; Consider" mode="responsive" height="638" width="2778" %}
{% /image %}

A full list of the rejection reasons are located at [Address report](/yoti-developer-documentation/identity-verification/address) with recommended next steps.

---

## AML report

A **successful** text data extraction of the name, iso country code and date of birth. If we are unable to extract the data the check will not be performed. A new bar will appear with the address check results, an example shown below is if we have responded back with CONSIDER.

Yoti will respond back with the results of the AML check with a comply advantage report link and results from the search. Yoti will show any matches. 

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/op0sl4ztcr29lqdsb7qo/1633163950.png" mode="responsive" height="587" width="1403" %}
{% /image %}

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/ndrrhjkk9ecsjib47ofn/1633163998.png" mode="responsive" height="685" width="1406" %}
{% /image %}

A full list of the rejection reasons are located at [AML report](/yoti-developer-documentation/identity-verification/aml) with recommended next steps.

---

## Biometric report

If liveness has been completed you will see 3 images of the user and a recommendation. 

The more liveness attempts the user tries the more images and checks you will see. Be sure to take the latest check as the final result.

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/m8uqvh6cq362dfb1eyti/1623412351.png" mode="responsive" height="570" width="2026" %}
{% /image %}

A full list of the rejection reasons are located at [Biometric report](/yoti-developer-documentation/identity-verification/liveness) with recommended next steps. 

---

## DBS/RTW Report

If a pre-configured DBS or RTW check has been configured a new bar will appear in the portal results. Detailing if the user has met the requirements of this check, and outlining the level of assurance the user has met.

{% image url="https://uploads.developerhub.io/prod/kvAX/jllxwf9tzhfjinx84e8vtpjk86igaez1y8e7w8c5humzj12vcqnugg7o2sz7wpk6.png" mode="responsive" height="652" width="1201" %}
{% /image %}

---

## Overall recommendation

The above will explain the check recommendations that Yoti returns. It is at your discretion if you want to overall APPROVE / REJECT a user. 

Hence at the top of each session there will be an option for you to make a decision on the client session once the session has been completed.

{% image url="https://image-archive.developerhub.io/image/upload/71142/xdzq5omtdprkvblwd4ft/1603128781.png" caption="Session &gt; Decision" mode="300" height="622" width="1480" %}
{% /image %}

This session will be overall marked with your decision and cannot be changed.

---

## Download Report

Once the session and all the checks have been completed, you can download a report version of the report. 

- Click on the session you wish to download.
- Click the three dots next to the session name:

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/fvi2ncki9vm9xy5s2g25/1623769481.png" caption="Session details &gt; 3 dots" mode="responsive" height="828" width="1656" %}
{% /image %}

- Click "Download PDF".

De-select if you do not want image or the users data. 

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/egtezd66o1jtuduq9ue0/1623769563.png" caption="Session details &gt; 3 dots &gt; Download PDF" mode="600" height="600" width="1020" %}
{% /image %}

- Press "GENERATE."
- Once completed press "DOWNLOAD."

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/t8fttgyfgvywsotonvsc/1623769638.png" caption="Session details &gt; 3 dots &gt; Download PDF&gt; Download" mode="600" height="524" width="990" %}
{% /image %}

To see PDF report please click [here](https://www.yoti.com/wp-content/uploads/IDV-portal.pdf) or see below:

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/tix1hdgx9uviduzzetm8/1623770552.png" caption="Report page 1" mode="responsive" height="1660" width="1150" %}
{% /image %}

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/sqkxop71uxtkzjswpjzq/1623770629.png" caption="Report page 2" mode="responsive" height="1664" width="1164" %}
{% /image %}

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/enf0fqqacf7ttcj1cqcn/1623770679.png" caption="Report page 3" mode="responsive" height="1648" width="1148" %}
{% /image %}

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/wu2edlm461xakp9jpbhj/1623770696.png" caption="Report page 4" mode="responsive" height="1654" width="1160" %}
{% /image %}

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/vsgn4k9n1zhc9oqsh5vw/1623770795.png" caption="Report page 5" mode="responsive" height="1646" width="1138" %}
{% /image %}