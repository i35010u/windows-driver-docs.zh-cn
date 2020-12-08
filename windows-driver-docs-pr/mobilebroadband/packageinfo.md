---
title: PackageInfo
description: PackageInfo
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd22cf6c74c598b71133b3ebde1a1e0d75d00107
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786219"
---
# <a name="packageinfo"></a>PackageInfo

[!include[MBAE deprecation warning](../includes/mbae-deprecation-warning.md)]

PackageInfo 元素是 [PACKAGEINFO XML 架构](packageinfo-xml-schema.md)的父元素。 PackageInfo 元素的子元素指定服务元数据包的属性。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<PackageInfo>
  child elements
</PackageInfo>
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
<td><p><a href="metadatabuilderinformation.md" data-raw-source="[MetadataBuilderInformation](metadatabuilderinformation.md)">MetadataBuilderInformation</a></p></td>
<td><p><a href="metadatabuilderinformation.md" data-raw-source="[MetadataBuilderInformation](metadatabuilderinformation.md)">MetadataBuilderInformation</a>元素指定有关创建服务元数据包的应用程序的信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="metadatakey.md" data-raw-source="[MetadataKey](metadatakey.md)">MetadataKey</a></p></td>
<td><p><a href="metadatakey.md" data-raw-source="[MetadataKey](metadatakey.md)">MetadataKey</a>元素指定服务元数据包的属性。 这些功能包括以下这些：</p>
<ul>
<li><p>设备支持的每个硬件功能的标识符。</p></li>
<li><p>包中的文本字符串的语言特定区域设置。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><a href="packagestructure.md" data-raw-source="[PackageStructure](packagestructure.md)">PackageStructure</a></p></td>
<td><p><a href="packagestructure.md" data-raw-source="[PackageStructure](packagestructure.md)">PackageStructure</a>元素指定服务元数据包引用的 XML 架构。</p></td>
</tr>
<tr class="even">
<td><p><a href="relationships.md" data-raw-source="[Relationships](relationships.md)">关系</a></p></td>
<td><p><a href="relationships.md" data-raw-source="[Relationships](relationships.md)">关系</a>元素通过其子元素，指定用于在设备元数据缓存中跟踪服务元数据包的数据。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idparent_elementsspanspan-idparent_elementsspanspan-idparent_elementsspanparent-elements"></a><span id="Parent_elements"></span><span id="parent_elements"></span><span id="PARENT_ELEMENTS"></span>父元素


没有父元素。

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


``` syntax
<xs:element name="PackageInfo" type="tns:PackageInfoType" />

<xs:complexType name="PackageInfoType">
  <xs:sequence>
    <xs:element name="MetadataKey" type="tns:MetadataKeyType" />
    <xs:element name="PackageStructure" type="tns:PackageStructureType" />
    <xs:element name="Relationships" type="tns:RelationshipsType" minOccurs="0" />
    <xs:element name="MetadataBuilderInformation" type="tns:MetadataBuilderInformationType" minOccurs="0" />
    <xs:any namespace="##other" processContents="lax" minOccurs="0"
      maxOccurs="unbounded" />
  </xs:sequence>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


PackageInfo 元素必须包含 [MetadataKey](metadatakey.md)、 [PackageStructure](packagestructure.md)和 [关系](relationships.md) 元素的一个实例。

 

 





