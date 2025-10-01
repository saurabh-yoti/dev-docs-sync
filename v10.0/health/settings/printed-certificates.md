---
type: page
title: Certificates
listed: true
slug: printed-certificates
description: 
index_title: Certificates
hidden: 
keywords: 
tags: 
---

Yoti has two types of certificates:

- Covid-19 test results certificate
- EU Digital Covid certificate - only available in Ireland.

Here you will have the ability to send a printed certificate a PDF certificate by email. You can turn this feature on by using the toggle. When ON, you can select the fields they wish to display in the certificate. If any field selected isn't actually being collected as part of the collection flow the user will see a notification and can choose to add it in the Data Collection field or not. If not, this field will be displayed empty in the certificate.

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/ar37rovpdn5om4guzdc8/1618428307.png" caption="Settings &gt; Printed certificate" mode="responsive" height="283" width="679" %}
{% /image %}

You will have the option to select fields to add to the certification and your organisation logo here too:

- Customer details
- Test details
- Medical details (report approved by)
- Authentication stamp / doctor signature. The image must be in jpeg or png format, under 500KB and size under 2000x2000.

You can preview the certificate template and download a copy to see what your users will receive:

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/w5ypghwgeyqwwq5ptfqs/1627286690.png" caption="Download certificate." mode="responsive" height="316" width="1022" %}
{% /image %}

The certificate will be sent via email to all customers, indifferent if they have used the Yoti App or the webform to share their details.

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/udppmzho2amqavurymec/1626955493.png" caption="Reporting &gt; Download print certificate" mode="responsive" height="800" width="1652" %}
{% /image %}

The certificate can also be downloaded by users with Reporting permissions by choosing the "Print certificate" option. The certificate will look along the lines of the document below:

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/uvlo4fnjlktunjikxy9c/1621353625.png" caption="Printed certificate" mode="responsive" height="860" width="1370" %}
{% /image %}

This QR code can be verified using our scanning platform. Head over [here](https://developers.yoti.com/health/certificates) for more information.

---

## EU digital covid certificate

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
Please contact us before using this feature so we can run a production test.</div>
   <div class="alert-links"> 
      <a  target="_self" href="https://support.yoti.com/yotisupport/s/contactsupport"> Contact us </a>
   </div>
</div>
{% /html %}

You can enable the EU digital covid certificate, this is only available for Ireland. 

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/gnttovk7b9dulawmszyy/1635495516.png" caption="Enable digital covid certificate" mode="responsive" height="563" width="1419" %}
{% /image %}

In order to use this certificate please ensure you have a supported LFT test and the following attributes ticked in the data collection tab:

- Given names
- Family name
- Date of birth.

You will receive a client ID and secret ID from [digitalcovidcerts.technical@per.gov.ie](mailto:digitalcovidcerts.technical@per.gov.ie).

The certificate will look along the lines of the document below:

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/bzhkshkokrlz30cf6rph/1635496375.png" mode="responsive" height="1766" width="1501" %}
{% /image %}

To verify your certificate you can head over [here](https://app.digitalcovidcertchecker.gov.ie/).