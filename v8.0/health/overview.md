---
type: page
title: Overview
listed: true
slug: overview
description: 
index_title: Overview
hidden: 
keywords: 
tags: 
---

Welcome to the documentation for using the Health testing service. Individuals can have their test results directly issued to their phone via the Yoti app, where their information is securely stored as encrypted data that only they can unlock. Users can use the app to securely share their test results, both in person and digitally.

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
Contact us to get you onboard.  </div>
   <div class="alert-links"> 
      <a  target="_self" href="mailto:clientsupport@yoti.com"> Onboard with us </a>
   </div>
</div>
{% /html %}

This service is offered as a portal, however Yoti has created an [API](https://developers.yoti.com/health/integration-guide) to allow you to retrieve your user’s test results and personal details.

The overview below sets out the entities and data flows involved.

{% badge type="warning" text="Help" /%} If you need any help please contact us [here](https://yoti.force.com/yotisupport/s/contactsupport).

---

### Supported browsers

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1615974256/v2_2762/kflkqvip7po9tkohzh6v.png" caption="Supported browsers" mode="600" height="972" width="1154" %}
{% /image %}

---

## Hardware requirements

- Please ensure your devices have cameras. 
- You may need an ethernet port or appropriate USB ethernet adaptor to be able to connect to your testing machine.

---

## Feature list

The health portal has many features please see overview below:

{% table %}
| Feature | Description | 
| ---- | ---- | 
| Data retention | Choose how you store the data. | 
| Symptom questionnaire | Capture what symptoms customers think they have at the point of taking a test. | 
| Test and release | The customer will receive an email with a PHE template containing guidance on self-isolation according to their test result | 
| Pre-registration | Allow your customers to pre-register by uploading a CSV. | 
| Self-registration | Generate a custom made URL so all your users to fill in their details prior to arriving at the testing site. | 
| Held results | Manage and manually take actions on held results. | 
| Edit CQ Value | Enable ability to edit CQ values on the upload test results page. | 
| Printed certificate | Send a printed certificate a PDF certificate by email | 
| Verify printed certificate | A QR code scanner to give a simple and secure way to verify that credentials are presented by their rightful owner. | 
| Yoti | Ask your customers to use Yoti to ensure you are dealing with verified users. | 
| Reporting | Track and analyse all of your test results | 
| Customer guides | Free auto generated customer guides. | 
{% /table %}

### Translations supported

Available translation languages for customer emails and collection flow:

- Czech (čeština) 🇨🇿
- Polish (Polskie) 🇵🇱

---

## Technical overview

Yoti supports two types of testing:

- RT-PCR & RT-LAMP testing
- Lateral flow testing. 

There are 4 personas:

1. The customer. The user that is performing the swab / test. 
2. The collector. The user that will be processing the results. 
3. The technician. The user that will be dealing with the machines.
4. The admin. The owner of the portal.

The process flows for sample collection is shown below:

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1618430123/v2_2762/dfbruu4fjcygqlqkxfza.png" caption="Technical overview" mode="600" height="574" width="863" %}
{% /image %}

The process flows for test results is shown below:

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1618430177/v2_2762/vvka8eolzg0e1bu9gymd.png" caption="Technical overview" mode="600" height="574" width="663" %}
{% /image %}

---

## The customer flow

Below details the end to end customer flow for RT-PCR & RT-LAMP testing.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1615974452/v2_2762/v7b2bqiyv7m5gkoiwth9.png" caption="RT-PCR & RT-LAMP testing customer flow" mode="responsive" height="604" width="1014" %}
{% /image %}

1. The collector links a customer to a testing bag via Yoti or email.
2. The sample is collected from the customer.
3. The customer can choose to submit an optional symptom questionnaire. This can be configured on or off. 
4. A technician assigns the customer sample to digital well, linking the customer to the real well in the testing plate.
5. A technician places the testing plate to the machine and runs the test.
6. Results are then uploaded to the portal and are automatically sent to customers.
7. The customer receives their test result in their Yoti app or via email.

Below details the end to end customer flow for lateral testing.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1615974600/v2_2762/ffap1wg3zhjvx3dczmhq.png" caption="Lateral testing customer flow" mode="responsive" height="610" width="992" %}
{% /image %}

1. The collector links a customer to a testing bag via Yoti or email.
2. The sample is collected from the customer.
3. The customer can choose to submit a symptom questionnaire. This can be configured on or off. 
4. The technician scans the test, allocating the customer to a number. Numbered cards on the screen show a countdown timer for each test.
5. The technician is notified to check for a result at the optimum time for each test.
6. The result is submitted to the portal and is sent to the customer.
7. The customer receives their test result in their Yoti app or via email.

---

## Using Yoti responsibly

We pride ourselves on how we handle our users' data. We use tech for good and enable users to securely prove their identity or age, always being transparent about what happens to their details.

- Be transparent about why you're collecting data and only use this data for those reasons.
- Only collect the information you actually need. Data minimisation is one of the main benefits of Yoti, so people don't have to provide more information than is actually necessary.
- Make sure any information you export to your own systems is stored securely. Data security is at the heart of what we do and we think it should be important to every organisation.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1575299497/20473/vwj6x1hjvfni5rzvlho3.jpg" mode="300" height="440" width="438" %}
{% /image %}