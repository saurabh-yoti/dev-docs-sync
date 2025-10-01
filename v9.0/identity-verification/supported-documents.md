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
- Residence Permit
- CitizenCard (UK specific)
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

{% table %}
| Type | Countries | 
| ---- | ---- | 
| Driving Licence | China, Iraq, Japan, South Korea, Syria | 
| National ID | China, Egypt, Iran, Israel, Japan, Kazakhstan, Lebanon, Russia, Saudi Arabia, South Korea, Syria, Tunisia, Taiwan | 
| Residence Permit | Saudi Arabia | 
{% /table %}


## All documents

{% table %}
| Issuing Country | Country Code | Passport | National ID | Driving Licence | Residence Permit | Travel Document | Other document type(s) | 
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | 
| Afghanistan | AFG | X | X | X |  | X |  | 
| Angola | AGO | X | X | X |  | X |  | 
| Anguilla | AIA | X |  |  |  | X |  | 
| Albania | ALB | X | X | X |  | X |  | 
| Andorra | AND | X |  | X | X | X |  | 
| United Arab Emirates | ARE | X | X | X | X | X |  | 
| Argentina | ARG | X | X | X |  | X |  | 
| Armenia | ARM | X | X | X |  | X |  | 
| American Samoa | ASM | X | X | X |  | X |  | 
| Antigua and Barbuda | ATG | X |  |  |  | X |  | 
| Australia | AUS | X | X | X | X | X |  | 
| Austria | AUT | X | X | X | X | X |  | 
| Azerbaijan | AZE | X | X | X |  | X |  | 
| Burundi | BDI | X |  |  |  | X |  | 
| Belgium | BEL | X | X | X | X | X |  | 
| Benin | BEN | X |  | X |  | X |  | 
| Burkina Faso | BFA | X | X | X |  | X |  | 
| Bangladesh | BGD | X | X | X |  | X |  | 
| Bulgaria | BGR | X | X | X | X | X |  | 
| Bahrain | BHR | X | X | X |  | X |  | 
| Bahamas | BHS | X |  | X |  | X |  | 
| Bosnia and Herzegovina | BIH | X | X | X |  | X |  | 
| Belarus | BLR | X | X | X | X | X |  | 
| Belize | BLZ | X |  |  |  | X |  | 
| Bermuda | BMU | X |  | X |  | X |  | 
| Bolivia, Plurinational State of | BOL | X | X | X |  | X |  | 
| Brazil | BRA | X | X | X | X | X |  | 
| Barbados | BRB | X |  | X |  | X |  | 
| Brunei Darussalam | BRN | X | X | X |  | X |  | 
| Bhutan | BTN | X | X |  |  | X |  | 
| Botswana | BWA | X | X | X |  | X |  | 
| Central African Republic | CAF | X |  | X |  | X |  | 
| Canada | CAN | X | X | X | X | X | X | 
| Switzerland | CHE | X | X | X | X | X |  | 
| Chile | CHL | X | X |  |  | X |  | 
| China | CHN | X | X | X |  | X |  | 
| Côte d'Ivoire | CIV | X | X | X |  | X |  | 
| Cameroon | CMR | X | X | X |  | X |  | 
| Congo, Democratic Republic of the | COD | X |  | X |  | X |  | 
| Congo | COG | X |  |  |  | X |  | 
| Colombia | COL | X | X | X | X | X |  | 
| Comoros | COM | X | X |  |  | X |  | 
| Cabo Verde | CPV | X | X | X |  | X |  | 
| Costa Rica | CRI | X | X | X |  | X |  | 
| Cuba | CUB | X | X | X |  | X |  | 
| Cayman Islands | CYM | X |  | X |  | X |  | 
| Cyprus | CYP | X | X | X | X | X |  | 
| Czechia | CZE | X | X | X | X | X |  | 
| Germany | DEU | X | X | X | X | X |  | 
| Djibouti | DJI | X | X |  |  | X |  | 
| Dominica | DMA | X |  |  |  | X |  | 
| Denmark | DNK | X |  | X | X | X |  | 
| Dominican Republic | DOM | X | X | X |  | X |  | 
| Algeria | DZA | X | X | X |  | X |  | 
| Ecuador | ECU | X | X | X |  | X |  | 
| Egypt | EGY | X | X |  | X | X |  | 
| Eritrea | ERI | X |  |  |  | X |  | 
| Spain | ESP | X | X | X | X | X |  | 
| Estonia | EST | X | X | X | X | X |  | 
| Ethiopia | ETH | X | X | X |  | X |  | 
| Finland | FIN | X | X | X | X | X |  | 
| Fiji | FJI | X |  | X |  | X |  | 
| France | FRA | X | X | X | X | X |  | 
| Faroe Islands | FRO | X |  | X |  | X |  | 
| Micronesia, Federated States of | FSM | X |  |  |  | X |  | 
| Gabon | GAB | X | X |  |  | X |  | 
| United Kingdom of Great Britain and Northern Ireland | GBR | X |  | X | X | X | X | 
| Georgia | GEO | X | X | X | X | X |  | 
| Guernsey | GGY | X |  | X |  | X |  | 
| Ghana | GHA | X | X | X |  | X |  | 
| Gibraltar | GIB | X | X | X |  | X |  | 
| Guinea | GIN | X | X | X |  | X |  | 
| Gambia | GMB | X | X |  |  | X |  | 
| Guinea-Bissau | GNB | X | X |  |  | X |  | 
| Equatorial Guinea | GNQ | X |  |  |  | X |  | 
| Greece | GRC | X | X | X | X | X |  | 
| Grenada | GRD | X |  |  |  | X |  | 
| Greenland | GRL | X |  |  |  | X |  | 
| Guatemala | GTM | X | X | X |  | X |  | 
| Guam | GUM | X | X | X |  | X |  | 
| Guyana | GUY | X | X |  |  | X |  | 
| Hong Kong | HKG | X | X |  |  | X |  | 
| Honduras | HND | X | X | X |  | X |  | 
| Croatia | HRV | X | X | X | X | X |  | 
| Haiti | HTI | X | X |  |  | X |  | 
| Hungary | HUN | X | X | X | X | X |  | 
| Indonesia | IDN | X | X | X |  | X |  | 
| Isle of Man | IMN | X |  | X |  | X |  | 
| India | IND | X |  | X |  | X | X | 
| Ireland | IRL | X | X | X | X | X |  | 
| Iran, Islamic Republic of | IRN | X | X |  |  | X |  | 
| Iraq | IRQ | X | X | X |  | X |  | 
| Iceland | ISL | X | X | X | X | X |  | 
| Israel | ISR | X | X | X |  | X |  | 
| Italy | ITA | X | X | X | X | X |  | 
| Jamaica | JAM | X |  | X |  | X |  | 
| Jersey | JEY | X |  | X |  | X |  | 
| Jordan | JOR | X | X | X |  | X |  | 
| Japan | JPN | X | X | X | X | X |  | 
| Kazakhstan | KAZ | X | X | X |  | X |  | 
| Kenya | KEN | X | X |  |  | X |  | 
| Kyrgyzstan | KGZ | X | X | X |  | X |  | 
| Cambodia | KHM | X | X | X |  | X |  | 
| Kiribati | KIR | X |  |  |  | X |  | 
| Saint Kitts and Nevis | KNA | X |  |  |  | X |  | 
| Korea, Republic of | KOR | X | X | X |  | X |  | 
| Kuwait | KWT | X | X | X |  | X |  | 
| Lao People's Democratic Republic | LAO | X |  |  |  | X |  | 
| Lebanon | LBN | X | X | X | X | X |  | 
| Liberia | LBR | X |  |  |  | X |  | 
| Libya | LBY | X |  | X |  | X |  | 
| Saint Lucia | LCA | X | X |  |  | X |  | 
| Liechtenstein | LIE | X | X | X | X | X |  | 
| Sri Lanka | LKA | X | X | X |  | X |  | 
| Lesotho | LSO | X | X |  |  | X |  | 
| Lithuania | LTU | X | X | X | X | X |  | 
| Luxembourg | LUX | X | X | X | X | X |  | 
| Latvia | LVA | X | X | X | X | X |  | 
| Macao | MAC | X | X |  | X | X |  | 
| Morocco | MAR | X | X | X | X | X |  | 
| Monaco | MCO | X | X | X |  | X |  | 
| Moldova, Republic of | MDA | X | X | X | X | X |  | 
| Madagascar | MDG | X |  | X |  | X |  | 
| Maldives | MDV | X |  |  |  | X |  | 
| Mexico | MEX | X | X | X |  | X |  | 
| Marshall Islands | MHL | X |  |  |  | X |  | 
| North Macedonia | MKD | X | X | X |  | X |  | 
| Mali | MLI | X | X |  |  | X |  | 
| Malta | MLT | X | X | X | X | X |  | 
| Myanmar | MMR | X |  |  |  | X |  | 
| Montenegro | MNE | X | X | X |  | X |  | 
| Mongolia | MNG | X | X | X |  | X |  | 
| Northern Mariana Islands | MNP | X |  |  |  | X |  | 
| Mozambique | MOZ | X | X |  |  | X |  | 
| Mauritania | MRT | X | X |  |  | X |  | 
| Montserrat | MSR | X |  |  |  | X |  | 
| Mauritius | MUS | X | X |  |  | X |  | 
| Malawi | MWI | X | X | X |  | X |  | 
| Malaysia | MYS | X |  | X |  | X | X | 
| Namibia | NAM | X | X | X |  | X |  | 
| Niger | NER | X |  |  |  | X |  | 
| Nigeria | NGA | X | X | X |  | X |  | 
| Nicaragua | NIC | X | X | X |  | X |  | 
| Netherlands, Kingdom of the | NLD | X | X | X | X | X |  | 
| Norway | NOR | X | X | X | X | X |  | 
| Nepal | NPL | X | X | X |  | X |  | 
| Nauru | NRU | X |  |  |  | X |  | 
| New Zealand | NZL | X |  | X |  | X |  | 
| Oman | OMN | X | X |  | X | X |  | 
| Pakistan | PAK | X | X |  |  | X |  | 
| Panama | PAN | X | X | X |  | X |  | 
| Peru | PER | X | X | X | X | X |  | 
| Philippines | PHL | X |  | X |  | X | X | 
| Palau | PLW | X |  |  |  | X |  | 
| Papua New Guinea | PNG | X |  |  |  | X |  | 
| Poland | POL | X | X | X | X | X |  | 
| Puerto Rico | PRI | X | X | X |  | X |  | 
| Korea, Democratic People's Republic of | PRK | X |  |  |  | X |  | 
| Portugal | PRT | X | X | X | X | X |  | 
| Paraguay | PRY | X | X | X |  | X |  | 
| Palestine, State of | PSE | X |  | X |  | X |  | 
| Qatar | QAT | X | X | X | X | X |  | 
| Romania | ROU | X | X | X | X | X |  | 
| Russian Federation | RUS | X | X | X |  | X |  | 
| Rwanda | RWA | X | X | X |  | X |  | 
| Saudi Arabia | SAU | X | X | X | X | X |  | 
| Sudan | SDN | X |  |  |  | X |  | 
| Senegal | SEN | X | X | X |  | X |  | 
| Singapore | SGP | X | X | X | X | X |  | 
| Solomon Islands | SLB | X |  |  |  | X |  | 
| Sierra Leone | SLE | X | X | X |  | X |  | 
| El Salvador | SLV | X | X | X |  | X |  | 
| San Marino | SMR | X | X | X |  | X |  | 
| Somalia | SOM | X | X |  |  | X |  | 
| Serbia | SRB | X | X | X |  | X |  | 
| South Sudan | SSD | X | X |  |  | X |  | 
| Sao Tome and Principe | STP | X |  |  |  | X |  | 
| Suriname | SUR | X | X | X |  | X |  | 
| Slovakia | SVK | X | X | X | X | X |  | 
| Slovenia | SVN | X | X | X | X | X |  | 
| Sweden | SWE | X | X | X | X | X |  | 
| Eswatini | SWZ | X |  |  |  | X |  | 
| Seychelles | SYC | X |  |  |  | X |  | 
| Syrian Arab Republic | SYR | X | X | X |  | X |  | 
| Turks and Caicos Islands | TCA | X |  |  |  | X |  | 
| Chad | TCD | X | X |  |  | X |  | 
| Togo | TGO | X |  | X |  | X |  | 
| Thailand | THA | X | X | X |  | X |  | 
| Tajikistan | TJK | X | X | X |  | X |  | 
| Turkmenistan | TKM | X |  | X |  | X |  | 
| Timor-Leste | TLS | X | X |  |  | X |  | 
| Tonga | TON | X |  |  |  | X |  | 
| Trinidad and Tobago | TTO | X | X | X |  | X |  | 
| Tunisia | TUN | X | X | X |  | X |  | 
| Türkiye | TUR | X | X | X | X | X |  | 
| Tuvalu | TUV | X |  |  |  | X |  | 
| Taiwan, Province of China | TWN | X | X |  | X | X |  | 
| Tanzania, United Republic of | TZA | X | X | X |  | X |  | 
| Uganda | UGA | X | X | X |  | X |  | 
| Ukraine | UKR | X | X | X | X | X |  | 
| Uruguay | URY | X | X | X |  | X |  | 
| United States of America | USA | X | X | X | X | X | X | 
| Uzbekistan | UZB | X | X | X |  | X |  | 
| Holy See | VAT | X |  |  |  | X |  | 
| Saint Vincent and the Grenadines | VCT | X |  |  |  | X |  | 
| Venezuela, Bolivarian Republic of | VEN | X | X | X |  | X |  | 
| Virgin Islands (British) | VGB | X |  |  |  | X |  | 
| Virgin Islands (U.S.) | VIR | X | X | X |  | X |  | 
| Viet Nam | VNM | X | X | X |  | X |  | 
| Vanuatu | VUT | X |  | X |  | X |  | 
| Samoa | WSM | X |  |  |  | X |  | 
| Kosovo | XKX | X | X | X | X | X |  | 
| Yemen | YEM | X |  | X |  | X |  | 
| South Africa | ZAF | X | X | X |  | X |  | 
| Zambia | ZMB | X |  | X |  | X |  | 
| Zimbabwe | ZWE | X | X |  |  | X |  | 
{% /table %}
