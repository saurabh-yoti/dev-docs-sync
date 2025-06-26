---
type: page
title: System preferences
listed: true
slug: system-preferences
description: 
index_title: System preferences
hidden: 
keywords: 
tags: 
---

To create your session please start by creating your system preferences. Each of the requested checks are explained in detail over the next few sections.

{% code %}
{% tab language="javascript" title="Node.js" %}
const sessionSpec = new SessionSpecificationBuilder()
    .withClientSessionTokenTtl(900)
    .withResourcesTtl(90000)
    .withUserTrackingId('some-user-tracking-id')
    .withRequestedCheck(documentAuthenticityCheck)
    .withRequestedCheck(livenessCheck)
    .withRequestedCheck(faceMatchCheck)
    .withRequestedTask(textExtractionTask)
    .withSdkConfig(sdkConfig)
    .withNotifications(notificationConfig)
    .build();
{% /tab %}
{% tab language="java" %}
SessionSpec sessionSpec = SessionSpec.builder()
    .withClientSessionTokenTtl(900)
    .withResourcesTtl(9000)
    .withUserTrackingId("<YOUR_USER_ID>")
    .withNotifications(notificationConfig)
    .withSdkConfig(sdkConfig)
    .withRequestedCheck(documentAuthenticityCheck)
    .withRequestedCheck(livenessCheck)
    .withRequestedCheck(faceMatchCheck)
    .withRequestedTask(textExtractionTask)
    .build();
{% /tab %}
{% tab language="php" %}
<?php

$sessionSpec = (new SessionSpecificationBuilder())
    ->withClientSessionTokenTtl(900)
    ->withResourcesTtl(90000)
    ->withUserTrackingId('some-user-tracking-id')
    ->withRequestedCheck($documentAuthenticityCheck)
    ->withRequestedCheck($livenessCheck)
    ->withRequestedCheck($faceMatchCheck)
    ->withRequestedTask($textExtractionTask)
    ->withSdkConfig($sdkConfig)
    ->withNotifications($notificationConfig)
    ->build();
{% /tab %}
{% tab language="python" %}
session_spec = (
    SessionSpecBuilder()
    .with_client_session_token_ttl(900)
    .with_resources_ttl(90000)
    .with_user_tracking_id("some-user-tracking-id")
    .with_requested_check(documentAuthenticityCheck)
    .with_requested_check(livenessCheck)
    .with_requested_check(faceMatchCheck)
    .with_requested_task(textExtractionTask)
    .with_sdk_config(sdk_config)
    .with_notifications(notification_config)
    .build()
)
{% /tab %}
{% tab language="csharp" %}
var sessionSpec = new SessionSpecificationBuilder()
    .WithClientSessionTokenTtl(900)
    .WithResourcesTtl(90000)
    .WithUserTrackingId("some-user-tracking-id")
    .WithRequestedCheck(documentAuthenticityCheck)
    .WithRequestedCheck(livenessCheck)
    .WithRequestedCheck(faceMatchCheck)
    .WithRequestedTask(textExtractionTask)
    .WithNotifications(notificationConfig)
    .WithSdkConfig(sdkConfig)
    .Build();
{% /tab %}
{% tab language="go" %}
sessionSpec, err = create.NewSessionSpecificationBuilder().
    WithClientSessionTokenTTL(900).
    WithResourcesTTL(90000).
    WithUserTrackingID("some-tracking-id").
    WithRequestedCheck(faceMatchCheck).
    WithRequestedCheck(documentAuthenticityCheck).
    WithRequestedCheck(livenessCheck).
    WithRequestedTask(textExtractionTask).
    WithSDKConfig(sdkConfig).
    Build()
{% /tab %}
{% tab language="json" %}
{
    "client_session_token_ttl": 900,
    "resources_ttl": 90000,
    "user_tracking_id": "some-user-tracking-id"
}
{% /tab %}
{% /code %}

The table below explains the optional parameters for the session and data retention configuration.

{% table widths="" %}
| Parameters | Description | Optional | 
| ---- | ---- | ---- | 
| withClientSessionTokenTtl | This is how long the full Identity verification session is open for in seconds. This must be longer than 300s (5 minutes).\n\n\n\nNote: If a session has less than 10 minutes remaining a prompt will be shown to the user instructing that the session is near expiry. \n\n\n\nWe recommend configuring your session ttl to at least 15 minutes to avoid showing this prompt to the user at the start of the process. | ✅ | 
| withResourcesTtl | Retention period ("time to live") for uploaded documents/images in number of seconds. Default is one week (`60_60_24*7=604800`). This can be a minimum of 24 hours and must be at least 24 hours longer than the `client_session_token_ttl`. The resource timer is based on media upload, not from session creation.\n\n\n\nNote: This config may result in additional charges. Please get in touch with support if considering a TTL longer than three months. | ✅ | 
| withUserTrackingId | Allows the relying business backend to track the same user across multiple sessions. **Note:** This should not contain any personal identifiable information. | ✅ | 
| WithBlockBiometricConsent | For several American states (currently Texas, Illinois and Washington US states*), the law mandates that you must collect the user’s specific consent to collect their biometric details for our liveness or face matching feature to be compliant with the US legislation.\n\n\n\n*and any other countries or states within countries\n\nIf you choose to only request specific consent in the above "territories" you must provide details of the effective geo location software you use to prevent any individuals located in one of these territories accessing the Yoti service without prior giving specific consent.\n\n\n\nSetting to true bypasses this screen. We recommend keeping this value to default (false) to enable consent for all users. | ✅ | 
{% /table %}