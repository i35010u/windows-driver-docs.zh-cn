---
title: HardwareId（APN 元素）
description: HardwareId（APN 元素）
ms.assetid: 9c09915c-d0f6-4ddf-b2e1-79f00599c3a0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63c8c0e1d6b997622f6118369835d3cea6870fc4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380156"
---
# <a name="hardwareid-apn-element"></a>HardwareId（APN 元素）


HardwareId 元素指定 HWID 对于指定的运算符。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<HardwareId>
...insert text here
</HardwareId>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


没有特性。

## <a name="span-idtextvaluespanspan-idtextvaluespanspan-idtextvaluespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>文本值


一个字符串，表示编码的硬件 id。 生成适当的硬件 ID 值涉及复杂的算法。 我们建议使用 mbidgenerator.exe 生成您的硬件 Id。

## <a name="span-idchildelementsspanspan-idchildelementsspanspan-idchildelementsspanchild-elements"></a><span id="Child_elements"></span><span id="child_elements"></span><span id="CHILD_ELEMENTS"></span>子元素


没有子元素。

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
<td><p><a href="hardwareidlist-apnxml.md" data-raw-source="[HardwareIdList](hardwareidlist-apnxml.md)">HardwareIdList</a></p></td>
<td><p>指定操作员的硬件 Id 列表。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element ref="HardwareId" maxOccurs="unbounded"/>

<xs:element name="HardwareId">
  <xs:complexType>
    <xs:attribute name="id" type="xs:string" use="required"/>
  </xs:complexType>
</xs:element>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


HardwareId 元素必须表示以下值之一：

-   GSM 网络：IMSI 范围

-   GSM 网络：ICCID 范围

-   CDMA 网络：提供程序名称值

-   CDMA 网络：提供程序 ID 值 (也称为 SID)

HardwareId 元素是必需的。

 

 





