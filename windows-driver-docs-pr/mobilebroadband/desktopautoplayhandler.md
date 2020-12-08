---
title: DesktopAutoplayHandler
description: DesktopAutoplayHandler
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c255058b3e3bb4a7439a61af7b88b4ff41c645f3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788585"
---
# <a name="desktopautoplayhandler"></a>DesktopAutoplayHandler

[!include[MBAE deprecation warning](../includes/mbae-deprecation-warning.md)]

当设备已连接并且未设置默认操作时，DesktopAutoplayHandler 元素指定应显示为建议的自动播放操作的桌面应用。 用户插入设备时，会引发自动播放事件。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<DesktopAutoplayHandler>
  text
</DesktopAutoplayHandler>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


没有特性。

## <a name="span-idtext_valuespanspan-idtext_valuespanspan-idtext_valuespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>文本值


指示用于处理自动播放事件的桌面应用程序的字符串。

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
<td><p><a href="windowsinfo.md" data-raw-source="[WindowsInfo](windowsinfo.md)">WindowsInfo</a></p></td>
<td><p><a href="windowsinfo-xml-schema.md" data-raw-source="[WindowsInfo XML schema](windowsinfo-xml-schema.md)">WINDOWSINFO XML 架构</a>的父元素。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


``` syntax
<xs:element name="DesktopAutoplayHandler" type="xs:string" />
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


设置桌面应用时，可在 DesktopAutoplayHandler 元素中指定桌面自动播放处理程序字符串。 你可以从在以下注册表项下注册的处理程序子项名称中检索字符串：

``` syntax
HKLM\Software\Microsoft\Windows\CurrentVersion\Explorer\AutoplayHandlers\Handlers
```

DesktopAutoplayHandler 元素是可选的。

 

 





