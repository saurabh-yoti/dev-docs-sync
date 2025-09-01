---
type: page
title: Integration guide
listed: true
slug: integration-guide
description: 
index_title: Integration guide
hidden: 
keywords: 
tags: 
---

This document will guide you through the configuration and implementation steps that are necessary in order for your backend to be able to retrieve user’s test results.

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
Make sure you are all set up with a portal account.</div>
   <div class="alert-links"> 
      <a  target="_self" href="https://developers.yoti.com/health/overview"> Health overview </a>
   </div>
</div>
{% /html %}

The integration steps are as follows:

1. Authentication
2. Retrieve the results
3. Extra: Pre-registration

The health endpoint is listed below:

{% table %}
| Environment | URL | 
| ---- | ---- | 
| Production | [https://health.yoti.com/admin-api](https://health.yoti.com/admin-api) | 
| Retrieve results | [https://health.yoti.com/admin-api/v1/results?fromId=0](https://health.yoti.com/admin-api/v1/results?fromId=0) | 
| Retrieve anonymised results | [https://health.yoti.com/admin-api/v1/anonymised-results?fromId=0](https://health.yoti.com/admin-api/v1/anonymised-results?fromId=0) | 
| Pre registration | [https://health.yoti.com/admin-api/v1/pre-registrations](https://health.yoti.com/admin-api/v1/pre-registrations) | 
{% /table %}

---

## Authentication

The health API uses an HTTP authentication scheme called ‘bearer authentication’. This involves security tokens called ‘bearer tokens’. They are the predominant type of access token used with [OAuth 2.0](https://oauth.net/2/). A resource should interpret a bearer token as "Give the bearer of this token access". The client must send this token in the Authorization header when making requests to protected resources.

Once you are onboard with us, login to your portal &gt;&gt; Head to "**Settings**" &gt;&gt; Type in an API key name with permissions enabled &gt;&gt; **GENERATE KEY.**

{% image url="https://uploads.developerhub.io/prod/kvAX/1zyyr3ma3yzb0l54f5naazqedby4cvaqb4ps1xxoi2qgv8znzgjxnt6lzqjpob31.png" caption="API settings" mode="responsive" height="419" width="514" %}
{% /image %}

{% table %}
| Permissions | Description | 
| ---- | ---- | 
| Collection | Creating a sample. | 
| Pre registration | Add your customer’s information before testing. | 
| Results anonymised | Receive a generic report. | 
| Results full | Receive a detailed report including user information. | 
| Self registration | Integrate with other systems you are using to send customers their invites to self-register. This will allow you to get the unique urls per customer. The Self-registration API takes a flag that you can choose if the email is sent or not via the Health Portal. | 
{% /table %}

It is important that your API Key remains strictly confidential. It must be stored securely. We advise that you never commit any code containing your API Key, and never share it beyond the authorised party.

If you believe your API key has been compromised, please contact us as soon as possible. This can be done through your account manager or through our [support form](https://support.yoti.com/yotisupport/s/contactsupport)

---

## Header explained

The following elements are needed in the header:

{% table %}
| Header | Description | 
| ---- | ---- | 
| Authorization | API Key to call the Health API. This should be sent as a bearer token. | 
| Content-Type | application/json | 
{% /table %}

---

## Collection

The collection endpoint allows you to create a sample via the api, instead of going through the normal bag collection flow.

{% code %}
{% tab language="http" %}
POST https://health.yoti.com/admin-api/v1/samples
{% /tab %}
{% /code %}

### Body explained

{% code %}
{% tab language="json" %}
type CreateSampleRequest struct {
	"bagId": "string",
  "paper": false,
  "fullName":"string",
  "phone":"string",
  "email":"string",
  "dateOfBirth": "time",
  "document": "DocumentDetails",
  "homeAddress": "Address",
  "givenNames":"string",
  "familyName":"string",
  "gender": "api.Gender",
  "nationality": "api.CountryCode",
  "healthNumber":"string",
  "birthNumber":"string",
  "idVerified":true,
  "stayingAddress": "Address",
  "dateOfArrival": "time",
  "countryFrom":"string",
  "countriesVisited":"string",
  "flightNumber":"string",
  "departureDate":"time",
  "ethnicity": "api.Ethnicity",
  "vaccinationStatus":"api.VaccinationStatus",
  "testingScheme":"api.TestingScheme",
  "futureDepartureDate": "time",
  "uniqueReference":"string",
  "booking_reference":"string"
}
{% /tab %}
{% /code %}

---

## Pre-registration

This PUT endpoint will allow you to add your customer’s information before testing to speed up collection flow. Once a pre-registration is added this allows the you to search for the customer’s pre-registered data using one of the lookup fields such as email, phone, dateOfBirth .

{% code %}
{% tab language="http" %}
PUT	https://health.yoti.com/admin-api/v1/pre-registrations
{% /tab %}
{% /code %}

All fields are optional but one of the below fields is required:

{% table %}
| Field | Format | 
| ---- | ---- | 
| Email | Email address | 
| Phone | Phone number format | 
| Date of birth | YYYY-MM-DD | 
{% /table %}

### Body explained

{% code %}
{% tab language="json" %}
{
  "phone": "07474747474",
  "email": "sample@email.com",
  "fullName": "Firstname Middlename Lastname",
  "dateOfBirth": "2000-01-20",
  "documentDetails": {
    "documentType": "PASSPORT",
    "issuingCountry": "GBR",
    "documentNumber": "<<<SOME<<MRZ<<<<<<09<<<"
  },
  "homeAddress": {
    "addressLine1": "Flat 7",
    "addressLine2": "25 Long Road",
    "addressLine3": "City",
    "postalCode": "EH1 1AA",
    "countryIso": "GBR"
  },
  "givenNames": "Firstname Middlename",
  "familyName": "Lastname",
  "gender": "MALE",
  "nationality": "GBR",
  "healthNumber": "123",
  "birthNumber": "123",
  "stayingAddress": {
    "addressLine1": "Flat 7",
    "addressLine2": "25 Long Road",
    "addressLine3": "City",
    "postalCode": "EH1 1AA",
    "countryIso": "GBR"
  },
  "dateOfArrival": "2020-12-31T00:00:00Z",
  "countryFrom": "GBR",
  "countriesVisited": "GBR",
  "flightNumber": "12",
  "departureDate": null,
  "ethnicity": "UNKNOWN",
  "vaccinationStatus": "None"
}
{% /tab %}
{% /code %}

### 

---

## Results

This GET endpoint allows you to retrieve the results of the tests performed within your organisation.  Yoti gives you the option to collate anonymous results.

This endpoint will allow to fetch results from the given ID that is provided as the query parameter fromId. Specifying fromId=0 means fetching results from the start, the maximum limit is 400. 

{% badge type="info" text="Hint" /%} The response will provide the lastId from which the next call should be made in order to fetch the remaining records (in case the response reports remaining&gt;0).

### Results full endpoint

{% code %}
{% tab language="http" %}
GET	https://health.yoti.com/admin-api/v1/results?fromId=0
{% /tab %}
{% /code %}

### Anonymised results endpoint

{% code %}
{% tab language="http" %}
GET https://health.yoti.com/admin-api/v1/anonymised-results?fromId=0
{% /tab %}
{% /code %}

### Body explained

{% code %}
{% tab language="json" %}
{
    "remaining": 0,
    "lastId": 1223,
    "records": [
      {
        "id": 321,
        "identityDetails": {
          "identityVerified": true,
          "fullName": "Firstname Middlename Lastname",
          "givenNames": "Firstname Middlename",
          "familyName": "Familyname",
          "gender": "MALE",
          "dateOfBirth": "2000-01-20",
          "nationality": "GBR",
          "healthNumber": "AB12345",
          "homeAddress": {
            "addressLine1":"Flat 7",
            "addressLine2":"25 Long Road",
            "addressLine3":"",
            "addressLine4":"City",
            "postalCode": "EH1 1AA",
            "countryIso": "GBR"
          },
          "email": "sample@email.com",
          "phoneNumber": "07474747474"
        },
        "testDetails": {
          "uniqueId": "3de87639-c19f-4a97-b961-d6aee11bb254",
          "testMethod": "NAAT",
          "manufacturer": "Xyz",
          "testTypeIdentifier": "CO-AG-01",
          "testingOrg": "NHS Scotland",
          "sampleCollectAt": "2018-09-14T21:19:10Z",
          "resultReportedAt": "2018-09-14T21:19:10Z",
          "testingMachine": {
            "id": "f64f5d74-3958-451c-b215",
            "name": "ThermoFisher"
          },
          "location": {
            "addressLine1": "Test Centre",
            "addressLine2": "Road",
            "addressLine3": "",
            "addressLine4": "City",
            "postCode": "EH1 1AA",
            "countryIso": "GBR"
          },
          "cqScore": "12",
          "overallResult": "VIRUS_OR_ANTIGEN_DETECTED"
        },
        "symptoms": {
          "temperature":"36C",
          "fever": false,
          "dryCough": false,
          "fatigue": false,
          "lossOfSmellTaste": false,
          "soreThroat": false,
          "achingJoints": false,
          "nasalCongestion": false,
          "shortnessOfBreath": false,
          "diarrhoea": false
        }
      },
      {
        "id": 1223,
        "identityDetails":{}
      }
    ]
  }



//Anonymisedresults 



{
    "remaining": 0,
    "lastId": 1223,
    "records": [
      {
        "id": 321,
        "testDetails": {
          "uniqueId": "3de87639-c19f-4a97-b961-d6aee11bb254",
          "testMethod": "NAAT",
          "manufacturer": "Xyz",
          "testTypeIdentifier": "CO-AG-01",
          "testingOrg": "NHS Scotland",
          "sampleCollectAt": "2018-09-14T21:19:10Z",
          "resultReportedAt": "2018-09-14T21:19:10Z",
          "testingMachine": {
            "id": "f64f5d74-3958-451c-b215",
            "name": ThermoFisher"
          },
          "location": {
            "addressLine1": "Test Centre",
            "addressLine2": "Road",
            "addressLine3": "",
            "addressLine4": "City",
            "postCode": "EH1 1AA",
            "countryIso": "GBR"
          },
          "cqScore": "12",
          "overallResult": "VIRUS_OR_ANTIGEN_DETECTED"
        },
        "symptoms": {
            "temperature":"36C",
            "fever": false,
            "dryCough": false,
            "fatigue": false,
            "lossOfSmellTaste": false,
            "soreThroat": false,
            "achingJoints": false,
            "nasalCongestion": false,
            "shortnessOfBreath": false,
            "diarrhoea": false
        }
      },
      {
        "id": 1223,
        "testDetails": {}
      }
    ]
  }
{% /tab %}
{% /code %}

See below for explanation on each property.

---

## Self registration

This will allow you to send a self registration invite

{% code %}
{% tab language="http" %}
POST	https://health.yoti.com/admin-api/v1/self-registration-invites
{% /tab %}
{% /code %}

{% code %}
{% tab language="json" %}
{
    "org_id": 101,
    "fullName": "User",
    "phoneNumber": "123",
    "dateOfBirth": "2000-01-01",
    "email": "user@example.com",
    "type": "SELF_REGISTRATION",
    "sendEmail": true,
    "testingScheme": "TEST_TO_RELEASE"
}
{% /tab %}
{% /code %}

{% table %}
| Field | Type | Description | 
| ---- | ---- | ---- | 
| org_id | Number | Your Org ID. | 
| fullName | String | The full name of the customer. | 
| phoneNumber | Number | The phone number of the customer. | 
| dateOfbirth | Date | The date of birth of the customer. This must be in the format: YYYY-MM-DD. | 
| email | String | The email address of the customer. | 
| type | String | `SELF_REGISTRATION`, `SELF_SWAB`, `HOME_TEST`, `HOME_TEST_UNVERIFIED` | 
| send email | Boolean | Send customer an email. | 
| testingScheme | String | `TEST_TO_RELEASE`, `DAY_2.`\nLeave blank for `STANDARD` | 
{% /table %}

### Response body

{% code %}
{% tab language="json" %}
{
    "token": "randomstring",
    "inviteUrl": "https://yoururl.com"
}
{% /tab %}
{% /code %}

---

## Properties explained

Below describes each JSON property:

{% table %}
| Field | Type | Description | 
| ---- | ---- | ---- | 
| remaining | Number | Reports how many records are left to retrieve. | 
| lastID | Number | Reports the ID of the last record returned in this response. | 
| records | Array | A list of records containing test results and personal data if not anonymised. | 
| record.id | Number | The ID of this record. | 
| record.identityDetails | Object | Identity details of the user being tested. | 
| record.testDetails | Object | Details about the test and its result. | 
| record.symptoms (optional) | Object | Reported symptoms if they were collected at time of swabbing. | 
{% /table %}

{% table widths="160,0,0" %}
| Field | Optional | Type | Description | 
| ---- | ---- | ---- | ---- | 
| identityVerified | ❌ | Boolean | Indicates whether a photo ID was verified for the user being tested. | 
| fullName | ✅ | Number | The full name of the user being tested.\n\nIncludes first and last name and optionally middle names.\n\nIf the split out name is also available the below given names and\n\nfamily name will also be populated. | 
| givenNames | ✅ | String | This includes first name and middle names if provided. | 
| familyName | ✅ | String | Family name of the user being tested. | 
| dateOfBirth | ✅ | String | The date of birth of the user being tested in the form:\n\nYYYY-MM-DD. | 
| gender | ✅ | String | The gender of the user being tested.\n\nPossible values:\n\n\n\n- MALE\n- FEMALE\n- TRANSGENDER\n- OTHER | 
| nationality | ✅ | String | Nationality of the user being tested as an ISO/ICAO alpha-3 country code. | 
| healthNumber | ✅ | String | Health number (e.g. NHS number) of the user being tested. | 
| homeAddress | ✅ | Object | The home address of the user being tested.\n\nThis is the address, post code and country. See below*. | 
| email | ✅ | String | Email of the user being tested. | 
| phoneNumber | ✅ | String | Phone number of the user being tested. | 
| contactAddress | ✅ | Object | The contact address of the user being tested.\n\nThis is the address, post code and country. | 
| dateOfArrival | ✅ | String | Timestamp (UTC) of the date of arrival provided in the RFC3339 format, \n\nfor example “2018-09-14T21:19:10Z” | 
| countryFrom | ✅ | String | The country the user has come from. | 
| countriesVisited | ✅ | Array | A list of the countries that a user has visited. | 
| flightNumber | ✅ | String | Flight number | 
| departureDate | ✅ | String | Timestamp (UTC) of the departure date provided in the RFC3339 format, for example “2018-09-14T21:19:10Z” | 
| vaccinationStatus | ✅ | String | - None\n- Partial\n- Complete\n- Exempt | 
| ethnicity | ✅ | String | - BLACK - AFRICAN\n- BLACK - CARIBBEAN\n- BLACK - OTHER\n- CHINESE\n- INDIAN\n- PAKISTANI\n- WHITE\n- WHITE AND ASIAN\n- WHITE AND BLACK AFRICAN\n- WHITE AND BLACK CARIBBEAN\n- WHITE BRITISH\n- WHITE IRISH\n- WHITE OTHER\n- ISC - UNSPECIFIED\n- ANY OTHER ETHNIC CATEGORY\n- ANY OTHER MIXED GROUP\n- OTHER / MIXED\n- UNKNOWN | 
| documentDetails | ✅ | String | - DOCUMENT_TYPE\n- ISSUING_COUNTRY\n- DOCUMENT_NUMBER\n- EXPIRATION_DATE\n- ISSUING_AUTHORITY | 
{% /table %}

*Address explained:

{% table %}
| Field | Type | Description | 
| ---- | ---- | ---- | 
| addressLine1 | String | AddressLine1 is the first line of the address | 
| addressLine2 | String | AddressLine2 is the first line of the address | 
| addressLine3 | String | AddressLine3 is the first line of the address | 
| addressLine4 | String | AddressLine4 is the first line of the address | 
| postalCode | String | Postcode | 
| countryIso | String | CountryIso is the country where this address is in ISO-3166-1 alpha-3 format. | 
{% /table %}

{% table %}
| Field | Optional | Type | Description | 
| ---- | ---- | ---- | ---- | 
| uniqueId | ❌ | String | Contains an RFC 4122-compliant UUID which identifies a single test. | 
| testMethod | ✅ | String | Possible values are: “NAAT”, “RT-PCR”, “LFT”. | 
| manufacturer | ✅ | String | Reports who is the manufacturer of the test. | 
| testTypeIdentifier | ✅ | String | Uniquely identifies the test in case there are different tests \n\nwith the same method from the same manufacturer. | 
| testingOrg | ❌ | String | Your organisation. | 
| sampleCollectAt | ❌ | String | Timestamp (UTC) at which the sample was collected, provided in the RFC3339 format, for example “2018-09-14T21:19:10Z” | 
| resultReportedAt | ❌ | String | Timestamp (UTC) at which the results were reported, provided in the RFC3339 format, for example “2018-09-14T21:19:10Z” | 
| testingMachine | ✅ | Object | If configured, this will report what machine was used for processing the test. | 
| testingMachine.id | ✅ | String | A unique ID to identify the machine. Could be a serial number or a UUID. | 
| testingMachine.name | ✅ | String | A name to quickly identify what machine was used.\n\nExample values: "MyGoPro", "ThermoFisher", "TestingCube",\n\n"GeneMeTestingMachine". | 
| location | ✅ | Object | The location at which the test was carried out.\n\nThis is the address, post code and country. | 
| cqScore | ✅ | String | Only returned when applicable for the testMethod.\n\nCycle of quantification indicating the cycle number \n\nwhere the amplification curve meets a predefined criteria. | 
| overallResult | ❌ | String | Reports the result of the test indicating if the virus or the\n\nantigen were detected. \n\nThe result is marked as invalid in case it was not possible \n\nto carry out the test or in case the control indicates that\n\nthe test was not valid.\n\nPossible values are:\n\n\n\n- "VIRUS_OR_ANTIGEN_DETECTED"\n- "VIRUS_OR_ANTIGEN_NOT_DETECTED"\n- "INVALID" | 
{% /table %}

---

## Error codes

See error codes listed below:

{% table %}
| Error code | Description | 
| ---- | ---- | 
| 400 | Malformed request | 
| 500 | Unexpected server error | 
{% /table %}