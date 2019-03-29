---
title: SoftwareInfo
description: SoftwareInfo
ms.assetid: 736040e9-76cd-4f59-b16a-1e8fc3b687fa
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae6df337514213881f0e73f4b7e109fadb9bb9db
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576769"
---
# <a name="softwareinfo"></a>SoftwareInfo

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

SoftwareInfo 元素是父元素[SoftwareInfo XML 架构](softwareinfo-xml-schema.md)。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<SoftwareInfo>
  child elements
</SoftwareInfo>
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
<td><p><a href="devicecompanionapplications.md" data-raw-source="[DeviceCompanionApplications](devicecompanionapplications.md)">DeviceCompanionApplications</a></p></td>
<td><p>指定在 PC 上检测到操作员的移动宽带硬件时将下载的应用。</p></td>
</tr>
<tr class="even">
<td><p><a href="privilegedapplications.md" data-raw-source="[PrivilegedApplications](privilegedapplications.md)">PrivilegedApplications</a></p></td>
<td><p>指定的应用程序有权访问特权的移动宽带接口。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idparentelementsspanspan-idparentelementsspanspan-idparentelementsspanparent-elements"></a><span id="Parent_elements"></span><span id="parent_elements"></span><span id="PARENT_ELEMENTS"></span>父元素


没有父元素。

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="SoftwareInfo" type="tns:SoftwareInfoType" />

<xs:complexType name="SoftwareInfoType">
  <xs:choice>
    <xs:sequence>
      <xs:element name="DeviceCompanionApplications" type="tns:DeviceCompanionApplicationsType" />
      <xs:element name="PrivilegedApplications" type="tns:PrivilegedApplicationsType" minOccurs="0" />
      <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
    </xs:sequence>
    <xs:element name="PrivilegedApplications" type="tns:PrivilegedApplicationsType" />
  </xs:choice>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


SoftwareInfo 元素是必需的。

 

 





