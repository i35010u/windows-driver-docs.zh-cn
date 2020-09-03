---
title: DeviceCompanionApplications
description: DeviceCompanionApplications
ms.assetid: 3e0b21a8-aa1f-4f7a-84fc-447bba172794
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1583f729f03ab7f3d3e35f04fe48c2243c1eff6a
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403308"
---
# <a name="devicecompanionapplications"></a>DeviceCompanionApplications

[!include[MBAE deprecation warning](../includes/mbae-deprecation-warning.md)]

DeviceCompanionApplications 元素指定在计算机上检测到操作员的移动宽带硬件时要下载的应用。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<DeviceCompanionApplications>
  child elements
</DeviceCompanionApplications>
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
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="package.md" data-raw-source="[Package](package.md)">包</a></p></td>
<td><p>指定将用于 Microsoft Store 设备应用的包。</p></td>
</tr>
</tbody>
</table>

 

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
<td><p><a href="softwareinfo.md" data-raw-source="[SoftwareInfo](softwareinfo.md)">SoftwareInfo</a></p></td>
<td><p><a href="softwareinfo-xml-schema.md" data-raw-source="[SoftwareInfo XML schema](softwareinfo-xml-schema.md)">SOFTWAREINFO XML 架构</a>的父元素。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


``` syntax
<xs:element name="DeviceCompanionApplications" type="tns:DeviceCompanionApplicationsType" />

<xs:complexType name="DeviceCompanionApplicationsType">
  <xs:sequence>
    <xs:element name="Package" type="tns:PackageType" maxOccurs="unbounded" />
    <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
  </xs:sequence>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


-   指定 DeviceCompanionApplications 元素时，当 Windows 检测到操作员的移动宽带硬件时，将下载指定的应用。

-   包 [标识](identity.md) 和 [应用程序](application-softwareinfo-schema.md) 元素的结构与应用程序清单结构相同。

-   对于 Windows 8、Windows 8.1 和 Windows 10，你只能指定一个包和一个应用程序 ID。 如果指定，则将忽略第二个包或应用程序 ID。

DeviceCompanionApplications 元素是可选的。

 

 





