---
title: 关系
description: 关系
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5eda600a54500ce84c308007ad4658ec2c2da5e7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821413"
---
# <a name="relationships"></a>关系

[!include[MBAE deprecation warning](../includes/mbae-deprecation-warning.md)]

关系元素指定用于在设备元数据缓存中跟踪设备元数据包的数据。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<Relationships>
  text
  child elements
</Relationships>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


没有特性。

## <a name="span-idtext_valuespanspan-idtext_valuespanspan-idtext_valuespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>文本值


如果指定了关系元素，则它必须指定 [ExperienceID](experienceid.md) 元素或 [LanguageNeutralIdentifier](languageneutralidentifier.md) 元素，或同时指定这两者。

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
<td><p><a href="experienceid.md" data-raw-source="[ExperienceID](experienceid.md)">ExperienceID</a></p></td>
<td><p><a href="experienceid.md" data-raw-source="[ExperienceID](experienceid.md)">ExperienceID</a>元素指定由 Windows 开发人员中心仪表板管理的 GUID。 此 GUID 用于为与包的区域设置无关的相同设备标识符组合一个或多个元数据包。</p></td>
</tr>
<tr class="even">
<td><p><a href="languageneutralidentifier.md" data-raw-source="[LanguageNeutralIdentifier](languageneutralidentifier.md)">LanguageNeutralIdentifier</a></p></td>
<td><p><a href="languageneutralidentifier.md" data-raw-source="[LanguageNeutralIdentifier](languageneutralidentifier.md)">LanguageNeutralIdentifier</a>元素指定一个 GUID，用于标识与设备元数据包无关的区域设置。</p></td>
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
<td><p><a href="packageinfo.md" data-raw-source="[PackageInfo](packageinfo.md)">PackageInfo</a>元素指定服务元数据包的属性。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


``` syntax
<xs:element name="Relationships" type="tns:RelationshipsType" minOccurs="0" />

<xs:complexType name="RelationshipsType">
  <xs:sequence>
    <xs:element name="ExperienceID" type="tns:GUIDType" minOccurs="0" />
    <xs:element name="LanguageNeutralIdentifier" type="tns:GUIDType" minOccurs="0" />
    <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded"
  </xs:sequence>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


关系元素的子元素 ([ExperienceID](experienceid.md) 和 [LanguageNeutralIdentifier](languageneutralidentifier.md)) 提供单独的搜索键，操作系统使用该搜索键来查询设备元数据缓存中安装的设备元数据包。

 

 





