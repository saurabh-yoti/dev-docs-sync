---
type: page
title: Pooling
listed: false
slug: pooling
description: 
index_title: Pooling
hidden: 
keywords: 
tags: 
---

You can test multiple samples in a single well for RT-PCR and RT-LAMP tests by turning on the pooling feature. A settings page in Admin lets you toggle this feature. In order for a user to log in and access the settings area, they must be given access. Access is obtained by being given the **Settings** permission to the user’s account in user management. You must have the **Settings** permission to be able to set up pooling in the Yoti Testing Platform.

With pooling set to ON, all users who have permission to collect samples will be given the choice of collecting samples in a pool or individual test bag.

---

## Setting up pooling

1. Go to **Admin** and then select **Settings.**
2. Select **Testing** tab.

Under the testing tab, there is a switch to turn on and off pooling.

## Pooling in collection flow

With pooling set to ON, collectors will be asked if a customer can be added to a pool or if they require an individual test.

The collector is also told how many customers can be added to this pooled test bag.

{% image url="https://image-archive.developerhub.io/image/upload/73686/jbhi3evdl1tfoxpukeya/1605866800.png" mode="responsive" height="438" width="304" %}
{% /image %}

Collectors see this for every customer they collect, to ensure a returning customer requiring an individual test is not added to a pool test.

The confirmation collection screen provide different actions for pooling:

{% image url="https://image-archive.developerhub.io/image/upload/73686/kw0rvf8ijrveeqai8twg/1605870246.png" mode="responsive" height="702" width="345" %}
{% /image %}

### Confirm collection

The collector has collected and added the customer's sample, and is ready to add a new customer to this pooled test.

### Confirm & finish pool

The collector has collected and added the customer's sample, and is ready to close this pooled test and send it for testing.

### Cancel Nth collection

The collector needs to cancel adding the current customer to the pooled test. This dissociates the customer from the test and deletes their personal details from the Yoti Testing Platform.

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        If you add the customer's sample to a pooled test
    </div>
    <div class="alert-text">
      If you add a customer's sample to a pooled test, you must not cancel this customer's collection. If it was added in error, you will need to <strong>cancel the pool</strong>.  
        </div>
    <div class="alert-links"> 

</div>
{% /html %}

### Cancel pool

The collector needs to cancel the pooled test. This will invalidate the test and send an inconclusive test result to all customers added to this pooled test.