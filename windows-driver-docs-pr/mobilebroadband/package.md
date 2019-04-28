---
title: 包 (SoftwareInfo)
description: 包 (SoftwareInfo)
ms.assetid: f15f0ffe-593d-4007-8002-4d593d18dd9a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 612d0a90275e67c0988c8254682a6f7b3cb2d065
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347570"
---
# <a name="package-softwareinfo"></a>包 (SoftwareInfo)

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

包元素指定在 PC 上检测到操作员的移动宽带硬件时将下载的应用。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<Package>
  child elements
</Package>
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
<td><p><a href="identity.md" data-raw-source="[Identity](identity.md)">标识</a></p></td>
<td><p>发布服务器标识的应用程序。</p></td>
</tr>
<tr class="even">
<td><p><a href="applications.md" data-raw-source="[Applications](applications.md)">Applications</a></p></td>
<td><p>当检测到移动宽带硬件设备时，将下载应用。</p></td>
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


包元素是可选的。

 

 





