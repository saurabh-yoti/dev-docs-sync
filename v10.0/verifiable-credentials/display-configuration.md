---
type: page
title: Display configuration
listed: true
slug: display-configuration
description: 
index_title: Display configuration
hidden: 
keywords: 
tags: 
---

In the credential definition, you can now include the display configuration. This provides a way to control how the information held in the credential will be displayed inside the Yoti/Digital ID app. The details for the credential will be shown in a generic rendering format. 

To specify the display config, you have to update the existing locales section in the [credential definition](/digital-id-legacy/defining-the-credential) to include the `displayTexts` array which contains the key-value pairs for the displayable text. In the new display section, integrators are able to define how the value of their credential will be shown in the app.

## Locales section

The locales section supports the definition of localised strings where texts can be defined in multiple languages.  When the locale required has not been defined, the default locale will be that is used. These strings have to be defined in `displayTexts` array in the form of key-value pairs.

{% code %}
{% tab language="json" %}
"locales": {
    "default": "en_GB",
    "values": [
        {
            "locale": "en_GB",
            "name": "Human readable name of the credential",
            "infoUri": "https://website.co.uk",
            "displayTexts": [
                {
                    "key": "loc.content.greeting",
                    "value": "Hello world!"
                }
            ]
        },
        {
            "locale": "es_ES",
            "name": "Nombre del atributo",
            "infoUri": "https://website.es",
            "displayTexts": [
                {
                    "key": "loc.content.greeting",
                    "value": "Hola mundo!"
                }
            ]
        }
    ]
}
{% /tab %}
{% /code %}

### Dynamic strings

There is also the possibility to create dynamic strings where pieces of text will come from data stored in the credential itself. In the following example, we have a value that contains two pieces of dynamic text. The idea here is to dynamically replace %1$s by the name of the user and %2$s by the surname.

{% code %}
{% tab language="json" %}
"locales": {
    "default": "en_GB",
    "values": [
        {
            "locale": "en_GB",
            "name": "Human readable name of the credential",
            "infoUri": "https://website.co.uk",
            "displayTexts": [
                {
                    "key": "loc.content.user_greeting",
                    "value": "Hello %1$s %2$s"
                }
            ]
        },
        {
            "locale": "es_ES",
            "name": "Nombre del atributo",
            "infoUri": "https://website.es",
            "displayTexts": [
                {
                    "key": "loc.content.user_greeting",
                    "value": "Hola %1$s %2$s"
                }
            ]
        }
    ]
}
{% /tab %}
{% /code %}

## Display section

In the display section, integrators are able to define how the value of their credential will be shown in the mobile app. It contains a "category" field which is the category a credential belongs to. For example - employment, degree, etc. A set of categories are defined by Yoti.

This section is further divided into three parts - compact, full and argDefinitions. These are explained below.

### Compact view

The compact view is where we show a summary of the credential. This section contains 3 lines of text where we can specify what specific data will go in each of them by making use of the identifiers that we will create in the "argDefinitions" section below. Title and subtitle are mandatory whilst extra is optional.

{% code %}
{% tab language="json" %}
"compact": {
    "title": {
        "argv": ["company_name"]
    },
    "subtitle": {
        "key": "loc.content.greeting"
    },
    "extra": {
        "key": "loc.content.user_greeting",
        "argv": ["user_name"]
    }
}
{% /tab %}
{% /code %}

In this example above, we have used three different ways to provide data to those fields.

- In title, we are using directly an argDefinition that we would declare below.
- In subtitle, we are using a key that points to one of the strings declared in the locales section and its valye corresponds to a hardcoded string.
- And in extra, we have a dynamic string declared in the locales section that will get populated with the value of an argDefinition.

### Full view

The full view is where we specify the information to be displayed in the screen where we show a most detailed version of the credential. It is comprised of four elements:

- **logo**: It is the company logo and is defined like this:

{% code %}
{% tab language="json" %}
"logo": {
    "argv": ["company_logo"]
}
{% /tab %}
{% /code %}

- **title**: It is the main text for the credential:

{% code %}
{% tab language="json" %}
"title": {
    "argv": ["company_name"]
}
{% /tab %}
{% /code %}

- **subtitle**: It is secondary text for the credential.

{% code %}
{% tab language="json" %}
"subtitle": {
    "argv": ["job_title"]
}
{% /tab %}
{% /code %}

- **items**: It is a list of label/value pairs where label is a string and value can be defined by a key, a key and argv or just argv which will be resolved to text, image, date or a set of texts.

{% code %}
{% tab language="json" %}
"items": [
    {
        "label": "loc.label.start_date",
        "argv": ["start_date"]
    },
    {
        "label": "loc.label.end_date",
        "argv": ["end_date"]
    },
    {
        "label": "loc.label.employee_of_month",
        "argv": ["employee_of_month"]
    },
    {
        "label": "loc.label.achievements",
        "key": "loc.achievements.content",
      	"argv": ["achievements"]
    },
    {
        "label": "loc.label.my_item",
        "key": "loc.my_static_item.value"
    }
]
{% /tab %}
{% /code %}

### ArgDefinitions

The argDefinitions section is an array where we can create identifiers for each piece of information (text, image or date) that we want to display from our credential. Those identifiers will be used in the views section (compact and full), where we decide what piece of information goes in which part of the screen.

Each argDefinition consists of four parts:

- **id**: This is a mandatory field to define the identifier (which we will use in the display section).
- **paths**: This is a mandatory field with the json paths to the value inside the credential.
- **schema**: This is a mandatory field with information about the the type and format.
    - **type (mandatory)**: “string”, “array_string”, “integer” or “float”
    - **format (optional)**: “image/url”, “image/base64”, “date”, “date-time”, “time” or “url” 

- **fallback**: This is an optional field that points to a localised key previously defined in the "locales" section. This will be shown to the user if for whatever reason the value specified in "paths" cannot be reached.

{% code %}
{% tab language="json" %}
"argDefinitions": [
    {
        "id": "company_name",
        "paths": ["$.companyInfo.companyName"],
        "schema": {
            "type": "string"
        },
        "fallback": "loc.content.company_name_fallback"
    },
    {
        "id": "start_date",
        "paths": ["$.employment.startDate"],
        "schema": {
            "type": "string",
            "format": "date"
        },
        "fallback": "loc.content.start_date_fallback"
    },
    {
        "id": "company_logo",
        "paths": ["$.companyInfo.companyLogoUrl"],
        "schema": {
            "type": "string",
            "format": "image/url"
        }
    }
]
{% /tab %}
{% /code %}

In the example above, we have three argDefinitions each with different format:

- **text**: This is the default format which is displayed a plain text.
- **date**: We can take timestamps from the credential to be displayed as dates, dates with time or just time. It is important to note that these dates will need to be compliant with the [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format.
- **image/url**: We will take the image from a url that points to an external server that hosts the image.

## Full example

### Credential definition

A complete example of the content for a credential with the display config could look like this:

{% code %}
{% tab language="json" %}
{
    "name": "com.yoti.test.employment.past",
    "icon": "data:image/jpeg;base64/9j/4AAQSkZJRgABAQAAAQABAAD/4gIcSUNDX...",
    "locales": {
        "default": "en_GB",
        "values": [
            {
                "locale": "en_GB",
                "name": "My example credential",
                "infoUri": "https://website.co.uk",
                "displayTexts": [
                    {"key": "loc.content.period",
                    "value": "%1$s - %2$s"},
                    {"key": "loc.label.start_date",
                    "value": "Start date"},
                    {"key": "loc.label.end_date",
                    "value": "End date"},
                    {"key": "loc.label.skills",
                    "value": "Skills"},
                    {"key": "loc.content.company_name_fallback",
                    "value": "N/A"},
                    {"key": "loc.content.role_description_fallback",
                    "value": "-"},
                    {"key": "loc.content.job_position_fallback",
                    "value": "-"}
                ]
            },
            {
                "locale": "es_ES",
                "name": "My atributo de ejemplo",
                "infoUri": "https://website.es",
                "displayTexts": [
                    {"key": "loc.content.period",
                    "value": "%1$s - %2$s"},
                    {"key": "loc.label.start_date",
                    "value": "Start date"},
                    {"key": "loc.label.end_date",
                    "value": "End date"},
                    {"key": "loc.label.skills",
                    "value": "Skills"}
                ]
            }
        ]
    },
    "display": {
        "category": "employment",
        "compact": {
            "title": {
                "argv": [
                    "company_name"
                ]
            },
            "subtitle": {
                "argv": [
                    "job_title"
                ]
            },
            "extra": {
                "key": "loc.content.period",
                "argv": [
                    "start_date",
                    "end_date"
                ]
            }
        },
        "full": {
            "logo": {
                "argv": [
                    "company_logo"
                ]
            },
            "title": {
                "argv": [
                    "company_name"
                ]
            },
            "subtitle": {
                "argv": [
                    "job_title"
                ]
            },
            "items": [
                {
                    "label": "loc.label.start_date",
                    "argv": [
                        "start_date"
                    ]
                },
                {
                    "label": "loc.label.end_date",
                    "argv": [
                        "end_date"
                    ]
                },
                {
                    "label": "loc.label.skills",
                    "argv": [
                        "skills"
                    ]
                }
            ]
        },
        "argDefinitions": [
            {
                "id": "company_name",
                "paths": [
                    "$.myCredential.companyDetails.companyName"
                ],
                "schema": {
                    "type": "string"
                },
                "fallback": "loc.content.company_name_fallback"
            },
            {
                "id": "company_logo",
                "paths": [
                    "$.myCredential.companyDetails.companyLogo"
                ],
                "schema": {
                    "type": "string",
                    "format": "image/url"
                }
            },
            {
                "id": "job_title",
                "paths": [
                    "$.myCredential.employmentDetails.position"
                ],
                "schema": {
                    "type": "string"
                },
                "fallback": "loc.content.job_position_fallback"
            },
            {
                "id": "role_description",
                "paths": [
                    "$.myCredential.employmentDetails.description"
                ],
                "schema": {
                    "type": "string"
                },
                "fallback": "loc.content.role_description_fallback"
            },
            {
                "id": "start_date",
                "paths": [
                    "$.myCredential.employmentDetails.startDate"
                ],
                "schema": {
                    "type": "string",
                    "format": "date"
                }
            },
            {
                "id": "end_date",
                "paths": [
                    "$.myCredential.employmentDetails.endDate"
                ],
                "schema": {
                    "type": "string",
                    "format": "date"
                }
            },
            {
                "id": "skills",
                "paths": [
                    "$.myCredential.employmentDetails.skills"
                ],
                "schema": {
                    "type": "array_string"
                }
            }
        ]
    }
}
{% /tab %}
{% /code %}

### Issuance payload

The JSON payload for issuing the above credential would be the following:

{% code %}
{% tab language="json" %}
{
    "myCredential": {
        "companyDetails": {
            "companyName": "Amazon",
            "companyLogo": "www.amazon.com/logos/main_logo.jpeg"
        },
        "employmentDetails": {
            "position": "Android Engineer",
            "startDate": "2020-09-29",
            "endDate": "2022-03-12",
            "description": "An engineer that builds Android apps.",
            "place": "London, UK",
            "skills": [
                "kotlin",
                "java",
                "json",
                "gradle",
                "dagger"
            ]
        }
    }
}
{% /tab %}
{% /code %}