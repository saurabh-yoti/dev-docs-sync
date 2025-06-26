---
type: page
title: Applicant pools
listed: true
slug: create-applicant-pool
description: 
index_title: Applicant pools
hidden: 
keywords: 
tags: 
---

## Create Applicant Pool

Once applicants have been created, you will then need to create an applicant pool to compile all of your applicants into a list.

{% code %}
{% tab language="http" %}
POST https://api.yoti.com/idverify/v1/pools
{% /tab %}
{% /code %}

### Request body

You simply need to provide a label for the applicant pool in the request body.

{% code %}
{% tab language="json" %}
{
    "label": "POOL EXAMPLE" 
}
{% /tab %}
{% /code %}

### Response

You will receive the pool id as well as your pool label in the response:

{% code %}
{% tab language="json" %}
{
  "id":"f419fe6e-0009-4ade-9c7e-3f1a08c045be",
  "label":"POOL EXAMPLE"
}
{% /tab %}
{% /code %}

---

## Add an applicant to an applicant pool

Once an applicant pool has been created, you can start to add applicants to this pool. You can add multiple applicants to a single pool, to create a list with multiple individuals.

{% code %}
{% tab language="http" %}
POST https://api.yoti.com/idverify/v1/pools/{poolId}/applicants
{% /tab %}
{% /code %}

### Request body

You need to include an applicant id that has been previously generated in the body of this request.

{% code %}
{% tab language="json" %}
{
  "applicant_id": "APPLICANT_ID"
}
{% /tab %}
{% /code %}

### Response

On a successful response you will simply receive a **204** status code.

---

## Error response

{% table widths="" %}
| Error code | Description | 
| ---- | ---- | 
| 400 | Bad request - there was an error when validating the request payload | 
| 401 | Unauthorised - the request to the endpoint is not authorised for the API keys use | 
| 403 | Insufficient permission - the sdk id does not have permission to use this service | 
| 404 | Not found - pool can't be found linked to the supplied id | 
| 503 | Service unavailable - Yoti services are temporarily unavailable | 
{% /table %}