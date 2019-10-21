---
title: 包（SoftwareInfo - 特权应用程序）
description: 包（SoftwareInfo - 特权应用程序）
ms.assetid: c9b22498-a7b6-4e17-9688-536883aa5844
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 152ed8306f713279a042a91c60ff68517758335c
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323706"
---
# <a name="package-softwareinfo---priviliged-applications"></a>包（SoftwareInfo - 特权应用程序）

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

Package 元素指定应有权访问特权移动宽带接口的应用。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<Package>
  child element
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
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="identity-privapps.md" data-raw-source="[Identity](identity-privapps.md)">标识</a></p></td>
<td><p>应用程序的发布者标识。</p></td>
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
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="privilegedapplications.md" data-raw-source="[PrivilegedApplications](privilegedapplications.md)">PrivilegedApplications</a></p></td>
<td><p>应该有权访问特权移动宽带接口的应用。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


``` syntax
<xs:element name="Package" type="tns:PackageForPrivilegedApplications" maxOccurs="unbounded" />

<xs:complexType name="PackageForPrivilegedApplications">
  <xs:sequence>
    <xs:element name="Identity" type="tns:IdentityForPrivilegedApplicationsType" />
    <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
  </xs:sequence>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


Package 元素是可选的。

 

 





