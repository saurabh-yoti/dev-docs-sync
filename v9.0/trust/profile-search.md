---
type: page
title: Profile Search
listed: true
slug: profile-search
description: 
index_title: Implementation
hidden: 
keywords: 
tags: 
---

## Overview

Profile Search is a feature of the Trust API that allows you to check users against managed groups using face comparisons. This document outlines the key concepts and implementation steps for integrating Profile Search into your application.

---

## Key Concepts

### Profiles

A profile represents a user and consists of up to 10 facial images used to construct a template for that user. Each profile is uniquely identified and can be associated with additional metadata.

### Groups

A group is a collection of profiles. Groups can be named to categorise users based on your application's needs, such as "Registered Users" or "VIP Members".

### Challenge

A challenge is the process of comparing a given facial image against profiles within a specified group to find potential matches.

---

## How It Works

1. You create profiles for your users, each containing one or more facial images.
2. You organise these profiles into groups based on your application's requirements.
3. When you need to check a user, you send a challenge request with a facial image to a specific group.
4. The API compares the provided image against the profiles in the group and returns any matches found.

---

## Implementation Steps

### 1. Create a Group

First, create a group to store your profiles:

{% code %}
{% tab language="http" %}
POST /accounts/{accountId}/groups
Content-Type: application/json
Authorization: Bearer YOUR_API_TOKEN

{
  "label": "Registered Users"
}
{% /tab %}
{% /code %}

Reference: [Create a group to collect profiles](/v9.0/trust-api/ref#postcreate-a-group-to-collect-profiles)

### 2. Create Profiles

For each user, create a profile with their facial image(s):

{% code %}
{% tab language="http" %}
POST /accounts/{accountId}/profiles
Content-Type: application/json
Authorization: Bearer YOUR_API_TOKEN

{
  "display_name": "John Doe",
  "reference": "user123",
  "face": "BASE64_ENCODED_IMAGE_DATA",
  "profile_type": 1
}
{% /tab %}
{% /code %}

Reference: [Create a profile that can contain a collection of faces](/v9.0/trust-api/ref#postcreate-a-profile-that-can-contain-a-collection-of-faces)

### 3. Add Profiles to a Group

Add the created profiles to your group:

{% code %}
{% tab language="http" %}
POST /accounts/{accountId}/groups/{groupId}
Content-Type: application/json
Authorization: Bearer YOUR_API_TOKEN

{
  "profile_id": "PROFILE_ID"
}
{% /tab %}
{% /code %}

Reference: [Add a profile to a group](/v9.0/trust-api/ref#postadd-a-profile-to-a-group)

### 4. Perform a Challenge

To search for a face within a group:

{% code %}
{% tab language="http" %}
POST /accounts/{accountId}/groups/{groupId}/challenge
Content-Type: application/json
Authorization: Bearer YOUR_API_TOKEN

{
  "image": "BASE64_ENCODED_IMAGE_DATA"
}
{% /tab %}
{% /code %}

The API will return any matching profiles found within the specified group.

Reference: [Check if a face exists in a group](/v9.0/trust-api/ref#postcheck-if-a-face-exists-in-a-group)

---

## Best Practices

- Use high-quality images when creating profiles for better accuracy.
- Organise your profiles into meaningful groups for efficient searching.
- Regularly update your profiles to maintain accuracy over time.
- Implement appropriate error handling and user feedback in your application.

---

## Use Cases

1. **User Authentication**: Verify a user's identity during login by challenging their webcam image against your "Registered Users" group.
2. **VIP Recognition**: Identify VIP customers by challenging against a "VIP Members" group.
3. **Duplicate Detection**: Prevent multiple accounts by challenging new user photos against all existing profiles.

---

## Limitations

- A maximum of 10 facial images per profile.
- Profile search accuracy may vary based on image quality.
- Ensure compliance with local privacy laws and regulations when implementing facial biometric features.

---

## Next Steps

- Explore the full [Trust API Documentation](/v9.0/trust-api/ref) for detailed endpoint specifications.
- Get help through support.yoti.com if you have any questions or need assistance.