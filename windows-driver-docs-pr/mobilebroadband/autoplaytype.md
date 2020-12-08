---
title: AutoplayType
description: AutoplayType
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c93fdc004e6b83cbf012b3840125ab07d188ad57
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782503"
---
# <a name="autoplaytype"></a>AutoplayType

[!include[MBAE deprecation warning](../includes/mbae-deprecation-warning.md)]

AutoplayType 元素指定自动播放事件是设备事件还是内容事件。 自动播放会确定设备类型，并为非卷设备引发设备事件，或为卷设备引发内容事件。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<AutoplayType>
  type
</AutoplayType>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


没有特性。

## <a name="span-idtext_valuespanspan-idtext_valuespanspan-idtext_valuespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>文本值


一个字符串，其值为 "Device" 或值为 "Content"。

## <a name="span-idchild_elementsspanspan-idchild_elementsspanspan-idchild_elementsspanchild-elements"></a><span id="Child_elements"></span><span id="child_elements"></span><span id="CHILD_ELEMENTS"></span>子元素


没有任何子元素。

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
<td><p><a href="autoplayhandler.md" data-raw-source="[AutoplayHandler](autoplayhandler.md)">AutoplayHandler</a></p></td>
<td><p>指定当用户插入设备时应显示为建议的自动播放操作的 UWP 设备应用。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


``` syntax
<xs:element name="AutoplayType" type="tns:AutoplayTypeType" />

<xs:simpleType name="AutoplayTypeType">
  <xs:restriction base="xs:string">
     <xs:enumeration value="Device" />
     <xs:enumeration value="Content" />
  </xs:restriction>
</xs:simpleType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


AutoplayType 元素是可选的。

 

 





