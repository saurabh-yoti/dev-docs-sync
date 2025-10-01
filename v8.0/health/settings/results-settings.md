---
type: page
title: Results settings
listed: true
slug: results-settings
description: 
index_title: Results settings
hidden: 
keywords: 
tags: 
---

You can control when you want to issue test results to your customers. A held results page helps you manage and manually take actions on held results.

Under the results tab, there are two options available for issuing results:

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/ain7hc1txsqts8jp78hb/1618428396.png" caption="Settings &gt; Results" mode="responsive" height="472" width="1296" %}
{% /image %}

{% table %}
| Results settings | Description | 
| ---- | ---- | 
| Automatically | By default, customers who have linked their test to their Yoti app or an email address, will automatically receive their test result, regardless of the result outcome. | 
| Hold results | Customers who have been tested will not automatically receive their result, enabling you to divulge a customer’s result at a more appropriate time. You can choose which result outcomes you would like to hold for review:\n\n\n\n- Hold negative results\n- Hold positive results\n- Hold inconclusive results\n\n\nPlease note that expiry timelines still apply even if you choose to hold results. A held result is automatically sent an inconclusive result if held for longer than the expiry time defined by your chosen sample collection kit.\n\n\n\nThe quicker you act on this, the less time your customers will need to wait to receive their test result.\n\n\n\nCustomers that are held for more than the defined expiry duration will automatically receive an inconclusive test result, and will be required to return and be tested again.\n\n\n\nExpired test results are automatically removed from the held results table. | 
{% /table %}

The last part of this section is to edit CQ value or add external results.

{% image url="https://image-archive.developerhub.io/image/upload/v2_2762/udlypzwghy92xvjcxoyu/1615827413.png" caption="Settings &gt; Results" mode="responsive" height="458" width="610" %}
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