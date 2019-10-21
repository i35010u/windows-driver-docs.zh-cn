---
title: ServiceNumber
description: ServiceNumber
ms.assetid: 7e02557a-34e5-41f2-9a27-122a144c2ab9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc89b599bf9bc0cd4a70d1945e6178f14011e399
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323686"
---
# <a name="servicenumber"></a>ServiceNumber

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

ServiceNumber 元素指定代表移动运营商的唯一自行生成的 GUID。 如果将帐户预配元数据应用于电脑以确保与该文件中标识的运营商 ID 中声明的 GUID 值匹配，则此 GUID 必须存在并选中。 帐户预配元数据是由移动宽带应用或操作员网站生成的。 帐户预配元数据在[帐户设置](account-provisioning.md)中进行了介绍。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<ServiceNumber>
  text
</ServiceNumber>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


没有特性。

## <a name="span-idtext_valuespanspan-idtext_valuespanspan-idtext_valuespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>文本值


[GUIDType](guidtype-serviceinfo.md)的字符串。

## <a name="span-idchild_elementsspanspan-idchild_elementsspanspan-idchild_elementsspanchild-elements"></a><span id="Child_elements"></span><span id="child_elements"></span><span id="CHILD_ELEMENTS"></span>子元素


没有子元素。

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
<td><p><a href="serviceinfo.md" data-raw-source="[ServiceInfo](serviceinfo.md)">ServiceInfo</a></p></td>
<td><p><a href="serviceinfo.md" data-raw-source="[ServiceInfo](serviceinfo.md)">ServiceInfo</a>元素是<a href="serviceinfo-xml-schema.md" data-raw-source="[ServiceInfo XML schema](serviceinfo-xml-schema.md)">ServiceInfo XML 架构</a>的父元素。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


``` syntax
<xs:element name="ServiceNumber" type ="tns:ServiceNumberType" />

<xs:simpleType name="ServiceNumberType">
  <xs:union memberTypes="tns:GUIDType xs:string" />
</xs:simpleType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


ServiceNumber 元素是必需的。

 

 





