---
title: LaunchApplicationOnDeviceConnect
description: LaunchApplicationOnDeviceConnect
ms.assetid: d8a5f20a-bd88-4279-9e15-4f20287edfd4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc87de4188efa8cf52467c232c223ca80ed33c66
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525102"
---
# <a name="launchapplicationondeviceconnect"></a>LaunchApplicationOnDeviceConnect

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

LaunchApplicationOnDeviceConnect 元素指定的应用程序时用户插入设备应显示为建议的自动播放操作。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<LaunchApplicationOnDeviceConnect>
  child elements
</LaunchApplicationOnDeviceConnect>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


没有特性。

## <a name="span-idchildelementsspanspan-idchildelementsspanspan-idchildelementsspanchild-elements"></a><span id="Child_elements"></span><span id="child_elements"></span><span id="CHILD_ELEMENTS"></span>子元素


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
<td><p>指定当用户插入设备时应显示为建议的自动播放操作的 UWP 设备应用程序。</p></td>
</tr>
<tr class="even">
<td><p><a href="desktopautoplayhandler.md" data-raw-source="[DesktopAutoplayHandler](desktopautoplayhandler.md)">DesktopAutoplayHandler</a></p></td>
<td><p>指定当用户插入设备时应显示为建议的自动播放操作的桌面应用。</p></td>
</tr>
</tbody>
</table>

 

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
<xs:element name="LaunchApplicationOnDeviceConnect" type ="tns:LaunchApplicationOnDeviceConnectType" />

<xs:complexType name="LaunchApplicationOnDeviceConnectType">
    <xs:choice>
      <xs:element name="AutoplayHandler" type="tns:AutoplayHandlerType" />
      <xs:element name="DesktopAutoplayHandler" type="xs:string" />
      <xs:any namespace="##other" processContents="lax" />
    </xs:choice>
  </xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


必须指定一个 UWP 设备应用或桌面应用程序。 使用[AutoplayHandler](autoplayhandler.md)如果你将指定 UWP 设备应用，并使用[DesktopAutoplayHandler](desktopautoplayhandler.md)如果指定的桌面应用程序。

LaunchApplicationOnDeviceConnect 元素是可选的。

 

 





