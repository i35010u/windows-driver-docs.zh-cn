---
title: DeviceCompanionApplications
description: DeviceCompanionApplications
ms.assetid: 3e0b21a8-aa1f-4f7a-84fc-447bba172794
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b9dcb11928c0985c8c4daf2a621453d82ddb4e4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534873"
---
# <a name="devicecompanionapplications"></a>DeviceCompanionApplications

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

DeviceCompanionApplications 元素指定在 PC 上检测到操作员的移动宽带硬件时将下载的应用。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<DeviceCompanionApplications>
  child elements
</DeviceCompanionApplications>
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
<td><p><a href="package.md" data-raw-source="[Package](package.md)">包</a></p></td>
<td><p>指定将用于 Microsoft Store 应用设备应用程序的包。</p></td>
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
<td><p><a href="softwareinfo.md" data-raw-source="[SoftwareInfo](softwareinfo.md)">SoftwareInfo</a></p></td>
<td><p>父元素<a href="softwareinfo-xml-schema.md" data-raw-source="[SoftwareInfo XML schema](softwareinfo-xml-schema.md)">SoftwareInfo XML 架构</a>。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


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


-   当指定 DeviceCompanionApplications 元素时，当 Windows 检测到的操作员的移动宽带硬件，将会下载指定的应用程序。

-   包的结构[标识](identity.md)并[应用程序](application-softwareinfo-schema.md)元素都完全相同的应用程序清单结构。

-   对于 Windows 8、 Windows 8.1 和 Windows 10，您可以指定只有一个包和一个应用程序 id。 如果指定该，将忽略第二个包或应用程序 ID。

DeviceCompanionApplications 元素是可选的。

 

 





