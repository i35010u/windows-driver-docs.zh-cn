---
title: WindowsInfo
description: WindowsInfo
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60e06f3b3554ac2b3510ef4284a6d648bdb67f7c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820630"
---
# <a name="windowsinfo"></a>WindowsInfo

[!include[MBAE deprecation warning](../includes/mbae-deprecation-warning.md)]

WindowsInfo 元素是 [WINDOWSINFO XML 架构](windowsinfo-xml-schema.md)的父元素。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<WindowsInfo>
  child elements
</WindowsInfo>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


没有特性。

## <a name="span-idchild_elementsspanspan-idchild_elementsspanspan-idchild_elementsspanchild-elements"></a><span id="Child_elements"></span><span id="child_elements"></span><span id="CHILD_ELEMENTS"></span>子元素


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
<td><p><a href="showdeviceindisconnectedstate.md" data-raw-source="[ShowDeviceInDisconnectedState](showdeviceindisconnectedstate.md)">ShowDeviceInDisconnectedState</a></p></td>
<td><p>此值应设置为 <strong>false</strong> ，因为它不适用于 windows 8、Windows 8.1 和 windows 10 中的服务元数据包。</p></td>
</tr>
<tr class="even">
<td><p><a href="launchdevicestageondeviceconnect.md" data-raw-source="[LaunchDeviceStageOnDeviceConnect](launchdevicestageondeviceconnect.md)">LaunchDeviceStageOnDeviceConnect</a></p></td>
<td><p>此值应设置为 <strong>false</strong> ，因为它不适用于 windows 8、Windows 8.1 和 windows 10 中的服务元数据包。</p></td>
</tr>
<tr class="odd">
<td><p><a href="launchdevicestagefromexplorer.md" data-raw-source="[LaunchDeviceStageFromExplorer](launchdevicestagefromexplorer.md)">LaunchDeviceStageFromExplorer</a></p></td>
<td><p>此值应设置为 <strong>false</strong> ，因为它不适用于 windows 8、Windows 8.1 和 windows 10 中的服务元数据包。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idparent_elementsspanspan-idparent_elementsspanspan-idparent_elementsspanparent-elements"></a><span id="Parent_elements"></span><span id="parent_elements"></span><span id="PARENT_ELEMENTS"></span>父元素


没有父元素。

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


``` syntax
<xs:element name="WindowsInfo" type="tns:WindowsInfoType" />

<xs:complexType name="WindowsInfoType">
  <xs:sequence>
    <xs:element name="ShowDeviceInDisconnectedState" type="xs:boolean" default="false" />
    <xs:element name="LaunchDeviceStageOnDeviceConnect" type="xs:boolean" default="false" minOccurs="0" />
    <xs:element name="LaunchDeviceStageFromExplorer" type="xs:boolean" default="false" minOccurs="0" />
    <xs:element ref="v2:LaunchApplicationOnDeviceConnect" minOccurs="0" />
    <xs:element ref="v2:WindowsHardwareLogoCertified" minOccurs="0" />
  </xs:sequence>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


WindowsInfo 元素是必需的。

 

 





