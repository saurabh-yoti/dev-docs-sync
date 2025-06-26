---
type: page
title: Branding object
listed: true
slug: branding-object
description: 
index_title: Branding object
hidden: 
keywords: 
tags: 
---

This section is only applicable for the embedded envelope flow. You can customise the embedded flow to add your own branding.

{% code %}
{% tab language="json" %}
"branding":
    {
        "logo_options":
        {
            "logo_choice": "brand_powered_by_yoti",
            "logo_base64": "base64-encoded-PNG-image"
        },
        "primary_color": "#000",
        "primary_color_hover": "#c0c0c0",
        "on_primary_color": "#fff",
        "secondary_color": "#00ffff",
        "secondary_color_hover": "#d2691e"
    }
{% /tab %}
{% /code %}

---

## logo_choice

This must be one of the following:

- `brand_powered_by_yoti`
- `powered_by_yoti`
- `no_logo`
- `yoti_sign -`This is the default value if branding JSON is provided, but nothing is specified for this field.

---

## logo_base64

This must be a base64 encoded PNG image less than or equal to 200kb. If this is not specified, the stored organisation logo will be used.

---

## primary_color

This is the button colour.

{% image url="https://uploads.developerhub.io/prod/kvAX/bq0qa88ny1ly5dy65pc43wpwbny44gwcx94rs2tzoa1d21b1gr7ud6spk9e5ljoj.png" mode="responsive" height="778" width="1412" %}
{% /image %}

---

## primary_color_hover

This is the colour when you hover over the button.

{% image url="https://uploads.developerhub.io/prod/kvAX/bx8hflcvalugjjh8auk1zxs0p8jfqjbv1wec2qagdhlgpt9f7qqlbvwxjbk8j4lp.png" mode="responsive" height="794" width="1422" %}
{% /image %}

---

## on_primary_color

Text colour on the buttons.

---

## secondary_color

Colour of the button on the signing confirmation page.

{% image url="https://uploads.developerhub.io/prod/kvAX/4mwe214ttjkylw3lcxo9tsqe8x62e1vxhn3a0l1mq6g8wbwq9rdb3jw17evikvli.png" mode="responsive" height="778" width="1414" %}
{% /image %}

---

## secondary_color_hover

This is the colour when you hover over the button on the signing confirmation page.