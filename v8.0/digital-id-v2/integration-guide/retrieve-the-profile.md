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

When a user scans a QR code, Yoti makes a GET request to your redirect URI, passing the receipt Id as a query string parameter. This receipt id is URL encoded and should be decoded before being used with the Yoti SDK.

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
{% tab language="javascript" %}
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
{% tab language="python" %}
# Coming soon
{% /tab %}
{% /code %}

### Sources and Verifiers

You have a choice to allow unverified attributes like full name and address. Before completing the share, the end-user can get the attribute verified. However, if they decide to share the attribute without verification, the share will still go through but the attribute will be unverified. In order to check the verification status for a profile attribute, you can retrieve its source and verifier as describe above.

As an example, if the user has manually entered their address without verification, the `postal_address` attribute will have a source of `USER_PROVIDED`  and verifier will be blank. If however, they chose to verify their address before sharing, the attribute verifier will be `YOTI_IDENTITY`  and the sub type will contain the processing method of its verification.