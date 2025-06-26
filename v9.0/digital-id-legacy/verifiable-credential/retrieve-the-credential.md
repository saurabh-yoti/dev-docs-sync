---
type: page
title: Retrieve the credential
listed: true
slug: retrieve-the-credential
description: 
index_title: Retrieve the credential
hidden: 
keywords: 
tags: 
---

{% html %}
<div class="alert-BYS">
   <div class="alert-title" id="BYS">
      Before you start
   </div>
   <div class="alert-text" >
      Please get familiar with our user profile service with the Yoti App.
   </div>
   <div class="alert-links"> 
           <a href="https://developers.yoti.com/digital-id/retrieve-the-profile">Retrieve a profile</a>
   </div>
</div>
{% /html %}

Once the user has scanned the Yoti QR code, Yoti will perform a GET request to the defined call-back URL, passing a token as a query string parameter, any additional relying party defined query parameters will also be passed here.

{% code %}
{% tab language="javascript" %}
const CONTENT_TYPE_STRING = 1;
const CONTENT_TYPE_JPEG = 2;
const CONTENT_TYPE_DATE = 3;
const CONTENT_TYPE_PNG = 4;
const CONTENT_TYPE_BYTES = 5;
const CONTENT_TYPE_INT = 7;

const stringValue = AttributeConverter.convertValueBasedOnContentType(
  profile.getAttribute("Third_Party_Attribute_Name").getValue(),
  CONTENT_TYPE_STRING //text/string
);

const imageJPG = AttributeConverter.convertValueBasedOnContentType(
  profile.getAttribute("Third_Party_Attribute_Name").getValue(),
  CONTENT_TYPE_JPEG //image/jpg
);

const dateTime = AttributeConverter.convertValueBasedOnContentType(
  profile.getAttribute("Third_Party_Attribute_Name").getValue(),
  CONTENT_TYPE_DATE //DateTime
);

const imagePNG = AttributeConverter.convertValueBasedOnContentType(
  profile.getAttribute("Third_Party_Attribute_Name").getValue(),
  CONTENT_TYPE_PNG //image/png
);

const jsonValue = AttributeConverter.convertValueBasedOnContentType(
  profile.getAttribute("Third_Party_Attribute_Name").getValue(),
  CONTENT_TYPE_BYTES //application/json
);

const intValue = AttributeConverter.convertValueBasedOnContentType(
  profile.getAttribute("Third_Party_Attribute_Name").getValue(),
  CONTENT_TYPE_INT //Integer
);
{% /tab %}
{% tab language="java" %}
Attribute<String> stringValue = profile.getAttribute("Third_Party_Attribute_Name", String.class);
Attribute<Image> imageJPG = profile.getAttribute("Third_Party_Attribute_Name", Image.class);
Attribute<Date> dateTime = profile.getAttribute("Third_Party_Attribute_Name", Date.class);
Attribute<Map<String, Object>> jsonValue = profile.getAttribute("Third_Party_Attribute_Name", (Class) Map.class);
Attribute<Integer> intValue = profile.getAttribute("Third_Party_Attribute_Name", Integer.class);
{% /tab %}
{% tab language="php" %}
private const CONTENT_TYPE_STRING = 1;
private const CONTENT_TYPE_JPEG = 2;
private const CONTENT_TYPE_DATE = 3;
private const CONTENT_TYPE_PNG = 4;
private const CONTENT_TYPE_JSON = 5;
private const CONTENT_TYPE_INT = 7;

$stringValue = AttributeConverter::convertValueBasedOnContentType(
  $profile->getProfileAttribute('Third_Party_Attribute_Name')->getValue(),
  CONTENT_TYPE_STRING, //text/string
  null
);

$imageJPG = AttributeConverter::convertValueBasedOnContentType(
  $profile->getProfileAttribute('Third_Party_Attribute_Name')->getValue(),
  CONTENT_TYPE_JPEG, //image/jpg
  null
);

$dateTime = AttributeConverter::convertValueBasedOnContentType(
  $profile->getProfileAttribute('Third_Party_Attribute_Name')->getValue(),
  CONTENT_TYPE_DATE, //DateTime
  null
);

$imagePNG = AttributeConverter::convertValueBasedOnContentType(
  $profile->getProfileAttribute('Third_Party_Attribute_Name')->getValue(),
  CONTENT_TYPE_PNG, //image/png
  null
);

$jsonValue = AttributeConverter::convertValueBasedOnContentType(
  $profile->getProfileAttribute('Third_Party_Attribute_Name')->getValue(),
  CONTENT_TYPE_JSON, //application/json
  null
);

$intValue = AttributeConverter::convertValueBasedOnContentType(
  $profile->getProfileAttribute('Third_Party_Attribute_Name')->getValue(),
  CONTENT_TYPE_INT, //Integer
  null
);
{% /tab %}
{% tab language="python" %}
from yoti_python_sdk import attribute_parser
from yoti_python_sdk.protobuf import protobuf

def proto():
    return protobuf.Protobuf()
  
stringValue = attribute_parser.value_based_on_content_type(
  profile.get_attribute("Third_Party_Attribute_Name").value, proto.STRING
)

imageJPG = attribute_parser.value_based_on_content_type(
  profile.get_attribute("Third_Party_Attribute_Name").value, proto.CT_JPEG
)

dateTime = attribute_parser.value_based_on_content_type(
  profile.get_attribute("Third_Party_Attribute_Name").value, proto.CT_DATE
)

imagePNG = attribute_parser.value_based_on_content_type(
  profile.get_attribute("Third_Party_Attribute_Name").value, proto.CT_PNG
)

jsonValue = attribute_parser.value_based_on_content_type(
  profile.get_attribute("Third_Party_Attribute_Name").value, proto.CT_JSON
)

intValue = attribute_parser.value_based_on_content_type(
  profile.get_attribute("Third_Party_Attribute_Name").value, proto.CT_INT
)
{% /tab %}
{% tab language="csharp" %}
profile.GetAttributeByName<string>(name: "_thirdPartyAttributeName"); //text/string
profile.GetAttributeByName<Dictionary<string, JToken>>(name: "_thirdPartyAttributeName"); //application/json
profile.GetAttributeByName<PngImage>(name: "_thirdPartyAttributeName"); //image/png
profile.GetAttributeByName<JpegImage>(name: "_thirdPartyAttributeName"); //image/jpeg
profile.GetAttributeByName<DateTime>(name: "_thirdPartyAttributeName"); //DateTime
profile.GetAttributeByName<int>(name: "_thirdPartyAttributeName"); //integer
{% /tab %}
{% tab language="go" %}
stringValue := userProfile.GetStringAttribute("Third_Party_Attribute_Name").Value()
imageJPG := userProfile.GetImageAttribute("Third_Party_Attribute_Name").Value()
dateTime := userProfile.GetAttribute("Third_Party_Attribute_Name").Value()
imagePNG := userProfile.GetImageAttribute("Third_Party_Attribute_Name").Value()
jsonValue := userProfile.GetJSONAttribute("Third_Party_Attribute_Name").Value()
intValue := userProfile.GetAttribute("Third_Party_Attribute_Name").Value()
{% /tab %}
{% tab language="ruby" %}
stringValue = Yoti::Protobuf.value_based_on_content_type(profile.get_attribute('Third_Party_Attribute_Name'), Yoti::Protobuf::CT_STRING)

imageJPG = Yoti::Protobuf.value_based_on_content_type(profile.get_attribute('Third_Party_Attribute_Name'), Yoti::Protobuf::CT_JPEG)

dateTime = Yoti::Protobuf.value_based_on_content_type(profile.get_attribute('Third_Party_Attribute_Name'), Yoti::Protobuf::CT_DATE)

imagePNG = Yoti::Protobuf.value_based_on_content_type(profile.get_attribute('Third_Party_Attribute_Name'), Yoti::Protobuf::CT_PNG)

jsonValue = Yoti::Protobuf.value_based_on_content_type(profile.get_attribute('Third_Party_Attribute_Name'), Yoti::Protobuf::CT_JSON)

intValue = Yoti::Protobuf.value_based_on_content_type(profile.get_attribute('Third_Party_Attribute_Name'), Yoti::Protobuf::CT_INT)
{% /tab %}
{% /code %}