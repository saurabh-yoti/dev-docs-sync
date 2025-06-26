---
type: page
title: Overview
listed: true
slug: trust-api
description: 
index_title: Overview
hidden: 
keywords: 
tags: 
---

## Trust API Overview

Welcome to the developer documentation for integrating Yoti's Community Moderation (Trust) solution. The Trust API provides powerful moderation capabilities to help you manage user-generated content, verify user identities, and ensure a safe environment for your platform.

---

## Key Features

Yoti's Community Moderation solution provides a content moderation API that is able to perform the following tasks:

1. **Profile Matching**: Compare the face from the user's profile image(s) against a face found in a video or live stream to make sure it is the same person.
2. **Image Consistency**: Compare the face from a user's profile image(s) to other images uploaded to make sure they are the same person.
3. **Age Estimation**: Perform age estimation on faces found in an image, video or live stream.
4. **Banned Face Detection**: Compare a list of banned faces against an image, video or live stream.

Additional features of the Trust API include:

5. **Account Management**: Create and manage accounts for content moderation.
6. **Profile Management**: Create, update, and manage user profiles with Profile Search capabilities.
7. **Group Management**: Organisation profiles into groups for efficient searching and categorisation.
8. **Content Moderation**: Submit content for moderation and receive detailed reports.
9. **Notification System**: Receive real-time notifications about moderation results.

---

## Core Concepts

### Accounts

An account represents your organisation within the Trust API. You can create multiple accounts for different purposes (e.g., testing, production).

### Profiles

A profile represents a user and can contain up to 10 facial images. These images are used to create a biometric template for Profile Search.

### Groups

Groups are collections of profiles. You can use groups to categorise users (e.g., "Registered", "Banned") and perform efficient searches.

### Content

The API supports moderation for various types of content:

- Images
- Videos
- Live video streams

### Moderation

When you submit content for moderation, the API performs checks based on your configuration:

- Profile matching against profiles or groups
- Age estimation
- Detection of unknown faces

### Notifications

The API provides a notification system to alert you about moderation results in real-time.

---

## Getting Started

To begin using the Trust API:

1. Obtain API credentials from the Yoti Hub.
2. Create an account using the `/accounts` endpoint.
3. Set up profiles and groups as needed for your use case.
4. Start submitting content for moderation using the `/moderations` endpoint.
5. Retrieve moderation results and handle notifications as appropriate for your application.

---

## Best Practices

- Regularly update and maintain your profiles and groups for optimal performance.
- Use meaningful names and references for profiles and groups to aid in organisation.
- Implement proper error handling to manage API responses effectively.
- Consider implementing a webhook to receive real-time notifications about moderation results.

---

## Support

If you need any assistance with the Trust API, please contact Yoti support through support.yoti.com