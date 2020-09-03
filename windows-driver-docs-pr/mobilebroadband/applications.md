---
title: 应用程序
description: 应用程序
ms.assetid: 40d73650-556e-4221-a679-0b8e9ead4df5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac5570bb76b9d90ba1a0877d4d16f162f19f08d1
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89402896"
---
# <a name="applications"></a>应用程序

[!include[MBAE deprecation warning](../includes/mbae-deprecation-warning.md)]

应用程序元素指定与移动宽带硬件设备关联的应用。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<Applications>
  Child element
</Applications>
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
<td><p><a href="application-softwareinfo-schema.md" data-raw-source="[Application](application-softwareinfo-schema.md)">应用程序</a></p></td>
<td><p>指定在计算机上检测到操作员的移动宽带硬件时要下载的应用。</p></td>
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
<td><p><a href="package.md" data-raw-source="[Package](package.md)">包</a></p></td>
<td><p>指定在计算机上检测到操作员的移动宽带硬件时要下载的应用。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


``` syntax
<xs:element name="Applications" type="tns:ApplicationsType" />

  <xs:complexType name="ApplicationsType">
    <xs:sequence>
      <xs:element name="Application" type="tns:ApplicationType" />
      <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
    </xs:sequence>
  </xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


应用程序元素是可选的。

 

 





