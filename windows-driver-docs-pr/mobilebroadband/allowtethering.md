---
title: AllowTethering
description: AllowTethering
ms.assetid: f9b92c46-5e0e-447a-b571-bf549e9a749d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d65981a1967012b5fe091da6d6da90cadd90f3ef
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327811"
---
# <a name="allowtethering"></a>AllowTethering

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

AllowTethering 元素指定用户是否是始终允许，永远不会允许，或允许权利检查后使用 Internet 共享。

**请注意**  如果此元素配置为允许授权检查后，必须指定[DeviceNotificationHandler](devicenotificationhandler.md)将处理权利检查在应用中。

 

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<AllowTethering>
  text
</AllowTethering>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


没有特性。

## <a name="span-idtextvaluespanspan-idtextvaluespanspan-idtextvaluespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>文本值


指示 Internet 共享是始终允许，永远不会允许，还是权利检查后，允许的字符串。

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
<td><p><a href="networkconfiguration.md" data-raw-source="[NetworkConfiguration](networkconfiguration.md)">NetworkConfiguration</a></p></td>
<td><p>指定的采购和 Internet 移动宽带的配置文件，以使用或标准用户是否可以执行 PIN 解锁操作。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="name="AllowTethering" type="tns:TetheringAllowedType" minOccurs="0" />

<xs:simpleType name="TetheringAllowedType">  
  <xs:restriction base="xs:string">
    <xs:enumeration value="Never"/>
    <xs:enumeration value="Always"/>
    <xs:enumeration value="EntitlementCheckRequired"/>
  </xs:restriction>
</xs:simpleType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


此元素是仅适用于 Windows 8.1 和 Windows 10。

AllowTethering 元素是可选的。

 

 





