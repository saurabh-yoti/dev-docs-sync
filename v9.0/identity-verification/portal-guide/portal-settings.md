---
type: page
title: Settings
listed: true
slug: portal-settings
description: 
index_title: Settings
hidden: 
keywords: 
tags: 
---

Here you can configure how long you want the session to be valid for, and how long you want to keep the images for.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1636397173/v2_2762/ocnzkgalkrjgavzxpbj4.png" caption="Portal &gt; Preferences" mode="responsive" height="372" width="1060" %}
{% /image %}

Yoti recommends you keep the data only if necessary. By default we set the session time to live for 1 week and the retention period to 3 months.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1636397191/v2_2762/wynyzzgp0kkbn8dixzvm.png" caption="Portal &gt; Preferences" mode="responsive" height="614" width="880" %}
{% /image %}

### Client view

Here you can configure the user view

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1636397207/v2_2762/sm7ny10mvy8yercyehhk.png" caption="Portal &gt; Preferences" mode="responsive" height="1054" width="1052" %}
{% /image %}

{% table %}
| Configuration | Description | 
| ---- | ---- | 
| Primary colour | Colour of the button on the user session view. | 
| Font colour | Change the colour of the font of the user session view. | 
| Locale | Select a translation language. See [auto$](/identity-verification/overview) for translations supported. | 
| Preset issuing country | Allows you to set which country is preset in the user session view. | 
| Success URL | If the session is successfully completed you can redirect the user to a URL. If a user is not specified, the user will remain on the final IDV screen. | 
| Error URL | If the session is unsuccessful you can redirect the user to a URL. If a user is not specified, the user will remain on the final IDV screen. | 
{% /table %}

### Mobile Handoff

You can enable a mobile handoff feature which will allow users to complete the session using their mobile devices. This can be toggled on or off and will be on as default for newly created applications.

{% image url="https://uploads.developerhub.io/prod/kvAX/mexpnk8rnidllrt8j9hqb6bni79ppbpbfy60pzya7qmdm1adounsjae3uoc0f3o5.png" mode="responsive" height="288" width="1396" %}
{% /image %}