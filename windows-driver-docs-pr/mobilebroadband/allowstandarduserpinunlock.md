---
title: AllowStandardUserPinUnlock
description: AllowStandardUserPinUnlock
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 751a320a013e0ddb2a3bdbf466810039a1929f19
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782560"
---
# <a name="allowstandarduserpinunlock"></a>AllowStandardUserPinUnlock

[!include[MBAE deprecation warning](../includes/mbae-deprecation-warning.md)]

> [!IMPORTANT]
> 从 Windows 10 版本1507开始，此元素已弃用，在未来版本的 Windows 中可能不受支持。

AllowStandardUserPinUnlock 元素指定是否允许标准用户执行 PIN 解锁操作。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


```syntax
<AllowStandardUserPinUnlock>
  text
</ AllowStandardUserPinUnlock >
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


没有特性。

## <a name="span-idtext_valuespanspan-idtext_valuespanspan-idtext_valuespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>文本值


一个布尔值，其中 true 允许标准用户执行 PIN 解锁操作，而 **false** **则** 不允许。

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
<xs:element name="AllowStandardUserPinUnlock" type="xs:boolean" minOccurs="0" />
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


AllowStandardUserPinUnlock 元素是可选的。

 

 





