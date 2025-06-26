---
type: page
title: Supported documents
listed: true
slug: supported-documents
description: 
index_title: Supported documents
hidden: 
keywords: 
tags: 
---

Please see below for supported documents for our IDV service. 

This list can also be requested by API through the following endpoint:

{% code %}
{% tab language="http" %}
GET https://api.yoti.com/idverify/v1/supported-documents?includeNonLatin=true
{% /tab %}
{% /code %}

## Supported Document Types

The following document types are supported across various countries:

- Passport (universal)
- National ID
- Driving Licence
- Biometric Residence Permit (BRP)
- Citizencard (UK specific)
- Post Office card (UK specific)
- Young Scot National Entitlement Card (UK specific)
- Health Card (Canada specific)
- Provincial or territorial ID (Canada specific)
- Secure Certificate of Indian Status (SCIS) (Canada specific)
- NEXUS Card (Canada and USA specific)
- State ID (USA specific)
- Aadhaar card (India specific)
- PAN card (India specific)
- MyKad (Malaysia specific)
- PhilSys ID (Philippines specific)
- Postal ID (Philippines specific)
- Professional ID (Philippines specific)
- SSS ID Card (Philippines specific)
- UMID (Philippines specific)
- Voter ID (Philippines specific)

## Non Latin Documents

Yoti supports some non-latin character documents. These are not enabled by default but can be included on an opt in basis.

Yoti will attempt to perform automated text extraction only on these documents and a document authenticity check. We cannot perform manual data entry.

{% synced id="non-latin-documents-table" %}
{% /synced %}

## All documents

{% table %}
| Region | Issuing Country | Passport | National ID | Driving Licence | BRP | Other document type(s) | 
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | 
| South America | Aruba |  |  |  |  |  | 
| Asia | Afghanistan | X | X | X |  |  | 
| Africa | Angola | X | X | X |  |  | 
| North America & Caribbean | Anguilla | X |  |  |  |  | 
| Europe | Åland Islands |  |  |  |  |  | 
| Europe | Albania | X | X | X |  |  | 
| Europe | Andorra | X |  | X |  |  | 
| Asia | United Arab Emirates | X | X | X |  |  | 
| South America | Argentina | X | X | X |  |  | 
| Asia | Armenia | X | X | X |  |  | 
| Asia | American Samoa | X | X | X |  |  | 
| North America & Caribbean | Antigua and Barbuda | X |  |  |  |  | 
| Oceania | Australia | X |  | X |  |  | 
| Europe | Austria | X | X | X | X |  | 
| Asia | Azerbaijan | X | X | X |  |  | 
| Africa | Burundi | X |  |  |  |  | 
| Europe | Belgium | X | X | X | X |  | 
| Africa | Benin | X |  | X |  |  | 
| South America | Caribbean Netherlands |  |  |  |  |  | 
| Africa | Burkina Faso | X | X | X |  |  | 
| Asia | Bangladesh | X | X | X |  |  | 
| Europe | Bulgaria | X | X | X | X |  | 
| Asia | Bahrain | X | X | X |  |  | 
| North America & Caribbean | Bahamas | X |  | X |  |  | 
| Europe | Bosnia and Herzegovina | X | X | X |  |  | 
| South America | St. Barthélemy |  |  |  |  |  | 
| Europe | Belarus | X | X | X |  |  | 
| North America & Caribbean | Belize | X |  |  |  |  | 
| North America & Caribbean | Bermuda | X |  | X |  |  | 
| South America | Bolivia | X | X | X |  |  | 
| South America | Brazil | X | X | X |  |  | 
| North America & Caribbean | Barbados | X |  | X |  |  | 
| Asia | Brunei | X | X | X |  |  | 
| Asia | Bhutan | X | X |  |  |  | 
| Africa | Botswana | X | X | X |  |  | 
| Africa | Central African Republic | X |  | X |  |  | 
| North America & Caribbean | Canada | X | X | X | X | X | 
| Asia | Cocos (Keeling) Islands |  |  |  |  |  | 
| Europe | Switzerland | X | X | X | X |  | 
| South America | Chile | X | X |  |  |  | 
| Asia | China | X | X | X |  |  | 
| Africa | Ivory Coast Côte d'Ivoire | X | X | X |  |  | 
| Africa | Cameroon | X | X | X |  |  | 
| Africa | Democratic Republic of the Congo | X |  | X |  |  | 
| Africa | Republic of the Congo | X |  |  |  |  | 
| Asia | Cook Islands |  |  |  |  |  | 
| South America | Colombia | X | X | X | X |  | 
| Africa | Comoros | X | X |  |  |  | 
| Africa | Cape Verde | X | X | X |  |  | 
| North America & Caribbean | Costa Rica | X | X | X |  |  | 
| North America & Caribbean | Cuba | X |  | X |  |  | 
| South America | Curaçao |  |  |  |  |  | 
| Asia | Christmas Island |  |  |  |  |  | 
| North America & Caribbean | Cayman Islands | X |  |  |  |  | 
| Europe | Cyprus | X | X | X | X |  | 
| Europe | Czechia | X | X | X | X |  | 
| Europe | Germany | X | X | X | X |  | 
| Africa | Djibouti | X |  |  |  |  | 
| North America & Caribbean | Dominica | X |  |  |  |  | 
| Europe | Denmark | X |  | X | X |  | 
| North America & Caribbean | Dominican Republic | X | X | X |  |  | 
| Africa | Algeria | X | X | X |  |  | 
| South America | Ecuador | X | X | X |  |  | 
| Africa | Egypt | X | X |  |  |  | 
| Africa | Eritrea | X |  |  |  |  | 
| Africa | Western Sahara |  |  |  |  |  | 
| Europe | Spain | X | X | X | X |  | 
| Europe | Estonia | X | X | X | X |  | 
| Africa | Ethiopia | X | X | X |  |  | 
| Europe | Finland | X | X | X | X |  | 
| Oceania | Fiji | X |  | X |  |  | 
| South America | Falkland Islands |  |  |  |  |  | 
| Europe | France | X | X | X | X |  | 
| Europe | Faroe Islands | X |  |  |  |  | 
| Oceania | Micronesia | X |  |  |  |  | 
| Africa | Gabon | X | X |  |  |  | 
| Europe | United Kingdom | X |  | X | X | X | 
| Europe | Georgia | X | X | X |  |  | 
| Europe | Guernsey | X |  | X |  |  | 
| Africa | Ghana | X | X | X |  |  | 
| Europe | Gibraltar | X | X | X |  |  | 
| Africa | Guinea | X |  | X |  |  | 
| South America | Guadeloupe |  |  |  |  |  | 
| Africa | Gambia | X |  |  |  |  | 
| Africa | Guinea Bissau | X | X |  |  |  | 
| Africa | Equatorial Guinea | X |  |  |  |  | 
| Europe | Greece | X | X | X | X |  | 
| North America & Caribbean | Grenada | X |  |  |  |  | 
| North America & Caribbean | Greenland | X |  |  |  |  | 
| South America | Guatemala | X | X | X |  |  | 
| South America | French Guiana |  |  |  |  |  | 
| Asia | Guam | X | X | X |  |  | 
| South America | Guyana | X | X |  |  |  | 
| Asia | Hong Kong | X | X |  |  |  | 
| North America & Caribbean | Honduras | X | X | X |  |  | 
| Europe | Croatia | X | X | X | X |  | 
| North America & Caribbean | Haiti | X | X |  |  |  | 
| Europe | Hungary | X | X | X | X |  | 
| Asia | Indonesia | X | X | X |  |  | 
| Europe | Isle of Man | X |  | X |  |  | 
| Asia | India | X | X | X |  | X | 
| Asia | British Indian Ocean Territory |  |  |  |  |  | 
| Europe | Ireland | X | X | X | X |  | 
| Asia | Iran | X |  |  |  |  | 
| Asia | Iraq | X |  |  |  |  | 
| Europe | Iceland | X |  | X | X |  | 
| Asia | Israel | X | X | X |  |  | 
| Europe | Italy | X | X | X | X |  | 
| North America & Caribbean | Jamaica | X |  | X |  |  | 
| Europe | Jersey | X |  | X |  |  | 
| Asia | Jordan | X | X | X |  |  | 
| Asia | Japan | X | X | X |  |  | 
| Asia | Kazakhstan | X | X | X |  |  | 
| Africa | Kenya | X | X |  |  |  | 
| Asia | Kyrgyzstan | X | X | X |  |  | 
| Asia | Cambodia | X | X | X |  |  | 
| Oceania | Kiribati | X |  |  |  |  | 
| North America & Caribbean | Saint Kitts and Nevis | X |  |  |  |  | 
| Asia | South Korea | X |  |  |  |  | 
| Asia | Kuwait | X | X | X |  |  | 
| Asia | Laos | X |  |  |  |  | 
| Asia | Lebanon | X |  | X |  |  | 
| Africa | Liberia | X |  |  |  |  | 
| Africa | Libya | X |  | X |  |  | 
| North America & Caribbean | Saint Lucia | X | X |  |  |  | 
| Europe | Liechtenstein | X | X | X |  |  | 
| Asia | Sri Lanka | X | X | X |  |  | 
| Africa | Lesotho | X | X |  |  |  | 
| Europe | Lithuania | X | X | X | X |  | 
| Europe | Luxembourg | X | X | X | X |  | 
| Europe | Latvia | X | X | X | X |  | 
| Asia | Macau | X | X |  |  |  | 
| South America | St. Martin |  |  |  |  |  | 
| Africa | Morocco | X | X | X |  |  | 
| Europe | Monaco | X | X | X |  |  | 
| Europe | Moldova | X | X | X |  |  | 
| Africa | Madagascar | X |  | X |  |  | 
| Asia | Maldives | X |  |  |  |  | 
| North America & Caribbean | Mexico | X | X | X |  |  | 
| Oceania | Marshall Islands | X |  |  |  |  | 
| Europe | Macedonia | X | X | X |  |  | 
| Africa | Mali | X | X |  |  |  | 
| Europe | Malta | X | X | X | X |  | 
| Asia | Myanmar | X |  |  |  |  | 
| Europe | Montenegro | X | X | X |  |  | 
| Asia | Mongolia | X | X | X |  |  | 
| Asia | Northern Mariana Islands | X |  |  |  |  | 
| Africa | Mozambique | X | X |  |  |  | 
| Africa | Mauritania | X | X |  |  |  | 
| North America & Caribbean | Montserrat | X |  |  |  |  | 
| South America | Martinique |  |  |  |  |  | 
| Africa | Mauritius | X | X |  |  |  | 
| Africa | Malawi | X | X | X |  |  | 
| Asia | Malaysia | X |  | X |  | X | 
| Africa | Mayotte |  |  |  |  |  | 
| Africa | Namibia | X | X | X |  |  | 
| Asia | New Caledonia |  |  |  |  |  | 
| Africa | Niger | X |  |  |  |  | 
| Asia | Norfolk Island |  |  |  |  |  | 
| Africa | Nigeria | X | X | X |  |  | 
| North America & Caribbean | Nicaragua | X | X | X |  |  | 
| Asia | Niue |  |  |  |  |  | 
| Europe | Netherlands | X | X | X | X |  | 
| Europe | Norway | X | X | X | X |  | 
| Asia | Nepal | X |  | X |  |  | 
| Oceania | Nauru | X |  |  |  |  | 
| Oceania | New Zealand | X |  | X |  |  | 
| Arab States | Oman | X | X |  |  |  | 
| Asia | Pakistan | X | X |  |  |  | 
| North America & Caribbean | Panama | X | X | X |  |  | 
| South America | Peru | X | X | X |  |  | 
| Asia | Philippines | X |  | X |  | X | 
| Oceania | Palau | X |  |  |  |  | 
| Oceania | Papua New Guinea | X |  |  |  |  | 
| Europe | Poland | X | X | X | X |  | 
| South America | Puerto Rico | X | X | X |  |  | 
| Asia | North Korea | X |  |  |  |  | 
| Europe | Portugal | X | X | X | X |  | 
| South America | Paraguay | X | X | X |  |  | 
| Arab States | Palestine | X |  | X |  |  | 
| Asia | French Polynesia |  |  |  |  |  | 
| Asia | Qatar | X | X | X |  |  | 
| Asia | Réunion |  |  |  |  |  | 
| Europe | Romania | X | X | X | X |  | 
| Europe | Russia | X | X | X |  |  | 
| Africa | Rwanda | X | X | X |  |  | 
| Asia | Saudi Arabia | X |  | X |  |  | 
| Africa | Sudan | X |  |  |  |  | 
| Africa | Senegal | X | X | X |  |  | 
| Asia | Singapore | X | X | X |  |  | 
| Europe | St. Helena |  |  |  |  |  | 
| Asia | Ascension Island |  |  |  |  |  | 
| Africa | Tristan da Cunha |  |  |  |  |  | 
| Europe | Svalbard & Jan Mayen |  |  |  |  |  | 
| Oceania | Solomon Islands | X |  |  |  |  | 
| Africa | Sierra Leone | X | X | X |  |  | 
| South America | El Salvador | X | X | X |  |  | 
| Europe | San Marino | X | X | X |  |  | 
| Arab States | Somalia | X |  |  |  |  | 
| North America | St. Pierre & Miquelon |  |  |  |  |  | 
| Europe | Serbia | X | X | X |  |  | 
| Africa | South Sudan | X | X |  |  |  | 
| Africa | São Tomé and Príncipe | X |  |  |  |  | 
| South America | Suriname | X |  | X |  |  | 
| Europe | Slovakia | X | X | X | X |  | 
| Europe | Slovenia | X | X | X | X |  | 
| Europe | Sweden | X | X | X | X |  | 
| Africa | Swaziland | X |  |  |  |  | 
| South America | Sint Maarten |  |  |  |  |  | 
| Africa | Seychelles | X |  |  |  |  | 
| Asia | Syria | X |  |  |  |  | 
| North America & Caribbean | Turks and Caicos Islands | X |  |  |  |  | 
| Africa | Chad | X | X |  |  |  | 
| Africa | Togo | X |  | X |  |  | 
| Asia | Thailand | X | X | X |  |  | 
| Asia | Tajikistan | X | X | X |  |  | 
| Asia | Tokelau |  |  |  |  |  | 
| Asia | Turkmenistan | X |  | X |  |  | 
| Asia | East Timor | X | X |  |  |  | 
| Oceania | Tonga | X |  |  |  |  | 
| North America & Caribbean | Trinidad and Tobago | X |  | X |  |  | 
| Africa | Tunisia | X |  | X |  |  | 
| Asia | Turkey | X | X | X |  |  | 
| Oceania | Tuvalu | X |  |  |  |  | 
| Asia | Taiwan | X |  |  | X |  | 
| Africa | Tanzania | X | X | X |  |  | 
| Africa | Uganda | X | X | X |  |  | 
| Europe | Ukraine | X | X | X |  |  | 
| South America | Uruguay | X | X | X |  |  | 
| North America & Caribbean | United States | X |  | X |  | X | 
| Asia | Uzbekistan | X |  |  |  |  | 
| Europe | Vatican | X |  |  |  |  | 
| North America & Caribbean | Saint Vincent and the Grenadines | X |  |  |  |  | 
| South America | Venezuela | X | X | X |  |  | 
| North America & Caribbean | British Virgin Islands | X |  |  |  |  | 
| South America | U.S. Virgin Islands | X | X | X |  |  | 
| Asia | Vietnam | X | X | X |  |  | 
| Oceania | Vanuatu | X |  | X |  |  | 
| Asia | Wallis & Futuna |  |  |  |  |  | 
| Oceania | Samoa | X |  |  |  |  | 
| Europe | Kosovo | X | X | X |  |  | 
| Asia | Yemen | X |  | X |  |  | 
| Africa | South Africa | X | X | X |  |  | 
| Africa | Zambia | X |  | X |  |  | 
| Africa | Zimbabwe | X | X |  |  |  | 
{% /table %}