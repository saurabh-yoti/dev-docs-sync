---
type: page
title: Android releases
listed: true
slug: identityverification-android-release
description: 
index_title: Android releases
hidden: 
keywords: 
tags: 
---

The identity verification Android SDK can be seamlessly integrated with your app so you can perform secure identity checks. You'll be able to request specific ID documents from users directly from your app.

### Quick Links

✏️[Developer docs](https://developers.yoti.com/identity-verification/getting-started)

🎨 [User experience](https://developers.yoti.com/identity-verification/user-experience)

ℹ️ [Further information](https://business.yoti.com/doc-scan/)

📧 [Integration help](mailto:clientsupport@yoti.com)

🏛 [Business help](https://www.yoti.com/contact-us/)

🖥 [Demo](https://yoti.world/yoti-doc-scan/) and [example projects](https://developers.yoti.com/identity-verification/quick-start)

See release notes below.

---

## V.2.6.1

This was released on 26th March 2021.

{% badge type="info" text="IMPROVEMENT" /%} Allow text data extraction to be set as ALWAYS.

---

## V.2.6.0

This was released on 8th March 2021.

{% badge type="success" text="NEW" /%} Add support for new document types: Bank Statement and Nexus Card.

{% badge type="info" text="IMPROVEMENT" /%} Copy changes in the "More About Verification" screen

{% badge type="info" text="IMPROVEMENT" /%} Generic error screen handling and improvements

{% badge type="info" text="IMPROVEMENT" /%} Update on OCR software.

{% badge type="success" text="NEW" /%} Third party identity checks.

{% badge type="error" text="BUG" /%} Minor bug fixes

---

## V.2.5.1

This was released on 19th November 2020.

{% badge type="success" text="NEW" /%} Add metadata parameter to track when React Native wrapper is used

{% badge type="success" text="NEW" /%} Handle parameter to call the Canadian data centre

{% badge type="success" text="NEW" /%} Show country name only in the available languages

{% badge type="success" text="NEW" /%} Rename PHL and IDN Id documents

{% badge type="success" text="NEW" /%} Handle biometric consent required option

{% badge type="success" text="NEW" /%} Hide logo feature

{% badge type="success" text="NEW" /%} Reduce Aadhaar educational video size

{% badge type="error" text="BUG" /%} Minor bug fixes

---

## V.2.4.0

This was released on 23rd September 2020.

{% badge type="success" text="NEW" /%}Enable support for supporting documents

{% badge type="success" text="NEW" /%}UI redesign of the "More about verification" screen

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
        Enable supporting documents into your flow.
    </div>
    <div class="alert-links"> 
        <a href="https://developers.yoti.com/identity-verification/document-checking#supporting-documents">Supporting documents</a>
   </div>
</div>
{% /html %}

---

## V.2.3.2

This was released on 3rd August 2020.

{% badge type="success" text="NEW" /%} New document types for the Philippines, namely "Voter Id" and "Professional Id".

{% badge type="info" text="FIX" /%} Bug fixes related to users located are in a negative GMT time zone not being able to use the NFC functionality when submitting a copy of their passport.

{% badge type="info" text="FIX" /%} Fix on NFC functionality with new British passports.

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
        Integrate our SDK to see what documents we support.
    </div>
    <div class="alert-links"> 
        <a href="https://developers.yoti.com/identity-verification/document-checking#supported-documents">Supported documents</a>
   </div>
</div>
{% /html %}

---

## V.2.3.1

This was released on 20th July 2020.

{% badge type="success" text="NEW" /%} Improve firebase plugin

{% badge type="info" text="FIX" /%} React native compatibility fix