---
type: page
title: Results
listed: true
slug: results
description: 
index_title: Results
hidden: 
keywords: 
tags: 
---

Collect the results file of the completed test from the independent test centre or laboratory and save the file locally on your device. This file should follow this [template](https://www.yoti.com/wp-content/uploads/External-lab-results-template.csv) and the name of the file should be alphanumerical. 

{% badge type="info" text="Hint" /%} You must have the **Run machine and upload results** permission to be able to upload result files from your testing machine software.

## Upload results

Select **Upload test results** from the homepage.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1615832733/v2_2762/owxotxwyjqdieyjmsayb.png" caption="Home page &gt; Upload machine results" mode="responsive" height="836" width="1316" %}
{% /image %}

Select the test results file and select **Upload**.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1605565884/72692/lugwyxgwnjs35zwltzqn.png" caption="Home page &gt; Upload machine results &gt; Upload file" mode="responsive" height="420" width="360" %}
{% /image %}

Once the file has been uploaded,

- Results will appear in the results data for your organisation. 

{% badge type="info" text="Hint" /%} You can edit the results, please see section below.

- Yoti and online form customers will automatically receive their test result.
- If the held results feature is set to ON, results are sent to the held results area before customers can receive their test result.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1615832821/v2_2762/upmyznnvipyg0igbkaya.png" caption="Home page &gt; Upload machine results &gt; Upload file&gt; Upload complete" mode="responsive" height="349" width="336" %}
{% /image %}

---

## Edit results

Yoti allows you to be able to update any results that require changing after a medical professional analysis of the raw machine test results file.

You can edit the test result and the CQ value.

#### Edit test results

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1635502459/v2_2762/x62m1ygbsexg5c5mwqxc.png" caption="Edit results" mode="responsive" height="1230" width="3311" %}
{% /image %}

#### Edit CQ value

{% badge type="info" text="Hint" /%} In order to have access to this feature you will need to enable it in **Results**, under **Settings**, by turning [Edit Cq value On.](https://developers.yoti.com/health-test/setup#results)

Once this is activated, the ability to edit results will be available as part of the normal **Upload** flow. You must have the **Run machine and upload results** permission to be able to upload result files from your testing machine software and have access to **Edit results**.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1616596603/v2_2762/zhsl9wr9xodvbkuhcgvt.png" caption="Settings &gt; Pre-registered flow &gt; ON" mode="600" height="1076" width="1656" %}
{% /image %}

After the upload is complete, a table will be displayed with all results in that batch, displaying all Cq values and results in an anonymised form.

You will be able to edit the Cq value by clicking on the pen at the end of the row and update the Cq value for that specific well. You have the option to select a reason for editing the result. This information will be kept for audit purposes.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1616597054/v2_2762/gzpjor8bqunp1wjzhngk.png" caption="Upload complete &gt; ... &gt; Edit" mode="responsive" height="642" width="1398" %}
{% /image %}

Given the impact that this type of change might have, a confirmation screen is displayed to ensure that:

1. The person editing the result has authority from the testing organisation to amend the result;
2. The new Cq value is accurate; and
3. The new Cq value was verified by a medical professional with the expertise to interpret the results of the tests.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1616597103/v2_2762/tdynatinv2ons8l4wgti.png" caption="Upload complete &gt; ... &gt; Edit &gt; Update" mode="300" height="606" width="344" %}
{% /image %}

The upload will complete after you press **YES**.

---

## Issuing results

Once the file has been uploaded, Yoti and online customers will receive their result differently:

- The Yoti app
- Email
- Contact them

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1615974794/v2_2762/mrmhfjmuwt1lgp6onnmt.png" caption="Results issuing methods" mode="600" height="674" width="986" %}
{% /image %}

Customers who have linked their Yoti will automatically receive their COVID-19 status in their secure, tamper proof Yoti app. Negative, positive and invalid results will look like this:

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1605566496/72693/szmjiebyqhevzuhh1ste.png" caption="Example of results on mobile" mode="full" height="860" width="1600" %}
{% /image %}

Customers who have provided an email address via the online form will automatically receive their COVID-19 status in an email. Negative, positive and unclear results look like this:

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1626958092/v2_2762/hhacvdfk2brjol3ede3z.png" caption="Email examples" mode="responsive" height="644" width="1383" %}
{% /image %}

The void test results looks like the following:

{% image url="https://uploads.developerhub.io/prod/kvAX/t0bkq90ol683ydpemim6vgcchg8gqpro4o3ooaf7qb3csqq777l6j67d3aj7xvk2.png" caption="Void email example" mode="300" height="1210" width="1040" %}
{% /image %}

Yoti has a NHS disclaimer which is added to UK Organisations:

{% table %}
| Result | Disclaimer | 
| ---- | ---- | 
| POSITIVE | A positive result means it is likely you had SARS-CoV-2 virus (coronavirus) when your test was done. SARS-CoV-2 is the name of the virus that causes the disease COVID-19. You and anyone you live with must self-isolate immediately to avoid spreading the infection to other people. Please follow the NHS guidance on receiving a Positive test result for coronavirus (COVID-19) here:[ https://www.nhs.uk/conditions/coronavirus-covid-19/testing/test-results/positive-test-result/](https://www.nhs.uk/conditions/coronavirus-covid-19/testing/test-results/positive-test-result/)\n\n\nFor more information, please get in contact with the business who issued the test result. | 
| NEGATIVE | A negative test result means that your test did not detect any SARS-CoV-2 virus (coronavirus) in your sample. SARS-CoV-2 is the name of the virus that causes the disease COVID-19.\n\n\nPlease be aware that no medical diagnostic test is 100% accurate, and a negative test result does not guarantee that you do not have COVID-19. If you feel unwell after a negative test result, stay at home until you are feeling better. Contact your GP if your symptoms get worse or do not go away. Please follow the NHS guidance on receiving a Negative test result for coronavirus (COVID-19) here:[ https://www.nhs.uk/conditions/coronavirus-covid-19/testing/test-results/negative-test-result/](https://www.nhs.uk/conditions/coronavirus-covid-19/testing/test-results/negative-test-result/)\nFor more information, please get in contact with the business who issued the test result. | 
| UNCLEAR | An unclear result means that your test sample could not give a reliable result and it is not possible to say if you had SARS-CoV-2 virus (coronavirus) when the test was done. SARS-CoV-2 is the name of the virus that causes the disease COVID-19. \n\n\nYou will usually need to get a repeat test as soon as possible. \n\n\n\nYou should self-isolate until you get the result of the repeat test if:\n\n\n- You had a test because you had symptoms\n- Someone you live with has tested positive or has symptoms and has not had a test yet\n- You have been told that you have been in contact with someone who tested positive\n- You are in quarantine because you have recently travelled to the United Kingdom from abroad\n\n\nAnyone you live with should also self-isolate if you had the test because you have symptoms, or someone you live with has symptoms or tested positive.\n\n\nPlease follow the NHS guidance on receiving an unclear test result for coronavirus (COVID-19) here:[ https://www.nhs.uk/conditions/coronavirus-covid-19/testing/test-results/test-sample-could-not-be-read-void/](https://www.nhs.uk/conditions/coronavirus-covid-19/testing/test-results/test-sample-could-not-be-read-void/)\n\n\nFor more information, please get in contact with the business who issued the test result. | 
| VOID | A Void result means that your test sample could not be read and it is not possible to say if you had SARS-CoV-2 virus (coronavirus) when the test was done. SARS-CoV-2 is the name of the virus that causes the disease COVID-19.\n\n\nWhat you need to do depends on the type of test you had.\n\n\n\nIf you had a PCR test and your sample could not be read, you'll usually need to get another test as soon as possible.\n\n\n\nIf you did a rapid lateral flow test and your result was Void, do another rapid lateral flow test as soon as possible. You can do another home test if you have one.\n\n\n\nPlease follow the NHS guidance on receiving a Void test result for coronavirus (COVID-19) \n\n\nFor more information, please get in contact with the business who issued the test result. | 
{% /table %}

If you used test and release the disclaimer will be as follows:

{% table %}
| Result | Disclaimer | 
| ---- | ---- | 
| POSITIVE | Your coronavirus test result is positive. You had the virus when the test was done.\n\n\n\nPlease follow the NHS guidance on receiving a Positive test result for coronavirus (COVID-19) here:[ https://www.nhs.uk/conditions/coronavirus-covid-19/testing/test-results/positive-test-result/](https://www.nhs.uk/conditions/coronavirus-covid-19/testing/test-results/positive-test-result/)\n\n\nIf you have not had symptoms of coronavirus, you must self-isolate for 10 days from the day after your test date. If you have symptoms of coronavirus, you must self-isolate for 10 days from the day your symptoms started, if earlier than when you took your test. (The day after symptom onset or test date is counted as the first full day of self-isolation.)\n\n\nPeople you live with or are travelling with should also self-isolate for 10 days from the day after you took a test.\n\n\nYou may be contacted for contact tracing and to check that you, and those who you live or are travelling with, are self-isolating.\n\n\nYou must not travel, including to leave the UK, during self-isolation.\n\n\nContact 111 if you need medical help. In an emergency dial 999.\nFor more information, go to [https://www.gov.uk/guidance/coronavirus-covid-19-test-to-release-for-international-travel](https://www.gov.uk/guidance/coronavirus-covid-19-test-to-release-for-international-travel) | 
| NEGATIVE | Your coronavirus test result is negative. You did not have the virus when the test was done. \n\n\n\nPlease be aware that no medical diagnostic test is 100% accurate, and a negative test result does not guarantee that you do not have COVID-19. If you feel unwell after a negative test result, stay at home until you are feeling better. Contact your GP if your symptoms get worse or do not go away. Please follow the NHS guidance on receiving a Negative test result for coronavirus (COVID-19) here: [https://www.nhs.uk/conditions/coronavirus-covid-19/testing/test-results/negative-test-result/](https://www.nhs.uk/conditions/coronavirus-covid-19/testing/test-results/negative-test-result/).\n\n\nIf you were self-isolating as an international arrival you may stop self-isolating.\n\n\nYou should self-isolate if:\n\n\n- you get symptoms of coronavirus (you should get an NHS coronavirus test and self-isolate until you get the results) \n- you’re going into hospital (self-isolating until the date you go in)\n- someone you live with tests positive\n- you’ve been traced as a contact of someone who tested positive\n\n\nFor advice on when you might need to self-isolate and what to do, go to [www.nhs.uk/conditions/coronavirus-covid-19](http://www.nhs.uk/conditions/coronavirus-covid-19) and read ‘Self-isolation and treating symptoms’.\n\n\nIt’s a legal requirement to self-isolate when you arrive in the UK from a non-exempt country, territory or region. If you’re contacted by the enforcement authorities or the police after you have received this negative result please show them this notification.\nFor more information, go to [https://www.gov.uk/guidance/coronavirus-covid-19-test-to-release-for-international-travel](https://www.gov.uk/guidance/coronavirus-covid-19-test-to-release-for-international-travel). | 
| UNCLEAR | Your coronavirus test result is unclear. It’s not possible to say if you had the virus when the test was done.\n\n\n\nYou will usually need to get a repeat PCR test as soon as possible. \n\n\n\nPlease follow the NHS guidance on receiving an Unclear test result for coronavirus (COVID-19) here: [https://www.nhs.uk/conditions/coronavirus-covid-19/testing/test-results/test-sample-could-not-be-read-void/](https://www.nhs.uk/conditions/coronavirus-covid-19/testing/test-results/test-sample-could-not-be-read-void/)\n\n\nYou must, by law, continue self-isolating for the remainder of your self-isolation period as an international arrival travelling to the UK from a non-exempt country, territory or region. You may be contacted to check that you are self-isolating.\nIf you want to shorten your self-isolation period you will need to take another test for international arrivals. For more information, go to [https://www.gov.uk/guidance/coronavirus-covid-19-test-to-release-for-international-travel](https://www.gov.uk/guidance/coronavirus-covid-19-test-to-release-for-international-travel). | 
| VOID | A Void result means that your test sample could not be read and it is not possible to say if you had SARS-CoV-2 virus (coronavirus) when the test was done. SARS-CoV-2 is the name of the virus that causes the disease COVID-19.\n\n\nIt is advised that you take another COVID-19 test.\n\n\nPlease follow the NHS guidance on receiving a Void test result for coronavirus (COVID-19) [here](https://www.nhs.uk/conditions/coronavirus-covid-19/testing/test-results/test-sample-could-not-be-read-void/)\n\n\nFor more information, please get in contact with the business who issued the test result. | 
{% /table %}

### Sending held results

If you have enabled held results, and decide you want to send the results out.

Go to **Admin** and then select **Held results.**

This is where you will see a list of held results in a table.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1626956694/v2_2762/rednxziajkcudixzfenz.png" caption="Admin &gt; Held results" mode="responsive" height="513" width="1637" %}
{% /image %}

Click on the **Send** icon for a held result. This will open a modal showing additional details on this test result.

This is where you can find the customer’s available contact details. You can also copy the email address to your clipboard.

To send the result to the customer, select **Send result**. You will be asked to confirm this action because it will automatically send this test result to a Yoti app or online form customer.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1626956738/v2_2762/kmicx0cx9okrpmbcjvqi.png" caption="Admin &gt; Held results &gt; Send results" mode="responsive" height="696" width="960" %}
{% /image %}

To go back to the table, select **Cancel**. You have the option to make the result as notified.

You can filter on these results by:

- Batch ID
- Notified / Not notified 
- Sample updated / Reported on.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1635499704/v2_2762/hhs12wxvcwnzc35yaumh.png" caption="Filter on held results" mode="responsive" height="622" width="2052" %}
{% /image %}

### Move held results

If you would like to remove results from the queue without sending the results please click the **...** and **press Move row to reporting.**

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1626957293/v2_2762/b7ofpfdcq9fj2y1g2tzf.png" caption="Admin &gt; Held results &gt; Move Row" mode="responsive" height="566" width="1600" %}
{% /image %}

You will be prompted with are confirmation screen:

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1616706510/v2_2762/zk3uzudrip79l3ndlmjk.png" caption="Admin &gt; Held results &gt; Move row &gt; Confirm" mode="responsive" height="862" width="944" %}
{% /image %}

Once this action is done, you cannot send a result out to the customer.

---

## Update customer information

When you have reliable information that the customer details are incorrect (e.g., a typo in an email) you will be able to edit these details from the **Held results** and the **Reporting** area. Editing customer details is only available when the customer chose to identify themselves via webform during the Collection flow.

You can edit the customer details via:

- Reporting 
- Held results

Clicking the three dots at the end of that customer's row and selecting the **Edit details** option; or

1. clicking the **Update customer details** button when you are seeing the customers details.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1626957418/v2_2762/dx4s4ouux7xlnejmtclu.png" caption="Admin &gt; Held results &gt; Edit details" mode="responsive" height="606" width="1613" %}
{% /image %}

Changing customer details will not send the results to the customer. In order to send the results to that customer you will still need to select the **Send test result** option.

{% image url="https://res.cloudinary.com/developerhub/image/upload/v1626957477/v2_2762/q7fyyybzznqbx7tfymth.png" caption="Edit customer details" mode="responsive" height="789" width="329" %}
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