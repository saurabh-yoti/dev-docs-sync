---
type: page
title: API settings
listed: true
slug: api-settings
description: 
index_title: API settings
hidden: 
keywords: 
tags: 
---

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

## Retrieve the results

This GET endpoint allows you to retrieve the results of the tests performed within your organisation.  Yoti gives you the option to collate anonymous results.

This endpoint will allow to fetch results from the given ID that is provided as the query parameter fromId. Specifying fromId=0 means fetching results from the start, the maximum limit is 400. 

{% badge type="info" text="Hint" /%} The response will provide the lastId from which the next call should be made in order to fetch the remaining records (in case the response reports remaining&gt;0).

**Results endpoint**

{% code %}
{% tab language="http" %}
GET	https://health.yoti.com/admin-api/v1/results?fromId=0
{% /tab %}
{% /code %}

**Anonymised results endpoint**

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

## Pre registration

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