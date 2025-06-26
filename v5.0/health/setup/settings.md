---
type: page
title: Settings
listed: true
slug: settings
description: 
index_title: Settings
hidden: 
keywords: 
tags: 
---

Here you will select your preferences for:

- Organisation details
- localisation 
- Data retention
- Data collection
- Results
- Printed certificate option
- API settings

To go to your settings click on the hamburger menu, click **Admin** and **Settings**.

---

## General

Your organisation details will be on this tab. You shouldn't need to change anything here.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1626954910/v2_2762/oh5gp30ucxayhfphub5z.png" caption="Settings &gt; General" mode="responsive" height="556" width="890" %}
{% /image %}

{% table widths="232" %}
| General settings | Description | 
| ---- | ---- | 
| Organisation name | This is the name of your organisation that is displayed so that customers know who is issuing or processing their test. It's displayed in:\n\n\n\n- Customer's test credential in their Yoti app\n- Customer's test result email | 
| Organisation short name | This short name forms part of the Verifiable Credential Issuer, which is used to identify who issued a credential. Maximum of 10 characters allowed. Must be all lowercase. | 
| Organisation address | This is your organisations address. | 
| Organisation email | An email address of a contact / representative from your organisation. | 
| Phone | A phone number of a contact / representative from your organisation. | 
| Localisation | You can change the language used in the web application, including user and customer emails:\n\n\n\n- English (UK)\n- Czech (CZE)\n- Polish (PL) | 
{% /table %}

You can also add your organisation logo to the portal.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1621278701/v2_2762/wf5q76u5tqkiwnw9rciu.png" caption="Settings &gt; General&gt; Logo upload" mode="responsive" height="295" width="553" %}
{% /image %}

---

## Data retention

Here you will manage how you store your customer testing data in the portal.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1623419793/v2_2762/mkidozjdgm7giwpahev9.png" caption="Settings &gt; Data Retention" mode="responsive" height="686" width="1862" %}
{% /image %}

{% table widths="294" %}
| Data retention settings | Description | 
| ---- | ---- | 
| Keep data in application | All data will remain encrypted on Yoti’s servers in the UK. | 
| Delete all data for results to users | Delete all data relating to a customer once they receive their result.\n\n\n\n{% badge type="info" text="Hint" /%} You will not be able to download data from the reporting area. | 
| Delete all customer personally identifiable information after 30 days | Delete all data relating to a customer 30 days after collection. | 
{% /table %}

---

## Data collection

You can configure what additional personal information you request when a customer gets tested. You can select a mix of attributes from Yoti app and online form for customers to fill in to suit your business needs.

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Good to know
    </div>
    <div class="alert-text">
Customers should provide as little personal information to be able to get tested. That’s why by default, Yoti customers only share their photo and Remember Me ID. Remember me ID is a unique identifier to differentiate between users.
    </div>
    <div class="alert-links"> 

   </div>
</div>
{% /html %}

{% table widths="269,0" %}
| Data | Yoti App | Online form | 
| ---- | ---- | ---- | 
| Remember me ID. \n\nA unique identifier. | ✅ | ❌ | 
| Photo | ✅ | ❌ | 
| Name | ✅ | ✅ | 
| Email address | This is mandatory. | This is mandatory. | 
| Phone number | ✅ | ✅ | 
| Date of birth | ✅ | ✅ | 
| Address | ✅ | ✅ | 
| Gender | ✅ | ✅ | 
| Nationality | ✅ | ✅ | 
| Document details. Including document number, issuing country and date of expiry. | ✅ | ✅ | 
{% /table %}

### Other details

{% table widths="320,0" %}
| Data | Yoti App | Online form | 
| ---- | ---- | ---- | 
| Health number | ❌ | ✅ | 
| Staying address | ❌ | ✅ | 
| Date of arrival | ❌ | ✅ | 
| Country or territory you are travelling from | ❌ | ✅ | 
| Countries or territories you have been in as part of the journey | ❌ | ✅ | 
| Flight number, train service, or ship name | ❌ | ✅ | 
| Date you last departed or transitioned through a non-exempt country, territory or region. | ❌ | ✅ | 
| Ethnicity | ❌ | ✅ | 
| Vaccination status | ❌ | ✅ | 
{% /table %}

### Symptom questionnaire

You can add a supplementary questionnaire enabling a collector to record any symptoms that the customer wishes to disclose. This information does not affect the outcome of a customer’s test and a customer has the choice to skip it.

{% table %}
| Information | Description | 
| ---- | ---- | 
| Symptoms | To capture what symptoms customers think they have at the point of taking a test. A symptom analysis report can provide further insight on regional and organisational test results.\n\n\n\n- Fever\n- New persistent dry cough\n- Fatigue\n- Loss of sense of smell/taste\n- Sore throat\n- Aching joints\n- Nasal congestion\n- Shortness of breath\n- Diarrhoea\n- Skin rash\n- Temperature reading (ºC) | 
| Temperature in ºC | If the business desires, the customer's temperature can be taken and recorded by the collector in addition to the swab test. | 
{% /table %}

### Test and release

If Test and Release is selected, the customer will receive an email following PHE template with guidance on self-isolation according to their test result.

If you toggle this feature, when you are in the collection flow you will see the option to click test and release. 

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1626959458/v2_2762/zm9npugdgbfqyqcs3qny.png" caption="Test and release option on collection flow" mode="300" height="1520" width="822" %}
{% /image %}

An example of the email sent to users is shown below:

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1626959718/v2_2762/vpxx9dlfoyfhdeack21u.png" caption="Example email for test and release" mode="responsive" height="559" width="1412" %}
{% /image %}

Head over here to see how to [send results. ](https://developers.yoti.com/health/results#issuing-results)

### Pre-registration

In order to expedite the Collection flow, you may choose to allow your customer to pre-register. If this option is enabled, you will be able to upload your customer's details via a csv file in the **Customer data** tab in **Admin**. You must have the **Customer data** permission to be able to access the **Customer data** area.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1612956284/v2_2762/uanaw7gbadtwmxih9zlq.png" mode="responsive" height="436" width="374" %}
{% /image %}

The csv should contain all the data you require from your customers, as per the [template](https://www.yoti.com/wp-content/uploads/Pre-registration-template.csv) displayed under. Once the customer has been tested, their details will be removed from the database where they were stored.

{% badge type="info" text="Hint" /%} Pre-registration does not support test to release.

### Self-registration

Yoti has implemented a feature which allows you to generate a custom made URL. This allows all your users to fill in their details prior to arriving at the testing site. 

The user will receive a confirmation number which they must bring with them to the site. 

If you enable this feature you will need to provide your:

- Privacy URL
- Terms and conditions URL (optional)

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1626960512/v2_2762/ahw4spw1cvgbl8yhjmlq.png" caption="Self registration toggle" mode="responsive" height="686" width="603" %}
{% /image %}

The custom made URL will look like this:

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1626960732/v2_2762/wuujh0xjgw2llmo68meb.png" caption="Self registration URL landing page" mode="responsive" height="805" width="954" %}
{% /image %}

The user will press **select** and will fill in their details and receive the following email:

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1626960975/v2_2762/yzdmbwqp5vmrd9sp6erq.png" mode="responsive" height="527" width="712" %}
{% /image %}

When the customer comes on site and you start collecting, after adding their Bag ID if you click **pre-registered**, you can enter their registration number and all their details should populate. 

### Customer guides

If you would like to use our helpful guide that you can send to your customers prior to arriving to be tested, you can download this from the portal or [here](https://www.yoti.com/wp-content/uploads/Receiving-your-test-results-with-GeneMe-and-Yoti.pdf).

---

## Results

You can control when you want to issue test results to your customers. A held results page helps you manage and manually take actions on held results. 

Under the results tab, there are two options available for issuing results:

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1618428396/v2_2762/ain7hc1txsqts8jp78hb.png" caption="Settings &gt; Results" mode="responsive" height="472" width="1296" %}
{% /image %}

{% table %}
| Results settings | Description | 
| ---- | ---- | 
| Automatically | By default, customers who have linked their test to their Yoti app or an email address, will automatically receive their test result, regardless of the result outcome. | 
| Hold results | Customers who have been tested will not automatically receive their result, enabling you to divulge a customer’s result at a more appropriate time. You can choose which result outcomes you would like to hold for review:\n\n\n\n- Hold negative results\n- Hold positive results\n- Hold inconclusive results\n\n\nPlease note that expiry timelines still apply even if you choose to hold results. A held result is automatically sent an inconclusive result if held for longer than the expiry time defined by your chosen sample collection kit.\n\n\n\nThe quicker you act on this, the less time your customers will need to wait to receive their test result.\n\n\n\nCustomers that are held for more than the defined expiry duration will automatically receive an inconclusive test result, and will be required to return and be tested again.\n\n\n\nExpired test results are automatically removed from the held results table. | 
{% /table %}

The last part of this section is to edit CQ value or add external results.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1615827413/v2_2762/udlypzwghy92xvjcxoyu.png" caption="Settings &gt; Results" mode="responsive" height="458" width="610" %}
{% /image %}

{% html %}
<div class="alert-API">
    <div class="alert-title" id="API">
         <i _ngcontent-cvo-c21="" class="fas fa-external-link-alt" style="margin-left: -35px; margin-right: 15px"></i>  
      API Link
    </div>
    <div class="alert-text">
      Yoti has created an API endpoint allowing you to retrieve the results of the tests performed within your organisation. 
    </div>
    <div class="alert-links"> 
        <a href="https://developers.yoti.com/health/integration-guide">API integration</a>
    </div>
</div>
{% /html %}

---

## Printed certificate

Here you will have the ability to send a printed certificate a PDF certificate by email. You can turn this feature on by using the toggle. When ON, you can select the fields they wish to display in the certificate. If any field selected isn't actually being collected as part of the collection flow the user will see a notification and can choose to add it in the Data Collection field or not. If not, this field will be displayed empty in the certificate.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1618428307/v2_2762/ar37rovpdn5om4guzdc8.png" caption="Settings &gt; Printed certificate" mode="responsive" height="283" width="679" %}
{% /image %}

You will have the option to select fields to add to the certification and your organisation logo here too:

- Customer details
- Test details
- Medical details (report approved by)
- Authentication stamp / doctor signature. The image must be in jpeg or png format, under 500KB and size under 2000x2000.

You can preview the certificate template and download a copy to see what your users will receive:

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1627286690/v2_2762/w5ypghwgeyqwwq5ptfqs.png" caption="Download certificate." mode="responsive" height="316" width="1022" %}
{% /image %}

The certificate will be sent via email to all customers, indifferent if they have used the Yoti App or the webform to share their details.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1626955493/v2_2762/udppmzho2amqavurymec.png" caption="Reporting &gt; Download print certificate" mode="responsive" height="800" width="1652" %}
{% /image %}

The certificate can also be downloaded by users with Reporting permissions by choosing the "Print certificate" option. The certificate will look along the lines of the document below:

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1621353625/v2_2762/uvlo4fnjlktunjikxy9c.png" caption="Printed certificate" mode="responsive" height="860" width="1370" %}
{% /image %}

This QR code can be verified using our scanning platform. Head over [here](https://developers.yoti.com/health/certificates) for more information.