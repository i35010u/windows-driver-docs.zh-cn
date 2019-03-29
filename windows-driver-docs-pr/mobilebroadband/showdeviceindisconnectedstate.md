---
title: ShowDeviceInDisconnectedState
description: ShowDeviceInDisconnectedState
ms.assetid: f2f517dd-68e5-4013-83ee-777579562db3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7cec04a76a0269e7864a146b3de6ed32418ffa3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569316"
---
# <a name="showdeviceindisconnectedstate"></a>ShowDeviceInDisconnectedState

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

ShowDeviceInDisconnectedState 元素应设置为**false**因为不适用于 Windows 8、 Windows 8.1 和 Windows 10 中的服务元数据包。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<ShowDeviceInDisconnectedState>
  text
</ShowDeviceInDisconnectedState>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


没有特性。

## <a name="span-idtextvaluespanspan-idtextvaluespanspan-idtextvaluespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>文本值


应设置为**false**因为不适用于 Windows 8、 Windows 8.1 和 Windows 10 中的服务元数据包。

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
<td><p><a href="windowsinfo.md" data-raw-source="[WindowsInfo](windowsinfo.md)">WindowsInfo</a></p></td>
<td><p>父元素<a href="windowsinfo-xml-schema.md" data-raw-source="[WindowsInfo XML schema](windowsinfo-xml-schema.md)">WindowsInfo XML 架构</a>。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="ShowDeviceInDisconnectedState" type="xs:boolean" default="false" />
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


ShowDeviceInDisconnectedState 元素是必需的。

 

 





