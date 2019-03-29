---
title: TrustedCertificate（APN 元素）
description: TrustedCertificate（APN 元素）
ms.assetid: 8b1b09ab-7ab8-4d6d-9ea6-395a109def91
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53061611095ebec830ce4fb80af4424cd2319893
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567597"
---
# <a name="trustedcertificate-apn-element"></a>TrustedCertificate（APN 元素）


TrustedCertificate 元素为指定的运算符指定受信任的证书。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<TrustedCertificate SubjectName=”xs:string” IssuerName=”xs:string”>
</TrustedCertificate>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>特性</th>
<th>在任务栏的搜索框中键入</th>
<th>必需</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SubjectName</p></td>
<td><p>xs:string</p></td>
<td><p>是</p></td>
<td><p>证书使用者名称。</p></td>
</tr>
<tr class="even">
<td><p>IssuerName</p></td>
<td><p>xs:string</p></td>
<td><p>是</p></td>
<td><p>证书的颁发者名称。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idchildelementsspanspan-idchildelementsspanspan-idchildelementsspanchild-elements"></a><span id="Child_elements"></span><span id="child_elements"></span><span id="CHILD_ELEMENTS"></span>子元素


没有子元素。

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
<td><p><a href="trustedcertificatelist.md" data-raw-source="[TrustedCertificateList](trustedcertificatelist.md)">TrustedCertificateList</a></p></td>
<td><p>运算符中指定受信任的证书的列表。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element ref="TrustedCertificate" maxOccurs="unbounded"/>

<xs:element name="TrustedCertificate">
  <xs:complexType>
    <xs:attribute name="SubjectName" type="xs:string" use="required"/>
    <xs:attribute name="IssuerName" type="xs:string" use="required"/>
  </xs:complexType>
</xs:element>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


TrustedCertificate 元素是可选的。

 

 





