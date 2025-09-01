---
type: page
title: Retrieve the profile
listed: true
slug: retrieve-the-profile
description: 
index_title: Retrieve the profile
hidden: 
keywords: 
tags: 
---

Retrieving a profile involves retrieving a Receipt ID, and decrypting it to get the user profile.

After the user scans a QR code and share their profile, the webshare script will perform an redirection from the QR code page to your redirect URI, passing the receipt Id as a query string parameter. This receipt id is URL encoded and should be decoded before being used with the Yoti SDK.

For a Redirect URI set as **[https://your-redirect-uri](https://your-redirect-uri)** in the Share session configuration, the returned URL would look like the following: **[https://your-redirect-uri?receiptId=](https://your-redirect-uri?receiptId=)**.

Yoti will automatically prefix this URL with domain name specified in your Yoti Hub app.

When your web application receives the receipt id via the defined endpoint as a query string parameter, you can easily retrieve the user profile. The user profile object provides a set of user attributes corresponding to the attributes that you request in the share session.

## SDK process

When you pass the receipt id to the Yoti Identity Client object, the SDK does the following:

- Decrypts the wrapped receipt key attribute, using the application private key.
- Uses the decrypted key to decrypt the other party profile content attribute.
- Decodes the decrypted profile and returns it to your application.

The profile attributes are central to the SDK and allow you to see and work with the information that your users share with you.

{% code %}
{% tab language="javascript" title="Node.js" %}
yotiClient.getShareReceipt(receiptId)
  .then((shareReceipt) => {
  	const sessionId = shareReceipt.getSessionId();
  	const rememberMeId = shareReceipt.getRememberMeId();
  	const parentRememberMeId = shareReceipt.getParentRememberMeId();

    const profile = shareReceipt.getProfile();
  
    const fullName = profile.getFullName().value;
    const dateOfBirth = profile.getDateOfBirth().getValue();
    const gender = profile.getGender().getValue();
    const nationality = profile.getNationality().getValue();
  	const postalAddress = profile.getPostalAddress().getValue();
    const emailAddress = profile.getEmailAddress().getValue();
    const phoneNumber = profile.getPhoneNumber().getValue();
    const selfieImageData = profile.getSelfie().getValue();
    const base64SelfieUri = selfieImageData.getBase64Content();
    
    const documentDetails = profile.getDocumentDetails().getValue();
  })
{% /tab %}
{% tab language="java" %}
try {
  	Receipt shareReceipt = client.fetchShareReceipt(receiptId);
  
  	String sessionId = shareReceipt.getSessionId();
  	String rememberMeId = shareReceipt.getRememberMeId();
  	String parentRememberMeId = shareReceipt.getParentRememberMeId();

    HumanProfile profile = shareReceipt.getProfile();
  
    String fullName = profile.getFullName().getValue();
		Date dateOfBirth = profile.getDateOfBirth().getValue();
		String gender = profile.getGender().getValue();
		String nationality = profile.getNationality().getValue();
  	String postalAddress = profile.getPostalAddress().getValue();
  	String emailAddress = profile.getEmailAddress().getValue();
  	String phoneNumber = profile.getPhoneNumber().getValue();

  	Image selfieImageData = profile.getSelfie().getValue();
		String selfieBase64Content = selfieImageData.getBase64Content();
  
  	DocumentDetails documentDetails = profile.getDocumentDetails().getValue();
} catch (DigitalIdentityException e) {
  	LOG.error(e.getMessage());
}
{% /tab %}
{% tab language="php" %}
<?php
  
$shareReceipt = $client->fetchShareReceipt($receiptId);

$sessionId = $shareReceipt->getSessionId();
$rememberMeId = $shareReceipt->getRememberMeId();
$parentRememberMeId = $shareReceipt->getParentRememberMeId();

$applicationProfile = $shareReceipt->getApplicationContent()->getProfile();
$applicationName = $applicationProfile->getApplicationName();

$profile = $shareReceipt->getProfile();

$fullName = $profile->getFullName()->getValue();
$dateOfBirth = $profile->getDateOfBirth()->getValue();
$nationality = $profile->getNationality()->getValue();
$postalAddress = $profile->getPostalAddress()->getValue();
$structuredPostalAddress = $profile->getStructuredPostalAddress()->getValue();
$selfieImageObj = $profile->getSelfie()->getValue();
$selfieImageBase64Content = $selfieImageObj->getBase64Content();

$documentDetails = $profile->getDocumentDetails()->getValue();
{% /tab %}
{% tab language="csharp" %}
ShareReceipt shareReceipt = yotiClient.GetShareReceipt(receiptId);

DateTime? timestamp = shareReceipt.Timestamp;
string sessionId = shareReceipt.SessionId;
string rememberMeId = shareReceipt.RememberMeId;

YotiProfile profile = shareReceipt.Profile;
Image selfie = profile.Selfie?.GetValue();
string selfieURI = profile.Selfie?.GetValue().GetBase64URI();

string fullName = profile.FullName?.GetValue();
string emailAddress = profile.EmailAddress?.GetValue();

DateTime? dateOfBirth = profile.DateOfBirth?.GetValue(); 
string nationality = profile.Nationality?.GetValue();
string address = profile.Address?.GetValue();

bool hasIdentityProfile = profile.IdentityProfileReport != null ? true : false;

if (hasIdentityProfile) {
	var identityProfileReport = profile.IdentityProfileReport.GetValue();
}
{% /tab %}
{% tab language="go" %}
shareReceipt, err := client.GetShareReceipt(receiptId)

sessionId := shareReceipt.SessionID
rememberMeID := shareReceipt.RememberMeID
parentRememberMeID := shareReceipt.ParentRememberMeID

userProfile := shareReceipt.UserContent.UserProfile
selfie := userProfile.Selfie()
selfieBase64URL := selfie.Value().Base64URL()
fullName := userProfile.FullName().Value()
givenNames := userProfile.GivenNames().Value()
familyName := userProfile.FamilyName().Value()
mobileNumber := userProfile.MobileNumber().Value()
emailAddress := userProfile.EmailAddress().Value()

var dateOfBirth *time.Time
dobAttr, err := userProfile.DateOfBirth()

if err != nil {
		// handle error
} else {
  dateOfBirth = dobAttr.Value()
}

gender := userProfile.Gender().Value()
address := userProfile.Address().Value()
nationality := userProfile.Nationality().Value()
{% /tab %}
{% /code %}

### Sources and Verifiers

You have a choice to allow unverified attributes like full name and address. Before completing the share, the end-user can get the attribute verified. However, if they decide to share the attribute without verification, the share will still go through but the attribute will be unverified. In order to check the verification status for a profile attribute, you can retrieve its source and verifier as describe above.

As an example, if the user has manually entered their address without verification, the `postal_address` attribute will have a source of `USER_PROVIDED` and verifier will be blank. If however, they chose to verify their address before sharing, the attribute verifier will be `YOTI_IDENTITY` and the sub type will contain the processing method of its verification.

{% code %}
{% tab language="javascript" title="Node.js" %}
// Get full name attribute and its sources/verifiers
const fullNameAttr = profile.getFullName();

const fullNameSources = fullNameAttr.getSources().map(source => ({
  value: source.getValue(),
  subType: source.getSubType(),
}));

const fullNameVerifiers = fullNameAttr.getVerifiers().map(verifier => ({
  value: verifier.getValue(),
  subType: verifier.getSubType(),
}));

// Get all attributes and their sources/verifiers
const attributes = profile.getAttributesList();
attributes.forEach(attribute => {
  const name = attribute.getName();
  const value = attribute.getValue();
  
  const sources = attribute.getSources().map(source => ({
    value: source.getValue(),
    subType: source.getSubType(),
  }));
  
  const verifiers = attribute.getVerifiers().map(verifier => ({
    value: verifier.getValue(),
    subType: verifier.getSubType(),
  }));
});
{% /tab %}
{% tab language="java" %}
// Get full name attribute and its sources/verifiers
Attribute<String> fullNameAttr = profile.getFullName();

List<Source> fullNameSources = fullNameAttr.getSources();
for (Source source : fullNameSources) {
    String value = source.getValue();
    String subType = source.getSubType();
}

List<Verifier> fullNameVerifiers = fullNameAttr.getVerifiers();
for (Verifier verifier : fullNameVerifiers) {
    String value = verifier.getValue();
    String subType = verifier.getSubType();
}

// Get all attributes and their sources/verifiers
List<Attribute<?>> attributes = profile.getAttributes();
for (Attribute<?> attribute : attributes) {
    String name = attribute.getName();
    Object value = attribute.getValue();
  
    List<Source> sources = attribute.getSources();
  
    List<Verifier> verifiers = attribute.getVerifiers();
}
{% /tab %}
{% tab language="php" %}
// Get full name attribute and its sources/verifiers
$fullNameAttr = $profile->getFullName();

$fullNameSources = $fullNameAttr->getSources();
foreach ($fullNameSources as $source) {
    $value = $source->getValue();
    $subType = $source->getSubType();
}

$fullNameVerifiers = $fullNameAttr->getVerifiers();
foreach ($fullNameVerifiers as $verifier) {
    $value = $verifier->getValue();
    $subType = $verifier->getSubType();
}

// Get all attributes and their sources/verifiers
$attributes = $profile->getAttributes();
foreach ($attributes as $attribute) {
    $name = $attribute->getName();
    $value = $attribute->getValue();
  
    $sources = $attribute->getSources();
  
    $verifiers = $attribute->getVerifiers();
}
{% /tab %}
{% tab language="csharp" %}
// Get full name attribute and its sources/verifiers
var fullNameAttr = profile.FullName;

var fullNameSources = fullNameAttr?.Sources;
if (fullNameSources != null)
{
    foreach (var source in fullNameSources)
    {
        var value = source.Value;
        var subType = source.SubType;
    }
}

var fullNameVerifiers = fullNameAttr?.Verifiers;
if (fullNameVerifiers != null)
{
    foreach (var verifier in fullNameVerifiers)
    {
        var value = verifier.Value;
        var subType = verifier.SubType;
    }
}

// Get all attributes and their sources/verifiers
var attributes = profile.Attributes;
foreach (var attribute in attributes)
{
    var name = attribute.Name;
    var value = attribute.Value;
  
    var sources = attribute.Sources;
  
    var verifiers = attribute.Verifiers;
}
{% /tab %}
{% tab language="go" %}
// Get full name attribute and its sources/verifiers
fullNameAttr := userProfile.FullName()

fullNameSources := fullNameAttr.Sources()
for _, source := range fullNameSources {
    value := source.Value()
    subType := source.SubType()
}

fullNameVerifiers := fullNameAttr.Verifiers()
for _, verifier := range fullNameVerifiers {
    value := verifier.Value()
    subType := verifier.SubType()
}

// Get all attributes and their sources/verifiers
attributes := userProfile.Attributes()
for _, attribute := range attributes {
    name := attribute.Name()
    value := attribute.Value()
  
    sources := attribute.Sources()
  
    verifiers := attribute.Verifiers()
}
{% /tab %}
{% /code %}

## Webhook notifications

If the webhook endpoint is provided during the [Share session](https://developers.yoti.com/digital-id/create-share-session#specify-the-session-configuration) creation, the notifications will be sent for each share performed by the end-user. These will also contain the Receipt ID that can be used to retrieve the decrypted user profile.

The notifications will be sent in the following format:

**COMPLETED:**

{% code %}
{% tab language="json" %}
{
    "id": "ss.v2.ChZV8h5GZTlLT1JrSzc5QkVMc1F0a9JR3gkyLmxkNS5nYnI=",
    "status": "COMPLETED",
    "created": "2023-08-01T13:21:06.389Z",
    "updated": "2023-08-01T13:22:48.284Z",
    "receipt": {
        "id": "RPA4ZvOZ/xIRhIeHh9Jw9HNpEK//610kEpCbZmQwNZlZ6H6w41VUlDQWn+4p7Lk"
    }
}
{% /tab %}
{% /code %}

**FAILED:**

{% code %}
{% tab language="json" %}
{
    "id": "ss.v2.ChYwYk5mSG9sdlJSbWNFQ1VJHw4kYlZ3EgkzLmxkNS5nYnI=",
    "status": "FAILED",
    "created": "2023-08-02T08:33:23.326Z",
    "updated": "2023-08-02T08:34:40.885Z",
    "receipt": {
      "id": "FYWI8nE8GAo8xMBVprPCG78J4TaWsW+prX5DEj9WN0eEROlg7avAP/ZAlJmlP3C1",
      "error": "MANDATORY_DOCUMENT_NOT_PROVIDED"
    }
}
{% /tab %}
{% /code %}

### Session status

A webhook notification is triggered based on the Session state, which could be one of the following:

{% table widths="218" %}
| Status | Description | 
| ---- | ---- | 
| COMPLETED | The share associated with the session was completed (with success receipt available). | 
| FAILED | The share associated with the session was completed (with failure receipt available). | 
| CANCELLED | Mobile app requested the session to be cancelled (before share was completed). | 
| EXPIRED | The share associated with the session was never completed (no receipt available). | 
| ERROR | A "catch-all" status for unexpected/unrecoverable errors that might happen during execution (e.g. we get a receipt but the service fails to parse it, required parameter not present). | 
{% /table %}