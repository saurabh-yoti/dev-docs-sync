---
type: page
title: Editing test results
listed: true
slug: results
description: 
index_title: Editing test results
hidden: 
keywords: 
tags: 
---

When uploading test results for RT-PCR/LAMP tests performed by tests supported by the Yoti Testing Platform, you will be able to edit any results that require changing after a medical professional analysis of the raw machine test results file. In order to have access to this feature you will need to enable it in **Results**, under **Settings**, by turning Edit Cq value On. 

Once this is activated, the ability to edit results will be available as part of the normal **Upload** flow. You must have the **Run machine and upload results** permission to be able to upload result files from your testing machine software to the Yoti Testing Platform and have access to **Edit results**.

## 1. Upload test result

Select the test results file and select **Upload**.

{% image url="https://image-archive.developerhub.io/image/upload/72692/lugwyxgwnjs35zwltzqn/1605565884.png" mode="responsive" height="420" width="360" %}
{% /image %}

## 2. Edit results table

A table will be displayed with all results in that batch, displaying all Cq values and results in an anonymised form.  

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/mymgv87j9riindcnl3bt/1612547736.jpg" mode="responsive" height="1636" width="2880" %}
{% /image %}

You will be able to edit the Cq value by clicking on the pen at the end of the row and update the Cq value for that specific well. You have the option to select a reason for editing the result. This information will be kept for audit purposes.

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/wsniisjcuwosnjl7vqg9/1612548223.png" mode="responsive" height="818" width="1440" %}
{% /image %}

Given the impact that this type of change might have, a confirmation screen is displayed to ensure that:

1. the person editing the result has authority from the testing organisation to amend the result;
2. the new Cq value is accurate; and
3. the new Cq value was verified by a medical professional with the expertise to interpret the results of the tests.

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/lrkthxderboqmbf7ecci/1612548248.png" mode="responsive" height="868" width="1440" %}
{% /image %}

## 3. Upload test result

Once all the results are accurate, select **Send test results.** Once the file has been sent,

- Results will appear in the results data for your organisation.
- Yoti and online form customers will automatically receive their test result.
- If the held results feature is set to ON, results are sent to the held results area before customers can receive their test result.

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/r1xsylyeqzvezzqbln2j/1612956093.png" mode="responsive" height="468" width="374" %}
{% /image %}