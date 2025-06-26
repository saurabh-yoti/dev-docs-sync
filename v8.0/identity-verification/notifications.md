---
type: page
title: Notifications
listed: true
slug: notifications
description: 
index_title: Notifications
hidden: 
keywords: 
tags: 
---

The Identity verification service optionally posts an update notification, based on the selected subscription topics.

{% code %}
{% tab language="javascript" %}
const notificationConfig = new NotificationConfigBuilder()
    .withEndpoint('https://yourdomain.example/idverify/updates')
    .withAuthToken('username:password')
    .forResourceUpdate()
    .forTaskCompletion()
    .forCheckCompletion()
    .forSessionCompletion()
    .withTopic('client_session_token_deleted')
    .build();

const sessionSpec = new SessionSpecificationBuilder()
    // ...
    .withNotifications(notificationConfig)
    // ...
    .build();
{% /tab %}
{% tab language="java" %}
NotificationConfig notificationConfig = NotificationConfig.builder()
    .withEndpoint("https://yourdomain.example/idverify/updates")
    .withAuthToken("username:password")
    .withAuthTypeBasic()
    .forResourceUpdate()
    .forTaskCompletion()
    .forCheckCompletion()
    .forSessionCompletion()
    .withTopic('client_session_token_deleted')
    .build();
{% /tab %}
{% tab language="php" %}
<?php

$notificationConfig = (new NotificationConfigBuilder())
    ->withEndpoint('https://yourdomain.example/idverify/updates')
    ->withAuthToken('username:password')
    ->forResourceUpdate()
    ->forTaskCompletion()
    ->forCheckCompletion()
    ->forSessionCompletion()
    ->withTopic('client_session_token_deleted')
    ->build();
{% /tab %}
{% tab language="python" %}
notification_config = NotificationConfigBuilder()
    .with_endpoint('https://yourdomain.example/idverify/updates')
    .with_auth_token('username:password')
    .for_resource_update()
    .for_task_completion()
    .for_check_completion()
    .for_session_completion()
    .with_topic('client_session_token_deleted')
    .build()
{% /tab %}
{% tab language="csharp" %}
var notificationConfig = new NotificationConfigBuilder()
    .WithEndpoint("https://yourdomain.example/idverify/updates")
    .WithAuthToken("username:password")
    .ForResourceUpdate()
    .ForTaskCompletion()
    .ForCheckCompletion()
    .ForSessionCompletion()
    .WithTopic('client_session_token_deleted')
    .Build();
{% /tab %}
{% tab language="json" %}
{
    "notifications": {
        "endpoint": "https://yourdomain.example/idverify/updates",
        "topics": [
            "RESOURCE_UPDATE",
            "TASK_COMPLETION",
            "CHECK_COMPLETION",
            "SESSION_COMPLETION",
          	"CLIENT_SESSION_TOKEN_DELETED"
        ],
        "auth_token": "username:password",
        "auth_type": "BASIC"
    }
}
{% /tab %}
{% /code %}

Below are the different updates and options Yoti can provide:

{% table %}
| Notification | Description | 
| ---- | ---- | 
| withEndpoint | Endpoint for notifications to be sent to. Only HTTPS endpoints with TLS 1.2 are supported. A POST message will be sent. Exposing this endpoint is not mandatory but highly recommended as it would avoid a continuous polling on the session retrieval endpoint. | 
| withAuthToken | Allows the relying business backend to define an authorisation token, if they have secured API endpoints, allowing Yoti to call endpoints. We recommend protecting any exposed routes with basic authorisation. This should be used in conjunction with either 'withAuthTypeBasic' or 'withAuthTypeBearer' | 
| withAuthTypeBasic | You may specify a basic auth token to the Identity verification API to be used when sending notifications to your endpoint. Credentials are automatically encoded as base64 and sent in the Authorisation header. For example "auth_token": "username:password" would result in Authorization: Basic dXNlcm5hbWU6cGFzc3dvcmQ= being sent into the request header from Yoti. | 
| withAuthTypeBearer | This allows use of the bearer token standard, the system will create the header as follows, using the entry from withAuthToken: Authorization: Bearer | 
| forResourceUpdate | Update received whenever there are changes to **resources** in the session. For example, a user uploading a new document. | 
| forTaskCompletion | Sent when a task is completed. If you require TEXT_EXTRACTION and the check has been fulfilled, Yoti will send this through as an update to your endpoint. | 
| forSessionCompletion | Triggered when all tasks and all checks inside of a given session have been completed. | 
| forCheckCompletion | Sent when a check completes – for example a document authenticity check being performed. | 
{% /table %}

See below for example notification payloads.

## Example response

{% code %}
{% tab language="json" title="Schema" %}
{
    // Always provided
    "session_id": "<uuid>",
    "topic": "string",
    // Optional and present only when "topic" is "task_completion"
    "task_id": "<uuid>",
    // Optional and present only when "topic" is "resource_update"
    "resource_id": "<uuid>",
    // Optional and present only when "topic" is "check_completion"
    "check_id": "<uuid>"
}
{% /tab %}
{% /code %}

{% code %}
{% tab language="json" title="Session Completion" %}
{
    "session_id": "04f3b176-dcb8-428e-9b8e-8c8cd0915158",
    "topic": "session_completion"
}
{% /tab %}
{% tab language="json" title="Check Completion" %}
{
    "session_id": "04f3b176-dcb8-428e-9b8e-8c8cd0915158",
    "check_id": "f2026861-2778-4ca5-b381-38c1b86a51cc",
    "topic": "check_completion"
}
{% /tab %}
{% tab language="json" title="Client Session Completion" %}
{
    "session_id": "04f3b176-dcb8-428e-9b8e-8c8cd0915158",
    "topic": "client_session_token_deleted"
}
{% /tab %}
{% tab language="json" title="Task Completion" %}
{
    "session_id": "04f3b176-dcb8-428e-9b8e-8c8cd0915158",
    "task_id": "6fa33fe2-e35e-4a53-be5c-fe30a776f9da",
    "topic": "task_completion"
}
{% /tab %}
{% tab language="http" title="Resource Update" %}
{
    "session_id": "04f3b176-dcb8-428e-9b8e-8c8cd0915158",
    "resource_id": "962c2caf-0822-4b95-a690-1df15df80e5f",
    "topic": "resource_update"
}
{% /tab %}
{% /code %}