---
type: page
title: Lateral Flow Testing
listed: true
slug: LFT-testing
description: 
index_title: Lateral Flow Testing
hidden: 
keywords: 
tags: 
---

The second stage of a Lateral Flow Test (LFT) is to process the collected sample. The sample is brought to a test inputter who registers the test to their testing session. Once the test shows a result, the test inputter registers the result in the Yoti Testing Platform, which automatically sends the result to the customer via their Yoti app or email.

## 1. Start testing session

Open your web browser and go to [**https://frankd.yoti.com/iam/login**](https://frankd.yoti.com/iam/login)

Use your Yoti app or email address and password to log in. Note: It is always more secure to log in using your Yoti app.

From the dashboard, select **Start testing** to begin a testing session.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1605622791/73687/ir2sels0akkshawkti0p.png" mode="300" height="297" width="268" %}
{% /image %}

## 2. Select LFT test type

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1609936508/73687/dqbbszn1r1tk28sanebt.png" mode="responsive" height="903" width="1435" %}
{% /image %}

## 3. Set up your testing session

{% html %}
<div class="alert-GTK">
    <div class="alert-title" id="GTK">
        Refer to your chosen test type
    </div>
    <div class="alert-text">
Please refer to your chosen test type to enter the correct information for your testing session. You can find this information in <strong>Sample collection kits</strong> area of this user guide.</div>
    <div class="alert-links"> 
    </div>
</div>
{% /html %}

Yoti Testing Platform provides an optimised LFT testing experience to increase customer throughput. The following is required to achieve this:

{% table %}
| Set up options | Description | 
| ---- | ---- | 
| When will this antigen test type expire? | This is the expiry time of the test you are using. If a test goes past this time, it must be voided. The customer will need to provide a new sample and be re-tested using a new LFT. | 
| When is the best time to check for a test result? | LFTs have a recommended time to check for a result. The Yoti Testing Platform uses this time to notify testers when they should be looking for a result. | 
| Expiring soon | This is an auto-generated time that the Yoti Testing Platform defines to warn a tester of an upcoming expiring test. | 
| How many tests can fit in your physical testing area? | Every LFT testing scenario is different. Defining the maximum number of tests that can be processed in parallel, helps the user administer results using a more sustainable and manageable approach. This also ensures that users are not overwhelmed with the number of tests to check at a similar time, minimising the chances of human error. | 
{% /table %}

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1605622956/73687/rb60wswwovlfvuygwfdl.png" mode="responsive" height="1800" width="2880" %}
{% /image %}

## 4. Start session

1. Select **Start testing** from the bottom-right corner of the screen.
2. Scan a LFT using the device's camera, referring to the scanning window positioned in the bottom-right corner of the screen.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1605623057/73687/mxanwhcf6nyi6gjnhdtt.png" mode="responsive" height="1800" width="2880" %}
{% /image %}

## 5. Add test to session

When a LFT has been scanned, you will be given an **allocation number**.

Place the physical LFT test in the space reserved for that allocation number, and select **Confirm.**

Continue to add tests as they arrive at your testing station. Test cards will stack in chronological order, with the most recent added test placed at the bottom of the stack.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1605623022/73687/e8k0awxjmbo7tk4ahilk.png" mode="responsive" height="1800" width="2880" %}
{% /image %}

## 6. Checking test result

When a test reaches the recommended time to check for a result. The Yoti Testing Platform will change the visual state of that test to notify you that it is ready to be checked.

When a test appears blue (shown below), please check to see if a result has appeared on that test.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1605623148/73687/js0j1qjf2wnoakgxfofl.png" mode="responsive" height="1800" width="2880" %}
{% /image %}

## 7. Issuing a result

1. Select the blue test card
2. Select whether it is a Negative, Inconclusive or Positive result.
3. The result you select will be sent to that customer's Yoti app or email.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1605623099/73687/xh8uhwznbfrnhre7dzip.png" mode="responsive" height="1800" width="2880" %}
{% /image %}

## Expired tests

When a test reaches its expiry time, it must be voided. The customer will need to provide a new sample and be re-tested using a new LFT. The Yoti Testing Platform shows expired cards in black.

Customer's are automatically sent an inconclusive result when the test expires. The test card persists in the Yoti Testing Platform in case the test was linked to a paper form customer, in which case the tester must contact this person to let them know they need to be tested again.

1. To dismiss an expired test, select its card.
2. Select **OK** on the confirmation modal.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1605623200/73687/qi5gmixohysevzbyn4lb.jpg" mode="responsive" height="1800" width="2880" %}
{% /image %}

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1605623220/73687/n3llkmywnsg7evnjbi0b.png" mode="responsive" height="1800" width="2880" %}
{% /image %}

## Filling your testing area

When you reach the maximum number of parallel tests, you are no longer able to scan test bags and the Yoti Testing Platform notifies you to complete tests in progress before scanning new tests.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1605623246/73687/o2rskx8xjt2wrnvotvs3.png" mode="responsive" height="1800" width="2880" %}
{% /image %}