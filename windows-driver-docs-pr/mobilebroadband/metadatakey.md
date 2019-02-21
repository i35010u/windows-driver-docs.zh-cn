---
title: MetadataKey
description: MetadataKey
ms.assetid: 1915db47-98bb-40f5-be3b-75e9af80f506
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8946fa983c1568129fe3dd9b2b082b444543c8d9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534049"
---
# <a name="metadatakey"></a>MetadataKey

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

MetadataKey 元素指定服务元数据包的属性。 例如：

-   每个设备支持的硬件函数的标识符。

-   特定于语言的区域设置的包中的文本字符串。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<MetadataKey>
  child elements
</MetadataKey>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


没有特性。

## <a name="span-idchildelementsspanspan-idchildelementsspanspan-idchildelementsspanchild-elements"></a><span id="Child_elements"></span><span id="child_elements"></span><span id="CHILD_ELEMENTS"></span>子元素


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>元素</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="hardwareidlist.md" data-raw-source="[HardwareIDList](hardwareidlist.md)">HardwareIDList</a></p></td>
<td><p><a href="hardwareidlist.md" data-raw-source="[HardwareIDList](hardwareidlist.md)">HardwareIDList</a>元素指定设备的一个或多个硬件标识字符串。</p></td>
</tr>
<tr class="even">
<td><p><a href="lastmodifieddate.md" data-raw-source="[LastModifiedDate](lastmodifieddate.md)">LastModifiedDate</a></p></td>
<td><p><a href="lastmodifieddate.md" data-raw-source="[LastModifiedDate](lastmodifieddate.md)">LastModifiedDate</a>元素指定服务元数据包的上次更改的时间戳。</p></td>
</tr>
<tr class="odd">
<td><p><a href="locale.md" data-raw-source="[Locale](locale.md)">区域设置</a></p></td>
<td><p><a href="locale.md" data-raw-source="[Locale](locale.md)">区域设置</a>元素指定服务元数据包的本地化的版本。</p></td>
</tr>
<tr class="even">
<td><p><a href="modelidlist.md" data-raw-source="[ModelIDList](modelidlist.md)">ModelIDList</a></p></td>
<td><p><a href="modelidlist.md" data-raw-source="[ModelIDList](modelidlist.md)">ModelIDList</a>元素指定每个设备类型或模型的服务元数据包中指定的 GUID。</p></td>
</tr>
<tr class="odd">
<td><p><a href="multiplelocale.md" data-raw-source="[MultipleLocale](multiplelocale.md)">MultipleLocale</a></p></td>
<td><p><a href="multiplelocale.md" data-raw-source="[MultipleLocale](multiplelocale.md)">MultipleLocale</a>元素指定服务元数据包是否支持多个区域设置。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idparentelementsspanspan-idparentelementsspanspan-idparentelementsspanparent-elements"></a><span id="Parent_elements"></span><span id="parent_elements"></span><span id="PARENT_ELEMENTS"></span>父元素


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>元素</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="packageinfo.md" data-raw-source="[PackageInfo](packageinfo.md)">PackageInfo</a></p></td>
<td><p><a href="packageinfo.md" data-raw-source="[PackageInfo](packageinfo.md)">PackageInfo</a>元素是父元素<a href="packageinfo-xml-schema.md" data-raw-source="[PackageInfo XML schema](packageinfo-xml-schema.md)">PackageInfo XML 架构</a>。 PackageInfo 元素的子元素指定设备元数据包的属性。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="MetadataKey" type="tns:MetadataKeyType" />

<xs:complexType name="MetadataKeyType">
  <xs:sequence>
    <xs:choice>
      <xs:sequence>
       <xs:element name="HardwareIDList" type="tns:HardwareIDListType" />
       <xs:element name="ModelIDList" type="tns:ModelIDListType" minOccurs="0" />
      </xs:sequence>
      <xs:element name="ModelIDList" type="tns:ModelIDListType" />
    </xs:choice>
    <xs:element name="Locale" type="tns:LocaleType" />
    <xs:element name="LastModifiedDate" type="xs:dateTime" />
    <xs:element ref="v2:MultipleLocale" minOccurs="0" />
    <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
  </xs:sequence>
</xs:complexType>
```

下面是 PackageInfov2 XML 架构元数据：

``` syntax
<?xml version="1.0" encoding="UTF-8"?>

<xs:schema targetNamespace="http://schemas.microsoft.com/windows/2010/08/DeviceMetadata/PackageInfov2"
           xmlns:tns="http://schemas.microsoft.com/windows/2010/08/DeviceMetadata/PackageInfov2"
           xmlns:xs="http://www.w3.org/2001/XMLSchema"
           elementFormDefault="qualified"
           blockDefault="#all">

<xs:element name="MultipleLocale" type ="xs:boolean" />

</xs:schema>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


MetadataKey 元素的子元素指定操作系统使用来执行以下操作的元数据：

-   搜索设备元数据存储区的设备上基于服务元数据包[ModelID](modelid.md)或[HardwareID](hardwareid.md)值。 如果多个元数据包匹配设备的模型或硬件 ID，操作系统也会比较[区域设置](locale.md)到用户的计算机上的当前语言设置的元数据包中的值。

-   使用服务元数据包更新设备元数据存储区，如果某个包包含较新[LastModifiedDate](lastmodifieddate.md)比设备元数据存储区中的现有程序包的值。

MetadataKey 元素必须包含：

-   一个实例[区域设置](locale.md)并[LastModifiedDate](lastmodifieddate.md)元素。

-   其中任何一个实例[HardwareIDList](hardwareidlist.md)或[ModelIDList](modelidlist.md)元素。 MetadataKey 元素可以包含这两个元素的一个实例。

MetadataKey 元素是必需的。

 

 





