---
title: 包 (SoftwareInfo)
description: 包 (SoftwareInfo)
ms.assetid: f15f0ffe-593d-4007-8002-4d593d18dd9a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8cf9d944b5958f9cafeb833f0b48543e4ba21d19
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403310"
---
# <a name="package-softwareinfo"></a>包 (SoftwareInfo)

[!include[MBAE deprecation warning](../includes/mbae-deprecation-warning.md)]

Package 元素指定在计算机上检测到操作员的移动宽带硬件时要下载的应用。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<Package>
  child elements
</Package>
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
<td><p><a href="identity.md" data-raw-source="[Identity](identity.md)">标识</a></p></td>
<td><p>应用程序的发布者标识。</p></td>
</tr>
<tr class="even">
<td><p><a href="applications.md" data-raw-source="[Applications](applications.md)">应用程序</a></p></td>
<td><p>检测到移动宽带硬件设备时将下载的应用。</p></td>
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
<xs:element name="Package" type="tns:PackageType" maxOccurs="unbounded" />

<xs:complexType name="PackageType">
    <xs:sequence>
        <xs:element name="Identity" type="tns:IdentityType" />
        <xs:element name="Applications" type="tns:ApplicationsType" />
      <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
    </xs:sequence>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


Package 元素是可选的。

 

 





