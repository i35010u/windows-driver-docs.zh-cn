---
title: ShowDeviceInDisconnectedState
description: ShowDeviceInDisconnectedState
ms.assetid: f2f517dd-68e5-4013-83ee-777579562db3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f2324c4b7bfa056f2d1c12d96b1b4f5efe421d5
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403168"
---
# <a name="showdeviceindisconnectedstate"></a>ShowDeviceInDisconnectedState

[!include[MBAE deprecation warning](../includes/mbae-deprecation-warning.md)]

由于 ShowDeviceInDisconnectedState 元素不适用于 Windows 8、Windows 8.1 和 Windows 10 中的服务元数据包，因此应将其设置为 **false** 。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<ShowDeviceInDisconnectedState>
  text
</ShowDeviceInDisconnectedState>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


没有特性。

## <a name="span-idtext_valuespanspan-idtext_valuespanspan-idtext_valuespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>文本值


应设置为 **false** ，因为它不适用于 windows 8、Windows 8.1 和 windows 10 中的服务元数据包。

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
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="windowsinfo.md" data-raw-source="[WindowsInfo](windowsinfo.md)">WindowsInfo</a></p></td>
<td><p><a href="windowsinfo-xml-schema.md" data-raw-source="[WindowsInfo XML schema](windowsinfo-xml-schema.md)">WINDOWSINFO XML 架构</a>的父元素。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


``` syntax
<xs:element name="ShowDeviceInDisconnectedState" type="xs:boolean" default="false" />
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


ShowDeviceInDisconnectedState 元素是必需的。

 

 





