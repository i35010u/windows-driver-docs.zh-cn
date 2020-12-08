---
title: PackageStructure
description: PackageStructure
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30f6a55c48dc6fb97c17d124b09dfdd6a726a275
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786275"
---
# <a name="packagestructure"></a>PackageStructure

[!include[MBAE deprecation warning](../includes/mbae-deprecation-warning.md)]

PackageStructure 元素指定服务元数据包引用的 XML 架构。 每个 XML 架构都是通过 [Metadata](metadata-service-schema.md) 元素指定的。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<PackageStructure>
  text
  child elements
</PackageStructure>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


没有特性。

## <a name="span-idtext_valuespanspan-idtext_valuespanspan-idtext_valuespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>文本值


需要四个或更多的 [元数据](metadata-service-schema.md) 元素。

## <a name="span-idchild_elementsspanspan-idchild_elementsspanspan-idchild_elementsspanchild-elements"></a><span id="Child_elements"></span><span id="child_elements"></span><span id="CHILD_ELEMENTS"></span>子元素


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>元素</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="metadata-service-schema.md" data-raw-source="[Metadata](metadata-service-schema.md)">元数据</a></p></td>
<td><p><a href="metadata-service-schema.md" data-raw-source="[Metadata](metadata-service-schema.md)">Metadata</a>元素指定通过设备元数据包引用的 XML 架构。</p></td>
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
<xs:element name="PackageStructure" type="tns:PackageStructureType" />

<xs:complexType name="PackageStructureType">
  <xs:sequence>
    <xs:element name="Metadata" type="tns:MetadataType" minOccurs="2" maxOccurs="unbounded" />
    <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
  </xs:sequence>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


在 PackageStructure 元素中，必须至少指定 [Metadata](metadata-service-schema.md) 元素的四个实例。 每个实例必须指定一个用于创建服务元数据包的必需 XML 架构：

-   [PackageInfo XML 架构](packageinfo-xml-schema.md)

-   [ServiceInfo XML 架构](serviceinfo-xml-schema.md)

-   [SoftwareInfo XML 架构](softwareinfo-xml-schema.md)

-   [MobileBroadbandInfo XML 架构](mobilebroadbandinfo-xml-schema.md)

PackageStructure 元素是必需的。

 

 





