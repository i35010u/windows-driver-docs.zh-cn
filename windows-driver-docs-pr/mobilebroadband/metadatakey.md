---
title: MetadataKey
description: MetadataKey
ms.assetid: 1915db47-98bb-40f5-be3b-75e9af80f506
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8946fa983c1568129fe3dd9b2b082b444543c8d9
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323625"
---
# <a name="metadatakey"></a>MetadataKey

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

MetadataKey 元素指定服务元数据包的属性。 这包括：

-   设备支持的每个硬件功能的标识符。

-   包中的文本字符串的语言特定区域设置。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<MetadataKey>
  child elements
</MetadataKey>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


没有特性。

## <a name="span-idchild_elementsspanspan-idchild_elementsspanspan-idchild_elementsspanchild-elements"></a><span id="Child_elements"></span><span id="child_elements"></span><span id="CHILD_ELEMENTS"></span>子元素


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
<td><p><a href="lastmodifieddate.md" data-raw-source="[LastModifiedDate](lastmodifieddate.md)">LastModifiedDate</a>元素指定服务元数据包的上次更改时间戳。</p></td>
</tr>
<tr class="odd">
<td><p><a href="locale.md" data-raw-source="[Locale](locale.md)">本地</a></p></td>
<td><p><a href="locale.md" data-raw-source="[Locale](locale.md)">Locale</a>元素指定服务元数据包的本地化版本。</p></td>
</tr>
<tr class="even">
<td><p><a href="modelidlist.md" data-raw-source="[ModelIDList](modelidlist.md)">ModelIDList</a></p></td>
<td><p><a href="modelidlist.md" data-raw-source="[ModelIDList](modelidlist.md)">ModelIDList</a>元素指定在服务元数据包中指定的每个设备类型或模型的 GUID。</p></td>
</tr>
<tr class="odd">
<td><p><a href="multiplelocale.md" data-raw-source="[MultipleLocale](multiplelocale.md)">MultipleLocale</a></p></td>
<td><p><a href="multiplelocale.md" data-raw-source="[MultipleLocale](multiplelocale.md)">MultipleLocale</a>元素指定服务元数据包是否支持多个区域设置。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idparent_elementsspanspan-idparent_elementsspanspan-idparent_elementsspanparent-elements"></a><span id="Parent_elements"></span><span id="parent_elements"></span><span id="PARENT_ELEMENTS"></span>父元素


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
<td><p><a href="packageinfo.md" data-raw-source="[PackageInfo](packageinfo.md)">PackageInfo</a>元素是<a href="packageinfo-xml-schema.md" data-raw-source="[PackageInfo XML schema](packageinfo-xml-schema.md)">PackageInfo XML 架构</a>的父元素。 PackageInfo 元素的子元素指定设备元数据包的属性。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


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


MetadataKey 元素的子元素指定操作系统用于执行以下操作的元数据：

-   基于设备的[ModelID](modelid.md)或[HardwareID](hardwareid.md)值搜索服务元数据包的设备元数据存储。 如果有多个元数据包与设备的型号或硬件 ID 匹配，操作系统还会将元数据包内的[区域设置](locale.md)值与用户计算机上的当前语言设置进行比较。

-   如果包的[LastModifiedDate](lastmodifieddate.md)值比设备元数据存储中现有的包新，则使用服务元数据包更新设备元数据存储。

MetadataKey 元素必须包含：

-   [Locale](locale.md)和[LastModifiedDate](lastmodifieddate.md)元素的一个实例。

-   [HardwareIDList](hardwareidlist.md)或[ModelIDList](modelidlist.md)元素的一个实例。 MetadataKey 元素可以包含两个元素的一个实例。

MetadataKey 元素是必需的。

 

 





