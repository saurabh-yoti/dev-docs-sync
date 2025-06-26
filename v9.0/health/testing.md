---
type: page
title: Testing
listed: true
slug: testing
description: 
index_title: Testing
hidden: 
keywords: 
tags: 
---

The second stage is to process the collected sample. Yoti supports

- RT-PCR / LAMP testing
- Lateral flow testing

This section of the document will walk you through what to do for both types of sample collection. 

## RT-PCR / LAMP Testing

The sample collection tube can be immediately processed on site, or it can be transported to a test centre or laboratory for testing in one of the tests supported.

{% badge type="info" text="Hint" /%} You must have the **Prepare test plates** permission to be able to add customer samples to your testing plates.

From the home page, select **Start testing** to begin a testing session.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1615831921/v2_2762/tlsuhya32j5fu9muhva5.png" caption="Home page" mode="responsive" height="836" width="1316" %}
{% /image %}

Select the machine you are using for this test session. Press SELECT.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1615832012/v2_2762/vtakppkwzhjkkzpbstd7.png" caption="Home page &gt; Start testing &gt; Select machine" mode="responsive" height="870" width="1636" %}
{% /image %}

Select a **well** on the virtual well plate. you will be shown an appropriate plate designs to match the testing machine you are using.

Well plates can cater for any number of well configurations, and is dependant on the size of the machine being used.

For this test example, the last two wells on each row are for a ‘negative’ and a ‘positive’ control sample, which help ensure validity of the test result. These control wells are coloured grey and cannot be allocated to any customer sample. Your test machine may position their control sample in different wells, but they will look the same as shown below.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1615832135/v2_2762/rve8i1esp4w2teln58ew.png" caption="Home page &gt; Start testing &gt; Select machine &gt; Select well" mode="responsive" height="529" width="781" %}
{% /image %}

Transfer 0.05 ml of buffer solution from the **control buffer tube** into each of the **control tubes** on the strip well, using a separate pipette for each control tube.

Scan the QR code on the bag.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1615832202/v2_2762/dfz07rwx8rvt3qqcgbbh.png" caption="Home page &gt; Start testing &gt; Select machine &gt; Select well &gt; Scan QR" mode="responsive" height="407" width="640" %}
{% /image %}

Confirm where you have placed the test in the correct position. 

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1615832272/v2_2762/qnljyiivzfdrvvymel4t.png" caption="Home page &gt; Start testing &gt; Select machine &gt; Select well &gt; Scan QR &gt; Confirm" mode="responsive" height="548" width="783" %}
{% /image %}

The selected well turns green on the virtual well display. This well cannot be selected again during this test batch. Repeat the well location assignment and solution transfer process for further sample tubes until the rest of the virtual wells are filled or you have no more tests to add.

Press Start machine test. This finalises this well plate assignment and generates a unique batch number for this virtual well plate to uniquely identify it. The virtual well plate securely contains the details of all the samples and customers.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1615832510/v2_2762/fmpkkc2gxbjbwm9icxuj.png" caption="Home page &gt; Start testing &gt; Select machine &gt; Select well &gt; Scan QR &gt; Confirm &gt; Start test" mode="responsive" height="415" width="631" %}
{% /image %}

---

## Lateral flow Testing

The sample is brought to a test inputter who registers the test to their testing session. Once the test shows a result, the test inputter registers the result in the portal, which automatically sends the result to the customer via their Yoti app or email.

From the home page, select **Start testing** to begin a testing session.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1615831921/v2_2762/tlsuhya32j5fu9muhva5.png" caption="Home page" mode="responsive" height="836" width="1316" %}
{% /image %}

Select the lateral flow testing test type you are using for this test session. Press SELECT.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1615832012/v2_2762/vtakppkwzhjkkzpbstd7.png" caption="Home page &gt; Start testing &gt; Select lateral flow testing type" mode="responsive" height="870" width="1636" %}
{% /image %}

Yoti provides an optimised lateral flow testing experience to increase customer throughput. The next step is to set up your session:

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1615972312/v2_2762/iv76ua2xno30st8jhl4c.png" caption="Home page &gt; Start testing &gt; Select lateral flow testing type &gt; set up" mode="responsive" height="1552" width="2880" %}
{% /image %}

{% table widths="298" %}
| Set up options | Description | 
| ---- | ---- | 
| When will this antigen test type expire? | This is the expiry time of the test you are using. If a test goes past this time, it must be voided. The customer will need to provide a new sample and be re-tested using a new LFT. | 
| When is the best time to check for a test result? | LFTs have a recommended time to check for a result. The portal uses this time to notify testers when they should be looking for a result. | 
| Expiring soon | This is an auto-generated time that the portal defines to warn a tester of an upcoming expiring test. | 
| How many tests can fit in your physical testing area? | Every LFT testing scenario is different. Defining the maximum number of tests that can be processed in parallel, helps the user administer results using a more sustainable and manageable approach. This also ensures that users are not overwhelmed with the number of tests to check at a similar time, minimising the chances of human error. | 
{% /table %}

Press **START** testing. 

Scan a lateral flow test using the device's camera, referring to the scanning window positioned in the bottom-right corner of the screen.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1615972798/v2_2762/adwpwjzizf3bdexfv25l.png" caption="Home page &gt; Start testing &gt; Select lateral flow testing type &gt; Set up &gt; Scan" mode="responsive" height="1538" width="2200" %}
{% /image %}

When a test has been scanned, you will be given an **allocation number**. Place the physical LFT test in the space reserved for that allocation number, and select **Confirm.**

Continue to add tests as they arrive at your testing station. 

{% badge type="info" text="Hint" /%} Test cards will stack in chronological order, with the most recent added test placed at the bottom of the stack.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1615972686/v2_2762/prlwuf6sdm87whoimess.png" caption="Home page &gt; Start testing &gt; Select lateral flow testing type &gt; Set up &gt; Scan &gt; Position" mode="responsive" height="1426" width="1298" %}
{% /image %}

When a test reaches the recommended time to check for a result, there will  be a change in the visual state of that test to notify you that it is ready to be checked.

When a test appears blue (shown below), please check to see if a result has appeared on that test.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1615972994/v2_2762/d19mm9whotwhyxe12oxs.png" caption="Testing check" mode="responsive" height="944" width="1480" %}
{% /image %}

Select the blue test card and select whether it is a Negative, Inconclusive or Positive result.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1615973102/v2_2762/hiox8krvs0zaxxzvrb3y.png" caption="Issuing results" mode="responsive" height="874" width="1388" %}
{% /image %}

The result you select will be sent to that customer's Yoti app or email.

When you reach the maximum number of parallel tests, you are no longer able to scan test bags and the Yoti will notify you to complete tests in progress before scanning new tests.

When a test reaches its expiry time, it must be voided. The customer will need to provide a new sample and be re-tested using a new LFT. The portal shows expired cards in black.

Customer's are automatically sent an inconclusive result when the test expires. The test card persists in the portal in case the test was linked to a paper form customer, in which case the tester must contact this person to let them know they need to be tested again.

To dismiss an expired test, select its card. Select **OK** on the confirmation modal.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1615973298/v2_2762/kypku5bprddq79jdmtgb.png" caption="Expired tests" mode="responsive" height="954" width="1366" %}
{% /image %}

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1615973331/v2_2762/aj0tmghvecyjzzgjcv3r.png" caption="Test removed screen" mode="300" height="374" width="450" %}
{% /image %}

---

## Test timeline and expiry

At the end of expiration, Yoti automatically sends an inconclusive result to the customer. The customer will be advised to contact the organisation that issued the result, and schedule an appointment to be re-tested.

Remember to upload processed batch files a soon as possible so that:

1. Customers receive their test result as quickly as possible.
2. Batch files are not left to expire, causing an increase in retesting.

---

## Incomplete test sessions

If you leave a session in progress, Yoti will automatically save tests that you have allocated in your session. This applies to RT-PCR/LAMP tests allocated to a testing plate and LFT test cards. This is so that you can return to those incomplete tests at a later time where necessary.

When you start a new testing session, you will be notified if you have an incomplete tests:

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1616597732/v2_2762/sxt8854ju9dz1v4alk0k.png" caption="Incomplete test sessions" mode="600" height="910" width="1506" %}
{% /image %}

Select **Continue incomplete plate** to load the plate into your testing session.

Select **Start a new plate** if you want to ignore the incomplete plate and start a new testing session. The incomplete plate remains until you start a new testing session, where you will see this message again.

If you have access to multiple testing devices, they will show you if there is a session in progress.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1606382914/-1/ujfi8fet9a1ozxuk2rqw.png" caption="Session in progress" mode="responsive" height="456" width="248" %}
{% /image %}