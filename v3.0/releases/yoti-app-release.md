---
type: page
title: Release V3.3.0
listed: true
slug: yoti-app-release
description: 
index_title: Release V3.3.0
hidden: 
keywords: 
tags: 
---

## Feature Notes

This was released on 9th July 2020.

We have built learn more pages that, when enabled, will add a 'How to set up your Yoti' link underneath the Yoti button and inline QR code which will take users to a helpful guide for end-users on how to set up their Yoti meaning as a business you don't need to provide as much information on Yoti on your own page.

To enable the learn more page on an integration the following needs to be passed in the config:

On the page the user will find:

- Your application logo and name
- Steps on how to set up their Yoti (these are dynamic based on the information you request in the share)
- A QR code to perform the share from the page (Note: this may not work if you are dynamically creating your scenario)
- Further information about Yoti and how we store their data
- A list of FAQs that we have found to be helpful ahead of on-boarding

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
       Go straight to using learn more pages and learning all about them.
    </div>
    <div class="alert-links"> 
        <a href="https://developers.yoti.com/yoti/web-integration#generate-a-yoti-button">Generate the button</a>
        <a target="_self" href="https://developers.yoti.com/yoti/user-experience-app#learn-more-page">User experience</a>
   </div>
</div>
{% /html %}

## What's New?

The following new features are available in this release:

- Learn more page functionality.
- Improvements to the error, loading and retry states in inline QR codes.

## Fixes

The following fixes are available in this release:

- N/A