---
title: DesktopAutoplayHandler
description: DesktopAutoplayHandler
ms.assetid: e1a07580-36dd-4618-b522-3f7605c9b87b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 578f2071d1847814bc878de55e704875cf6f9f80
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554167"
---
# <a name="desktopautoplayhandler"></a>DesktopAutoplayHandler

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

DesktopAutoplayHandler 元素指定的桌面应用，应显示为建议的自动播放操作时将设备连接并设置没有默认操作。 用户插入设备时，将引发自动播放事件。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<DesktopAutoplayHandler>
  text
</DesktopAutoplayHandler>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


没有特性。

## <a name="span-idtextvaluespanspan-idtextvaluespanspan-idtextvaluespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>文本值


指示处理自动播放事件桌面应用程序的字符串。

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
<xs:element name="DesktopAutoplayHandler" type="xs:string" />
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


当设置桌面应用程序时 DesktopAutoplayHandler 元素中指定桌面自动播放处理程序的字符串。 可以从以下注册表项下注册处理程序子项名称来检索该字符串：

``` syntax
HKLM\Software\Microsoft\Windows\CurrentVersion\Explorer\AutoplayHandlers\Handlers
```

DesktopAutoplayHandler 元素是可选的。

 

 





