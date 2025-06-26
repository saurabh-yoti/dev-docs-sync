---
type: page
title: AML Check
listed: false
slug: aml
description: 
index_title: AML Check
hidden: 
keywords: 
tags: 
---

Yoti provides an AML (Anti-Money Laundering) check service to allow a deeper KYC process to prevent fraud. This is a chargeable service, so please contact [sdksupport@yoti.com](mailto:sdksupport@yoti.com) for more information.

{% html %}
<div class="alert-BYS">

   <div class="alert-title" id="BYS">

      Before you start

   </div>

   <div class="alert-text" >

  Make sure your application is assigned to your organisation in Yoti Hub.

   </div>

   <div class="alert-links"> 

         <a href="https://developers.yoti.com/yoti/welcome#creating-a-yoti-application">Create an application</a>

   </div>

</div>
{% /html %}

### [AML check types](https://developers.yoti.com/yoti/aml#aml-check-types)

Yoti will provide a boolean result on the following checks:

- PEP list:- Verify against Politically Exposed Persons list.
- Fraud list:- Verify against US Social Security Administration Fraud (SNN Fraud) list.
- Watch list:- Verify against watch lists from the Office of Foreign Assets Control

---

### [What you need to provide](https://developers.yoti.com/yoti/aml#what-you-need-to-provide)

For an AML check you will need to provide the following from the doc scan response:

- Given name(s).
- Family name.
- Country of residence. (must be an ISO 3166 3-letter code).
- Social Security Number (US citizens only).
- Postcode/Zip code (US citizens only)

{% html %}
<div class="alert-GTK">

    <div class="alert-title" id="GTK">

       Important information

    </div>

    <div class="alert-text">

      Performing an AML check on a person requires their consent. You must ensure you have user consent before using this service.
    </div>


</div>
{% /html %}

{% code %}
{% tab language="javascript" %}
// Performing an AML check for a US resident

let amlAddress = new Yoti.AmlAddress('USA', '10118');
let amlProfile = new Yoti.AmlProfile('Hunter Avery', 'McCreedy', amlAddress, '121341234');
// Performing an AML check outside of the US
let amlAddress = new Yoti.AmlAddress('GBR');
let amlProfile = new Yoti.AmlProfile('Edward Rupert', 'Taylor', amlAddress);
yotiClient.performAmlCheck(amlProfile).then((amlResult) => {
  console.log(amlResult.isOnPepList);
  console.log(amlResult.isOnFraudList);
  console.log(amlResult.isOnWatchList);
  // Or
  console.log(amlResult);
}).catch((err) => {
  console.error(err);
})
{% /tab %}
{% tab language="ruby" %}
// Cl# Performing an AML check for a US resident
aml_address = Yoti::AmlAddress.new('USA', '10118')
aml_profile = Yoti::AmlProfile.new('Hunter Avery', 'McCreedy', aml_address, '121341234')
# Performing an AML check outside of the US
aml_address = Yoti::AmlAddress.new('GBR')
aml_profile = Yoti::AmlProfile.new('Edward Rupert', 'Taylor', aml_address)
puts Yoti::Client.aml_check(aml_profile)ick to edit code
{% /tab %}
{% tab language="php" %}
<?php

use Yoti\Entity\Country;
use Yoti\Entity\AmlAddress;
use Yoti\Entity\AmlProfile;
// Performing an AML check for a US resident
$amlAddress = new AmlAddress(new Country('USA'), '10118');
$amlProfile = new AmlProfile('Hunter Avery', 'McCreedy', amlAddress, '121341234');
// Performing an AML check outside of the US
$amlAddress = new AmlAddress(new Country('GBR'));
$amlProfile = new AmlProfile('Edward Rupert', 'Taylor', amlAddress);
$amlResult = $yotiClient->performAmlCheck($amlProfile);
var_dump($amlResult->isOnPepList());
var_dump($amlResult->isOnFraudList());
var_dump($amlResult->isOnWatchList());
// Or
echo $amlResult;
{% /tab %}
{% tab language="python" %}
from yoti_python_sdk import aml
from yoti_python_sdk import Client
# Performing an AML check for a US resident
aml_address = aml.AmlAddress("USA", "10118")
aml_profile = aml.AmlProfile("Hunter Avery", "McCreedy", aml_address, "121341234")
# Performing an AML check outside of the US
aml_address = aml.AmlAddress("GBR")
aml_profile = aml.AmlProfile("Edward Rupert", "Taylor", aml_address)
aml_result = yotiClient.perform_aml_check(aml_profile)
print("AML Result for {0} {1}:".format(given_names, family_name))
print("On PEP list: " + str(aml_result.on_pep_list))
print("On fraud list: " + str(aml_result.on_fraud_list))
print("On watchlist: " + str(aml_result.on_watch_list))
{% /tab %}
{% tab language="java" %}
// Performing an AML check for a US resident
AmlAddress amlAddress = new AmlAddressBuilder()
                            .withPostcode("10118")
                            .withCountry("USA")
                            .build();

AmlProfile amlProfile = new AmlProfileBuilder()
                            .withGivenNames("Hunter Avery")
                            .withFamilyName("McCreedy")
                            .withSsn("121341234")
                            .withAddress(amlAddress)
                            .build();

// Perform the check
AmlResult amlResult = client.performAmlCheck(amlProfile); // where client is the initialised Yoti Client

// Result returned in a POJO
System.out.println(amlResult.isOnFraudList());
System.out.println(amlResult.isOnWatchList());
System.out.println(amlResult.isOnPepList());
{% /tab %}
{% tab language="go" %}
// Performing an AML check for a US resident
amlAddress := yoti.AmlAddress{
    Country:  "USA",
    PostCode: "10118"}
amlProfile := yoti.AmlProfile{
    GivenNames: "Hunter Avery",
    FamilyName: "McCreedy",
    Ssn:        "121341234",
    Address:    amlAddress}
// Performing an AML check outside of the US
amlAddress := yoti.AmlAddress{
    Country: "GBR"}
amlProfile := yoti.AmlProfile{
    GivenNames: "Edward Rupert",
    FamilyName: "Taylor",
    Address:    amlAddress}
result, err := client.PerformAmlCheck(amlProfile)
log.Printf("AML Result for %s %s:", givenNames, familyName)
log.Printf("On PEP list: %s", strconv.FormatBool(result.OnPEPList))
log.Printf("On Fraud list: %s", strconv.FormatBool(result.OnFraudList))
log.Printf("On Watch list: %s", strconv.FormatBool(result.OnWatchList))
{% /tab %}
{% tab language="csharp" %}
// Performing an AML check for a US resident

AmlAddress amlAddress = new AmlAddress(
   country: "USA",
   postCode: "10118");
AmlProfile amlProfile = new AmlProfile(
    givenNames: "Hunter Avery",
    familyName: "McCreedy",
    ssn: "121341234",
    amlAddress: amlAddress);
// Performing an AML check outside of the US
AmlAddress amlAddress = new AmlAddress(
   country: "GBR");
AmlProfile amlProfile = new AmlProfile(
    givenNames: "Edward Rupert",
    familyName: "Taylor",
    amlAddress: amlAddress);
AmlResult amlResult = yotiClient.PerformAmlCheck(amlProfile);
bool onPepList = amlResult.IsOnPepList();
bool onFraudList = amlResult.IsOnFraudList();
bool onWatchList = amlResult.IsOnWatchList();
{% /tab %}
{% /code %}