---
title: 关系
description: 关系
ms.assetid: 78443a49-96c6-45d9-a4f3-8213005f82d5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 62e6b2714071466b7bf988dd040d3dab647c32ac
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342977"
---
# <a name="relationships"></a>关系

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

Relationships 元素指定用于跟踪设备元数据包设备元数据缓存中的数据。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<Relationships>
  text
  child elements
</Relationships>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


没有特性。

## <a name="span-idtextvaluespanspan-idtextvaluespanspan-idtextvaluespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>文本值


如果指定的关系元素，则它必须指定[ExperienceID](experienceid.md)元素或[LanguageNeutralIdentifier](languageneutralidentifier.md)元素，或两者。

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
<td><p><a href="experienceid.md" data-raw-source="[ExperienceID](experienceid.md)">ExperienceID</a></p></td>
<td><p><a href="experienceid.md" data-raw-source="[ExperienceID](experienceid.md)">ExperienceID</a>元素指定由 Windows 开发人员中心仪表板的 GUID。 此 GUID 用于组相同的设备标识符独立于包的区域设置的一个或多个元数据包。</p></td>
</tr>
<tr class="even">
<td><p><a href="languageneutralidentifier.md" data-raw-source="[LanguageNeutralIdentifier](languageneutralidentifier.md)">LanguageNeutralIdentifier</a></p></td>
<td><p><a href="languageneutralidentifier.md" data-raw-source="[LanguageNeutralIdentifier](languageneutralidentifier.md)">LanguageNeutralIdentifier</a>元素指定用于标识独立于其区域设置的设备元数据包的 GUID。</p></td>
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
<td><p><a href="packageinfo.md" data-raw-source="[PackageInfo](packageinfo.md)">PackageInfo</a>元素指定服务元数据包的特性。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


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


Relationships 元素的子元素 ([ExperienceID](experienceid.md)并[LanguageNeutralIdentifier](languageneutralidentifier.md)) 提供操作系统使用到查询设备元数据的单独的搜索密钥包安装在设备元数据缓存。

 

 





