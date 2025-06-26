---
type: page
title: Entities Overview
listed: true
slug: entities-overview
description: 
index_title: Entities Overview
hidden: 
keywords: 
tags: 
---

The page describes the relationship between all components which make up the Trust API.

---

#### Accounts

Accounts contain the profiles of the users to be compared to the faces found in the content to be moderated. Each account can have as many profiles as required. _Currently each account can have only one set of banned profiles._

{% image url="https://uploads.developerhub.io/prod/kvAX/vv4asn7joglkqdzfiwep31geoigqg6rzjmwjnm9oit1o20zufuedjirl7xkmkmio.png" mode="300" height="290" width="244" %}
{% /image %}

---

#### Profiles

Profiles should be created for each user that is in your platform.  They contain the images of the user (faces) and are the entity used when setting up moderation requests.

They contain the following information:

Images of the user (Faces) - Images are used to compare against the moderated content to check for matches

is_banned flag - When moderating content, unknown faces will be compared against banned profiles to check for matches

is_active flag - Inactive accounts will not be moderated

---

#### Faces

Faces are images of the user that are added to the profile.  When added, a new face will be checked against the existing images in a profile for a match to make sure it is the same user. These faces will be used in a moderation request to compare against faces found in the content being moderated. The captured_at timestamp is used for the purpose of age estimating the face and comparing that to the profile.