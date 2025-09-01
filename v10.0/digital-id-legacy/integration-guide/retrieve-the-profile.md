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

Retrieving a profile involves receiving a one-time-use token, and decrypting it to get a user profile.

When a user scans a QR code, Yoti makes a GET request to your callback URL, passing a token as a query string parameter. The token is URL encoded and should be decoded before being used with the Yoti SDK.

For a URL set as **[https://your-callback-url](https://your-callback-url/)** in Yoti Hub, the returned callback URL would look like the following: **[https://your-callback-url?token=](https://your-callback-url/?token=)**

You can set and edit the callback URL within your Yoti application under the Integration tab. Yoti will automatically prefix the URL with your domain.

When your web application receives a token via the exposed endpoint as a query string parameter, you can easily retrieve the user profile. The user profile object provides a set of attributes corresponding to the user attributes you specified during the creation of your Yoti application on Hub.

## SDK process

When you pass the token to the Yoti Client object, the SDK does the following:

- Decrypts the wrapped receipt key attribute, using the application private key.
- Uses the decrypted key to decrypt the other party profile content attribute.
- Decodes the decrypted profile and returns it to your application.

The profile attributes are central to the SDK and allow you to see and work with the information that your users share with you.

{% code %}
{% tab language="javascript" %}
yotiClient.getActivityDetails(oneTimeUseToken)
  .then((activityDetails) => {
    const rememberMeId = activityDetails.getRememberMeId();
    const parentRememberMeId = activityDetails.getParentRememberMeId();
    const receiptId = activityDetails.getReceiptId();
    const timestamp = activityDetails.getTimestamp();
    const profile = activityDetails.getProfile();
    const applicationProfile = activityDetails.getApplicationProfile();
  
    const selfieImageData = profile.getSelfie().getValue();
  	const base64SelfieUri = profile.getSelfie().getValue().getBase64Content();
    const fullName = profile.getFullName().getValue();
    const familyName = profile.getFamilyName().getValue();
    const givenNames = profile.getGivenNames().getValue();
    const phoneNumber = profile.getPhoneNumber().getValue();
    const emailAddress = profile.getEmailAddress().getValue();
    const dateOfBirth = profile.getDateOfBirth().getValue();
    const postalAddress = profile.getPostalAddress().getValue();
    const structuredPostalAddress = profile.getStructuredPostalAddress().getValue();
    const gender = profile.getGender().getValue();
    const nationality = profile.getNationality().getValue();
    const ageVerifications = profile.getAgeVerifications();
    const ageVerified = profile.findAgeVerification('age_over:', 18).getValue(); // or 'age_under:'
    const documentDetails = profile.getDocumentDetails().getValue();
    const applicationName = applicationProfile.getName().getValue();
    const applicationUrl = applicationProfile.getUrl().getValue();
    const applicationLogo = applicationProfile.getLogo().getValue();
    const applicationReceiptBgColor = applicationProfile.getReceiptBgColor().getValue();

    // You can retrieve the sources and verifiers for each attribute as follows
    const givenNamesObj = profile.getGivenNames()
    const givenNamesSources = givenNamesObj.getSources(); // list/array of anchors
    const givenNamesVerifiers = givenNamesObj.getVerifiers(); // list/array of anchor

    // You can also retrieve further properties from these respective anchors in the following way:
    // Retrieving properties of the first anchor
    const value = givenNamesSources[0].getValue(); // string
    const subtype = givenNamesSources[0].getSubType(); // string
    const timestamp = givenNamesSources[0].getSignedTimeStamp().getTimestamp(); // Date object
    const originServerCerts = givenNamesSources[0].getOriginServerCerts(); // list of X509 certificates
  })
{% /tab %}
{% tab language="java" %}
ActivityDetails activityDetails = client.getActivityDetails(oneTimeUseToken);
HumanProfile profile = activityDetails.getUserProfile();
ApplicationProfile applicationProfile = activityDetails.getApplicationProfile();

String rememberMeId = activityDetails.getRememberMeId();
String parentRememberMeId = activityDetails.getParentRememberMeId();
Date timestamp = activityDetails.getTimestamp();
String receiptId = activityDetails.getReceiptId();
Image selfie = profile.getSelfie().getValue();
String selfieBase64Content = selfie.getBase64Content();
String fullName = profile.getFullName().getValue();
String givenNames = profile.getGivenNames().getValue();
String familyName = profile.getFamilyName().getValue();
String phoneNumber = profile.getPhoneNumber().getValue();
String emailAddress = profile.getEmailAddress().getValue();
Date dateOfBirth = profile.getDateOfBirth().getValue();
String gender = profile.getGender().getValue();
String address = profile.getPostalAddress().getValue();
String nationality = profile.getNationality().getValue();
AgeVerification over18Verification = profile.findAgeOverVerification(18);
if (over18Verification != null) {
  boolean isAgedOver18 = over18Verification.getResult();
}
AgeVerification under55Verification = profile.findAgeUnderVerification(55);
if (under55Verification != null) {
  boolean isAgedUnder55 = under55Verification.getResult();
}

Map<?, ?> structuredPostalAddress = profile.getStructuredPostalAddress().getValue();
DocumentDetails documentDetails = profile.getDocumentDetails().getValue();
String applicationName = applicationProfile.getApplicationName().getValue();
String applicationUrl = applicationProfile.getApplicationUrl().getValue();
Image applicationLogo = applicationProfile.getApplicationLogo().getValue();
String applicationReceiptBgColor = applicationProfile.getApplicationReceiptBgColor().getValue();

// You can retrieve the sources and verifiers for each attribute as follows:
Attribute<String> givenNamesAttr = profile.getGivenNames();
List<Anchor> givenNamesSources = givenNamesAttr.getSources();
List<Anchor> givenNamesVerifiers = givenNamesAttr.getVerifiers();
List<Anchor> givenNamesAnchors = givenNamesAttr.getAnchors();

// You can also retrieve further properties from these respective anchors in the following way:
// Retrieving properties of the first anchor
Anchor firstSourceAnchor = givenNamesSources.get(0);
String type = firstSourceAnchor.getType();
String value = firstSourceAnchor.getValue();
String subType = firstSourceAnchor.getSubType();
SignedTimestamp signedTimestamp = firstSourceAnchor.getSignedTimestamp();
List<X509Certificate> originCertificates = firstSourceAnchor.getOriginCertificates(); // list of X509 certificates
{% /tab %}
{% tab language="php" %}
<?php
$activityDetails = $client->getActivityDetails($oneTimeUseToken);
rememberMeId = $activityDetails->getRememberMeId();
parentRememberMeId = $activityDetails->getParentRememberMeId();
$profile = $activityDetails->getProfile();
$applicationProfile = $activityDetails->getApplicationProfile();

$selfieImageObj = $profile->getSelfie()->getValue();
$selfieImageBase64Content = $selfieImageObj->getBase64Content();
$fullName = $profile->getFullName()->getValue();
$givenNames = $profile->getGivenNames()->getValue();
$familyName = $profile->getFamilyName()->getValue();
$phoneNumber = $profile->getPhoneNumber()->getValue();
$emailAddress = $profile->getEmailAddress()->getValue();
$dateOfBirth = $profile->getDateOfBirth()->getValue();
$postalAddress = $profile->getPostalAddress()->getValue();
$structuredPostalAddress = $profile->getStructuredPostalAddress()->getValue();
$gender = $profile->getGender()->getValue();
$nationality = $profile->getNationality()->getValue();
$ageVerifications = $profile->getAgeVerifications();
$ageUnderVerification = $profile->findAgeUnderVerification($age);
$ageOverVerification = $profile->findAgeOverVerification($age);
$documentDetails = $profile->getDocumentDetails()->getValue();

$applicationName = $applicationProfile->getApplicationName()->getValue();
$applicationUrl = $applicationProfile->getApplicationUrl()->getValue();
$applicationLogo = $applicationProfile->getApplicationLogo()->getValue();
$applicationReceiptBgColor = $applicationProfile->getApplicationReceiptBgColor()->getValue();

// You can retrieve the sources and verifiers for each attribute as follows:
$givenNamesObj = $profile->getGivenNames();
$givenNamesSources = $givenNamesObj->getSources(); // list of anchors
$givenNamesVerifiers = $givenNamesObj->getVerifiers(); // list of anchors

// You can also retrieve further properties from these respective anchors in the following way:

// Retrieving properties of the first anchor
$value = $givenNamesSources[0]->getValue(); // string
$subType = $givenNamesSources[0]->getSubType(); // string
$timeStamp = $givenNamesSources[0]->getSignedTimeStamp()->getTimestamp(); // DateTime object
$originServerCerts = $givenNamesSources[0]->getOriginServerCerts(); // list of X509 certificates
{% /tab %}
{% tab language="python" %}
activity_details = client.get_activity_details(oneTimeUseToken)
profile = activity_details.profile

selfie = profile.selfie.value
given_names = profile.given_names.value
family_name = profile.family_name.value
full_name = profile.full_name.value
phone_number = profile.phone_number.value
date_of_birth = profile.date_of_birth.value
postal_address = profile.postal_address.value
structured_postal_address = profile.structured_postal_address.value
gender = profile.gender.value
nationality = profile.nationality.value
remember_me_id = activity_details.user_id
base64_selfie_uri = activity_details.base64_selfie_uri

# You can retrieve the anchors, sources and verifiers for each attribute as follows:
given_names_attribute = profile.given_names
given_names_anchors = given_names_attribute.anchors
given_names_sources = given_names_attribute.sources
given_names_verifiers = given_names_attribute.verifiers

# You can also retrieve further properties from these respective anchors in the following way:
source_anchor = given_names_sources[0]
value = source_anchor.value
sub_type = source_anchor.sub_type
timestamp = source_anchor.signed_timestamp
origin_server_certs = source_anchor.origin_server_certs
{% /tab %}
{% tab language="csharp" %}
ActivityDetails activityDetails = yotiClient.GetActivityDetails(oneTimeUseToken);
YotiProfile profile = activityDetails.Profile;

Image selfie = profile.Selfie?.GetValue();
string selfieURI = profile.Selfie?.GetValue().GetBase64URI();
string fullName = profile.FullName?.GetValue();
string givenNames = profile.GivenNames?.GetValue();
string familyName = profile.FamilyName?.GetValue();
string mobileNumber = profile.MobileNumber?.GetValue();
string emailAddress = profile.EmailAddress?.GetValue();
DateTime? dateOfBirth = profile.DateOfBirth?.GetValue();       
string address = profile.Address?.GetValue();
Dictionary<string, Newtonsoft.Json.Linq.JToken> structuredPostalAddress = profile.StructuredPostalAddress?.GetValue();
string gender = profile.Gender?.GetValue();
string nationality = profile.Nationality?.GetValue();
Yoti.Auth.Document.DocumentDetails documentDetails = profile.DocumentDetails?.GetValue();
bool? isAgedOver18 = profile.FindAgeOverVerification(18)?.Result();
bool? isAgedUnder55 = profile.FindAgeUnderVerification(55)?.Result();

// You can retrieve the anchors, sources and verifiers for each attribute as follows:
using System.Linq;
using System.Security.Cryptography.X509Certificates;
using Yoti.Auth.Anchors;
List<Anchor> givenNamesAnchors = profile.GivenNames.GetAnchors();
List<Anchor> givenNamesSources = profile.GivenNames.GetSources();
List<Anchor> givenNamesVerifiers = profile.GivenNames.GetVerifiers();

// You can also retrieve further properties from these respective anchors in the following way:
Anchor givenNamesFirstSource = profile.GivenNames.GetSources().First();
AnchorType anchorType = givenNamesFirstSource.GetAnchorType();
List<X509Certificate2> originServerCerts = givenNamesFirstSource.GetOriginServerCerts();
byte[] signature = givenNamesFirstSource.GetSignature();
DateTime signedTimeStamp = givenNamesFirstSource.GetSignedTimeStamp().GetTimestamp();
string subType = givenNamesFirstSource.GetSubType();
string value = givenNamesFirstSource.GetValue();
{% /tab %}
{% tab language="go" %}
activityDetails, err := client.GetActivityDetails(yotiOneTimeUseToken)

	rememberMeID := activityDetails.RememberMeID()
	parentRememberMeID := activityDetails.ParentRememberMeID()

	userProfile := activityDetails.UserProfile
	selfie := userProfile.Selfie().Value().Data()
	givenNames := userProfile.GivenNames().Value()
	familyName := userProfile.FamilyName().Value()
	fullName := userProfile.FullName().Value()
	mobileNumber := userProfile.MobileNumber().Value()
	emailAddress := userProfile.EmailAddress().Value()
	address := userProfile.Address().Value()
	gender := userProfile.Gender().Value()
	nationality := userProfile.Nationality().Value()
	var dateOfBirth *time.Time
	dobAttr, err := userProfile.DateOfBirth()

	if err != nil {
		// handle error
	} else {
		dateOfBirth = dobAttr.Value()
	}

	var structuredPostalAddress map[string]interface{}
	structuredPostalAddressAttribute, err := userProfile.StructuredPostalAddress()

	if err != nil {
		// handle error
	} else {
		structuredPostalAddress = structuredPostalAddressAttribute.Value()
	}

	// If you have chosen Verify Condition on the Yoti Dashboard with the age condition of "Over 18",
	// you can retrieve the user information with the generic .GetAttribute method, which requires the
	// result to be cast to the original type:
	age_over := userProfile.GetAttribute("age_over:18").Value().(string)

	// GetAttribute returns an interface, the value can be acquired through a type assertion.
	// From each attribute you can retrieve the Anchors, and subsets Sources and Verifiers
	// (all as []*anchor.Anchor) as follows:
	givenNamesAnchors := userProfile.GivenNames().Anchors()
	givenNamesSources := userProfile.GivenNames().Sources()
	givenNamesVerifiers := userProfile.GivenNames().Verifiers()

	// You can also retrieve further properties from these respective anchors in the following way:
	var givenNamesFirstAnchor *anchor.Anchor = givenNamesAnchors[0]
	var anchorType anchor.Type = givenNamesFirstAnchor.Type()
	var signedTimestamp *time.Time = givenNamesFirstAnchor.SignedTimestamp().Timestamp()
	var subType string = givenNamesFirstAnchor.SubType()
	var value string = givenNamesFirstAnchor.Value()
{% /tab %}
{% tab language="ruby" %}
yoti_activity_details = Yoti::Client.get_activity_details(oneTimeUseToken)

remember_me_id = yoti_activity_details.remember_me_id
parent_remember_me_id = yoti_activity_details.parent_remember_me_id
receipt_id = yoti_activity_details.receipt_id
timestamp = yoti_activity_details.timestamp
base64_selfie_uri = yoti_activity_details.base64_selfie_uri
age_verified = yoti_activity_details.age_verified
profile = yoti_activity_details.profile
application_profile = yoti_activity_details.application_profile

selfie_image_data = profile.selfie.value
full_name = profile.full_name.value
given_names = profile.given_names.value
family_name = profile.family_name.value
phone_number = profile.phone_number.value
email_address = profile.email_address.value
date_of_birth = profile.date_of_birth.value
postal_address = profile.postal_address.value
structured_postal_address = profile.structured_postal_address.value
gender = profile.gender.value
nationality = profile.nationality.value

application_name = application_profile.name.value
application_url = application_profile.url.value
application_logo = application_profile.logo.value
application_receipt_bgcolor = application_profile.receipt_bgcolor.value

# You can retrieve the sources and verifiers for each attribute as follows:
given_names_obj = profile.given_names
given_names_sources = given_names_obj.sources # list of anchors
given_names_verifiers = given_names_obj.verifiers # list of anchors
given_names_anchors = given_names_attribute.anchors

# You can also retrieve further properties from these respective anchors in the following way:

# Retrieving properties of the first anchor
type = given_names_sources[0].type # string
value = given_names_sources[0].value # string
sub_type = given_names_sources[0].sub_type # string
time_stamp = given_names_sources[0].signed_time_stamp.time_stamp # DateTime object
origin_server_certs = given_names_sources[0].origin_server_certs # list of X509 certificates
{% /tab %}
{% /code %}

{% html %}
<div class="alert-SAND">
    <div class="alert-title" id="SAND">
      Sandbox
    </div>
    <div class="alert-text">
       To see how to do this using our sandbox, please head over to the link below.
    </div>
    <div class="alert-links"> 
        <a href="https://developers.yoti.com/digital-id/sandbox#creating-a-sandbox-request">Creating the request</a>
    </div>
</div>
{% /html %}

Well done! This is the end of the integration!

### Sources and Verifiers

As discussed earlier, you have a choice to allow unverified attributes like full name and address. Before completing the share, the end-user can get the attribute verified. However, if they decide to share the attribute without verification, the share will still go through but the attribute will be unverified. In order to check the verification status for a profile attribute, you can retrieve its source and verifier as describe above. 

As an example, if the user has manually entered their address without verification, the `postal_address` attribute will have a source of `USER_PROVIDED`  and verifier will be blank. If however, they chose to verify their address before sharing, the attribute verifier will be `YOTI_IDENTITY`  and the sub type will contain the processing method of its verification.