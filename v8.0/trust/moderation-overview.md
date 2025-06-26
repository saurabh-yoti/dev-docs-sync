---
type: page
title: Moderation Overview
listed: true
slug: moderation-overview
description: 
index_title: Moderation Overview
hidden: 
keywords: 
tags: 
---

#### Moderation Requests

When setting up a moderation request you will need to provide the following:

{% table %}
| Request | Description | 
| ---- | ---- | 
| URL of the content | The location of the content to be moderated. This needs to be publicly accessible / accessible to the Trust & Safety tool | 
| Content type | The type of content to be checked. Currently supported types are: `VIDEO`, `LIVE_VIDEO`, `IMAGE` | 
| Profile IDs that should be in the content | The profiles of the performers that you are expecting to see in the video.  These profiles will be checked against the faces found in the content | 
| Age estimation threshold | The threshold for the age estimation check. Any unknown faces that are age estimated as below the threshold will trigger an `UNDERAGE` notification to be sent | 
| Unknown Faces Flag | The flag to set if you want to be notified about any unknown faces found in the content. If set to `TRUE`, any faces found in the video that do not match the profiles to be checked will trigger a `UNKNOWN_FACE` notification to be sent | 
| Banned Profiles Flag | The flag to set if you want to be notified about any banned faces found in the content. If set to `TRUE`, any unknown faces found in the content will be compared against the banned profiles of your account to check for matches. Any matches found will trigger a `BANNED_PROFILE` notification to be sent | 
| Notifications configuration | Configure how you want to receive notifications for the moderation request. Currently we support notifications via Websocket, Slack or via a Webhook | 
{% /table %}

---

#### Moderation Notifications

As the content gets moderated, notifications will be sent to you. These provides you with information for further review. The notifications include:

{% table %}
| Notification | Description | 
| ---- | ---- | 
| Type | The notification type will be one of the following:\n\n\n\n- `KNOWN_FACE`\n- `BANNED_FACE`\n- `UNKNOWN_FACE`\n- `AGE_ESTIMATION` (underage) | 
| Moderation ID | The ID for the moderation request | 
| Content Type | The content type will be one of the following:\n\n\n\n- `VIDEO`\n- `LIVE_VIDEO`\n- `IMAGE` | 
| Content URL | The URL of the content being moderated | 
| Content ID | The ID of the content being moderated | 
| Check ID | The ID of the check | 
| Timestamp | The timestamp of the frame where the face was found | 
| Coordinates | Coordinates of the face found that triggered the notification | 
{% /table %}