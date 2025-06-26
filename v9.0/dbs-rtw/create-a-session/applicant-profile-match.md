---
type: page
title: Applicant Profile Match
listed: true
slug: applicant-profile-match
description: 
index_title: Applicant Profile Match
hidden: 
keywords: 
tags: 
---

A profile for an applicant may be provided during a session's creation. Should it be included, the applicant's profile data will be cross-referenced with all identity documents and address information collected within that session. The result will yield either a "match", "no match" or "partial" status for each piece of data compared. The supplied applicant profile may include any combination of the following fields:

- Name
- Date of birth
- Address

{% callout type="info" title="Info" %}
The profile match does not affect the outcome of an identity profile.
{% /callout %}

### Configure the profile

{% code %}
{% tab language="java" %}
import com.yoti.api.client.docs.session.create.resources.ResourceCreationContainer;
import java.util.Map;
import java.util.HashMap;

public class Main {
    public static Map<String, Object> address = new HashMap<>();
    static {
        address.put("address_format", 1);
        address.put("building_number", "74");
        address.put("address_line1", "74 AddressLine1");
        address.put("town_city", "London");
        address.put("postal_code", "E14 3RN");
        address.put("country_iso", "GBR");
        address.put("country", "United Kingdom");
    }  

    public static Map<String, Object> applicantProfileInput = new HashMap<>();
    static {
        applicantProfileInput.put("first_name", "John");
        applicantProfileInput.put("middle_name", "James");
        applicantProfileInput.put("family_name", "Doe");
        applicantProfileInput.put("date_of_birth", "1988-11-02");
        applicantProfileInput.put("structured_postal_address", address);
    }

    public static void main(String[] args) {
        SessionSpec sessionSpec = SessionSpec.builder()
            .withClientSessionTokenTtl(600)
            .withResourcesTtl(90000)
            .withUserTrackingId("some-user-tracking-id")
            .withSdkConfig(sdkConfig) // sdkConfig needs to be defined
            .withIdentityProfile(identityProfile) // identityProfile needs to be defined
            .withResources(ResourceCreationContainer.builder()
            		.withApplicantProfile(applicantProfileInput)
            		.build()
            )
            .build();
    }
}
{% /tab %}
{% tab language="json" %}
{
    // ...
    "resources": {
        "applicant_profile": {
            "first_name": "John",
            "middle_name": "James",
            "family_name": "Doe",
            "date_of_birth": "1988-11-02",
            "structured_postal_address": {
                "address_format": 1,
                "building_number": "74",
                "address_line1": "74 AddressLine1",
                "town_city": "London",
                "postal_code": "E14 3RN",
                "country_iso": "GBR",
                "country": "United Kingdom"
            }
        }
    }
}
{% /tab %}
{% /code %}

#### Name

There are three combinations of fields that can be used to configure the candidate name in the applicant profile:

{% callout type="warning" title="Warning" %}
It is crucial to provide the most accurate combination of names whenever possible. Please provide the name split only if you are confident that it is correct.

Favour combination 2 or 3 instead of attempting to split names if unsure.
{% /callout %}

**Combination 1 (preferred)**

{% table widths="212" %}
| Field | Description | 
| ---- | ---- | 
| first_name | The first name of the applicant | 
| middle_name | The middle name of the applicant | 
| family_name | The surname of the applicant | 
{% /table %}

**Combination 2**

{% table widths="224" %}
| Field | Description | 
| ---- | ---- | 
| given_names | All forenames of the applicant (first and all middle names) | 
| family_name | The applicant surname | 
{% /table %}

**Combination 3 (least preferred)**

{% table widths="239" %}
| Field | Description | 
| ---- | ---- | 
| full_name | The full name of the applicant, including all forenames and surname | 
{% /table %}

#### Date of birth & Address

{% table widths="256" %}
| Field | Description | 
| ---- | ---- | 
| date_of_birth | DateOfBirth is the date of birth in the form yyyy-mm-dd.\nyyyy-mm and yyyy is also accepted, however will result in a partial match against a full identity document date of birth. | 
| structured_postal_address | The postal address with a breakdown in address lines.\n\n\n\nSee details for the `structured_postal_address` JSON properties below. | 
{% /table %}

#### Structured postal address

{% synced id="structuredpostaladdress" %}
{% /synced %}

---

### Results

The results of the match will be displayed when retrieving the identity profile. Each data subset will have a result field. If the data subset is not extracted you will get a null response, otherwise the result field will either be "MATCH", "NO_MATCH" or "PARTIAL".

{% code %}
{% tab language="json" %}
{
    // ...
    "profile_match_report": {
        "provided_profile": {
            "current_name": {
                "given_names": "",
                "first_name": "John",
                "middle_name": "James",
                "family_name": "Doe",
                "full_name": ""
            },
            "date_of_birth": "1988-05-23",
            "current_address": {
                "address": {
                    "address_format": 1,
                    "care_of": "",
                    "sub_building": "",
                    "building_number": "14",
                    "building": "",
                    "street": "",
                    "landmark": "",
                    "address_line1": "14 Grove Avenue",
                    "address_line2": "",
                    "address_line3": "",
                    "address_line4": "",
                    "address_line5": "",
                    "address_line6": "",
                    "locality": "",
                    "town_city": "London",
                    "subdistrict": "",
                    "district": "",
                    "state": "",
                    "postal_code": "W7 3EP",
                    "post_office": "",
                    "country_iso": "GBR",
                    "country": "United Kingdom",
                    "formatted_address": "14 Grove Avenue\nLondon\nW7 3EP\nUnited Kingdom",
                    "udprn": ""
                },
                "move_in": ""
            }
        },
        "name": {
            "result": "PARTIAL"
        },
        "dob": {
            "result": "NO_MATCH"
        },
        "address": {
            "result": "MATCH"
        }
    }
}
{% /tab %}
{% /code %}

{% table widths="122" %}
| Result | Description | 
| ---- | ---- | 
| MATCH | The applicant profile data has matched the data extracted from the Id document/s. | 
| NO_MATCH | The applicant profile data has not matched the data extracted from the Id document/s. | 
| PARTIAL | The applicant profile data has partially matched the data extracted from the Id document/s. | 
| null | Data has not been extracted, thus nothing to compare against. | 
{% /table %}