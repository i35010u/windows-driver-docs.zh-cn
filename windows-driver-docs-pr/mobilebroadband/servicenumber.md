---
title: ServiceNumber
description: ServiceNumber
ms.assetid: 7e02557a-34e5-41f2-9a27-122a144c2ab9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc89b599bf9bc0cd4a70d1945e6178f14011e399
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520418"
---
# <a name="servicenumber"></a>ServiceNumber

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

ServiceNumber 元素指定表示移动运营商的唯一自行生成的 GUID。 此 GUID 必须存在，并且帐户预配的元数据应用于的 PC 以确保通过在该文件中标识的运营商 ID 中声明的 GUID 值的匹配项时进行检查。 帐户预配的元数据是由移动宽带应用或运算符网站生成。 帐户预配的元数据中所述[帐户预配](account-provisioning.md)。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<ServiceNumber>
  text
</ServiceNumber>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


没有特性。

## <a name="span-idtextvaluespanspan-idtextvaluespanspan-idtextvaluespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>文本值


一串[GUIDType](guidtype-serviceinfo.md)。

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
<td><p><a href="serviceinfo.md" data-raw-source="[ServiceInfo](serviceinfo.md)">ServiceInfo</a></p></td>
<td><p><a href="serviceinfo.md" data-raw-source="[ServiceInfo](serviceinfo.md)">ServiceInfo</a>元素是父元素<a href="serviceinfo-xml-schema.md" data-raw-source="[ServiceInfo XML schema](serviceinfo-xml-schema.md)">ServiceInfo XML 架构</a>。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="ServiceNumber" type ="tns:ServiceNumberType" />

<xs:simpleType name="ServiceNumberType">
  <xs:union memberTypes="tns:GUIDType xs:string" />
</xs:simpleType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


ServiceNumber 元素是必需的。

 

 





