---
type: page
title: Yoti Doc Scan Integration
listed: true
slug: yoti-doc-scan-integration
description: 
index_title: Yoti Doc Scan Integration
hidden: 
keywords: 
tags: 
---

Yoti is an identity checking platform that allows organisations to verify who people are, online and in person. Yoti offers two methods to obtain verified identity attributes from your users. 

1) **The Yoti App integration**, please see [this section](/yoti-app/web-integration) for more details. This requires users to download the Yoti App and scan a QR code integrated on your website once.

2) **The Yoti Doc Scan integration**, allowing the user to take a photo of their ID, we then verify this instantly and prepare a response, which your system can then retrieve on your hosted site.

{% image url="https://image-archive.developerhub.io/image/upload/12868/cb8vus81lr3ebsvvhf1y/1564055850.png" mode="responsive" height="1200" width="1600" %}
{% /image %}

### Yoti App Integration vs Yoti Doc Scan

In order to decide which product is best for you please see the below comparison table:

{% table %}
| Functionality | Yoti App | Yoti Doc | 
| ---- | ---- | ---- | 
| Reusable | YES | NO | 
| Embedded | NO | YES | 
| Time to receive verified details&lt;br&gt; | Instant (if user has Yoti already) | ~5 minutes | 
| Suitable for login authentication&nbsp; | YES | NO | 
| Report with ID security features checks&nbsp; | NO | YES | 
| Business client verifies individual's identity after receiving Yoti checks | NO | YES | 
{% /table %}

If you are unsure on the product to integrate please contact [business@yoti.com](mailto:business@yoti.com). 

---

### Yoti Doc Scan User flow

This document will guide you through the configuration and implementation steps that are necessary in order for your system to be able to retrieve the user's profile and verification status programmatically. 

This solution step by step flow for the user is as follows:

1) The user will be presented with issuing country options and what type of government ID they will send you:

- Passport
- Driving license
- National ID

2) The user's camera will be initiated, the user will take a picture of their identity document (including the back if required). They will have the option to take the photo again if needed. We provide guidelines to the user on how to take the photo appropriately.

4) This will upload to Yoti, if successfully uploaded the user will be redirected to a success screen.

5) Yoti will process the ID and provide an authenticity report for you. It is at your discretion to define what messaging you provide the user.

The flow is illustrated here:

{% video %}
{% /video %}

## Yoti Doc Scan Technical Overview

The following terms are used throughout this documentation and a general description is provided below:

**A session:** represents one end-to-end use of the ID verification service. Each time the ID verification service is initiated a unique session identifier is assigned. All resources, media, tasks and checks belong to a specific session. Data about the session can be retrieved and deleted by the relying party. The session contains the configuration, including the requested checks, tasks and client SDK behaviour, requested by the replying party.

**A resource:** represents an entity that checks and tasks are performed on. For example, a resource could represent an identity document, a face capture, or liveness capture. One or more resources will be required to process a given task or check.

**Resource media:** represents component parts of a resource, usually sensitive information about that resource, and always encrypted with AES-256 encryption. For example, resource media can take the form of images, a video or structured data about a resource.

**Checks:** An action Yoti performs to check an element or elements of a resource. For example, checking document authenticity. See more [here](/yoti-doc-scan/generating-the-session#2-requested-checks-configuration).

**Task:** An action Yoti performs to process the resource or media, for example Text data extraction from an Id document image. These checks can be performed in an automated fashion or manual human intervention or both, depending on the task. See more [here](/yoti-doc-scan/generating-the-session#3-tasks).

A session is always initiated programmatically from the relying party backend to the Yoti API service. The Yoti client is then able to launch, requesting the appropriate configuration from the Yoti API, using the newly created session.

### Technical Diagram

The below diagram details the interaction with the Yoti API, Yoti client, relying party backend and replying party customer client. This describes the API interactions for a web, mobile web and native mobile integration. Exchanges of data will occur securely between the relying party backend, Yoti API and Yoti client.

A session is always initiated programmatically from the relying party backend to the Yoti API service. The Yoti client is then able to launch, requesting the appropriate configuration from the Yoti API, using the newly created session.

{% image url="https://image-archive.developerhub.io/image/upload/12868/ddxuzri4fz7uivsplpxk/1565625363.jpg" mode="600" height="1200" width="1601" %}
{% /image %}

Here are the main client/server interactions for the ID verification flow:

1) Initiate a session with Yoti

2) Yoti will respond with a session ID and authentication token.

3) Launch the Yoti SDK with relevant parameters with the received ID and token.

4) The Yoti SDK and back-end determine what flow is required, based on the session ID.

5) Yoti backend will respond with the desired flow and associated parameters.

6) Launch the desired flow, and upload the resources to the Yoti Backend.

7) When all the resources have been received by the backend successfully, the client confirms this and instructs the backend to execute checks using the given resources.

8) Yoti backend provides updates to the relying business backend when available.

---

## Support

If you have any other questions please do not hesitate to contact [sdksupport@yoti.com](mailto:sdksupport@yoti.com).

Once we have answered your question we may contact you again to discuss Yoti products and services. If you’d prefer us not to do this, please let us know when you e-mail.

---