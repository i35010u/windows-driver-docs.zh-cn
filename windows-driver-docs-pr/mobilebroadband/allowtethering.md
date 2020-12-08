---
title: AllowTethering
description: AllowTethering
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e1c1f9efec37bc05de377983fe310e142913116
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782557"
---
# <a name="allowtethering"></a>AllowTethering

[!include[MBAE deprecation warning](../includes/mbae-deprecation-warning.md)]

AllowTethering 元素指定是始终允许还是从不允许用户，或在权利检查后允许用户使用 Internet 共享。

**注意**  
如果此元素配置为在授权检查后允许，则必须在应用中指定将处理权限检查的 [DeviceNotificationHandler](devicenotificationhandler.md) 。

 

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<AllowTethering>
  text
</AllowTethering>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


没有特性。

## <a name="span-idtext_valuespanspan-idtext_valuespanspan-idtext_valuespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>文本值


一个字符串，指示是否始终允许、不允许或在权利检查后允许 Internet 共享。

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
<td><p><a href="networkconfiguration.md" data-raw-source="[NetworkConfiguration](networkconfiguration.md)">NetworkConfiguration</a></p></td>
<td><p>指定要使用的购买和 Internet 移动宽带配置文件，或者标准用户是否可以执行 PIN 解锁操作。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


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


此元素仅适用于 Windows 8.1 和 Windows 10。

AllowTethering 元素是可选的。

 

 





