---
type: page
title: Metrics
listed: true
slug: metrics
description: 
index_title: Metrics
hidden: 
keywords: 
tags: 
---

You can retrieve metrics regarding the AVS sessions that have been created using your API keys by calling the below endpoint:

{% code %}
{% tab language="http" %}
GET https://age.yoti.com/api/v1/report/fetch-summary-stats
{% /tab %}
{% /code %}

#### Headers

{% table widths="" %}
| Header | Description | 
| ---- | ---- | 
| Authorisation | API Key to call the Yoti Age API. Should be sent as a 'Bearer {{API_TOKEN}}'. | 
| Yoti-Sdk-Id | Your unique SDK ID (uuid). | 
{% /table %}

#### Query parameters

{% table widths="" %}
| Parameter | Description | Type | 
| ---- | ---- | ---- | 
| createdAfter | Metrics will be returned for all session created after this date. Metrics will fetch data for up to six months. | dateTime | 
| createdBefore | Metrics will be returned for all session created before this date. Metrics will fetch data for up to six months. | dateTime | 
{% /table %}

#### Example response

{% code %}
{% tab language="json" %}
{
    "time_period_of_results": {
        "period_start": "2024-07-01T00:00:00Z",
        "period_end": "2024-08-14T15:00:32.144701741Z"
    },
    "total_created_sessions": 16,
    "total_complete_sessions": 7,
    "total_failed_sessions": 2,
    "total_pending_sessions": 4,
    "total_cancelled_sessions": 1,
    "total_inprogress_sessions": 0,
    "total_errored_sessions": 2,
    "address_direct_check": {
        "total_checks": 0,
        "total_complete_checks": 0,
        "total_failed_checks": 0,
        "total_errored_checks": 0,
        "total_cancelled_checks": 0,
        "total_inprogress_checks": 0,
        "total_pending_checks": 0
    },
    "age_estimation": {
        "total_checks": 5,
        "total_complete_checks": 5,
        "total_failed_checks": 0,
        "total_errored_checks": 0,
        "total_cancelled_checks": 0,
        "total_inprogress_checks": 0,
        "total_pending_checks": 0
    },
    "age_estimation_direct_check": {
        "total_checks": 0,
        "total_complete_checks": 0,
        "total_failed_checks": 0,
        "total_errored_checks": 0,
        "total_cancelled_checks": 0,
        "total_inprogress_checks": 0,
        "total_pending_checks": 0
    },
    "digital_id": {
        "total_checks": 3,
        "total_complete_checks": 0,
        "total_failed_checks": 2,
        "total_errored_checks": 0,
        "total_cancelled_checks": 0,
        "total_inprogress_checks": 0,
        "total_pending_checks": 1
    },
    "doc_scan": {
        "total_checks": 2,
        "total_complete_checks": 0,
        "total_failed_checks": 0,
        "total_errored_checks": 2,
        "total_cancelled_checks": 0,
        "total_inprogress_checks": 0,
        "total_pending_checks": 0
    },
    "credit_card": {
        "total_checks": 0,
        "total_complete_checks": 0,
        "total_failed_checks": 0,
        "total_errored_checks": 0,
        "total_cancelled_checks": 0,
        "total_inprogress_checks": 0,
        "total_pending_checks": 0
    },
    "mobile": {
        "total_checks": 0,
        "total_complete_checks": 0,
        "total_failed_checks": 0,
        "total_errored_checks": 0,
        "total_cancelled_checks": 0,
        "total_inprogress_checks": 0,
        "total_pending_checks": 0
    },
    "mobile_direct_check": {
        "total_checks": 0,
        "total_complete_checks": 0,
        "total_failed_checks": 0,
        "total_errored_checks": 0,
        "total_cancelled_checks": 0,
        "total_inprogress_checks": 0,
        "total_pending_checks": 0
    },
    "mit_id": {
        "total_checks": 0,
        "total_complete_checks": 0,
        "total_failed_checks": 0,
        "total_errored_checks": 0,
        "total_cancelled_checks": 0,
        "total_inprogress_checks": 0,
        "total_pending_checks": 0
    },
    "swedish_bank_id": {
        "total_checks": 0,
        "total_complete_checks": 0,
        "total_failed_checks": 0,
        "total_errored_checks": 0,
        "total_cancelled_checks": 0,
        "total_inprogress_checks": 0,
        "total_pending_checks": 0
    },
    "ftn": {
        "total_checks": 0,
        "total_complete_checks": 0,
        "total_failed_checks": 0,
        "total_errored_checks": 0,
        "total_cancelled_checks": 0,
        "total_inprogress_checks": 0,
        "total_pending_checks": 0
    },
    "la_wallet": {
        "total_checks": 0,
        "total_complete_checks": 0,
        "total_failed_checks": 0,
        "total_errored_checks": 0,
        "total_cancelled_checks": 0,
        "total_inprogress_checks": 0,
        "total_pending_checks": 0
    },
    "login": {
        "total_checks": 2
    },
    "social_security_number": {
        "total_checks": 0,
        "total_complete_checks": 0,
        "total_failed_checks": 0,
        "total_errored_checks": 0,
        "total_cancelled_checks": 0,
        "total_inprogress_checks": 0,
        "total_pending_checks": 0
    }
}
{% /tab %}
{% /code %}