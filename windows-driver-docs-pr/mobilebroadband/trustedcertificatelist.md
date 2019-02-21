---
title: TrustedCertificateList
description: TrustedCertificateList
ms.assetid: 116ee448-b0a8-4441-845c-945fc5ae0ddd
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f045ea209aaa1db14ee2a37862c13575634d96a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546118"
---
# <a name="trustedcertificatelist"></a>TrustedCertificateList


TrustedCertificateList 元素指定的操作员的受信任的证书列表。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<TrustedCertificateList>
   child elements
</TrustedCertificateList>
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
<td><p><a href="trustedcertificate-apnxml.md" data-raw-source="[TrustedCertificate](trustedcertificate-apnxml.md)">TrustedCertificate</a></p></td>
<td><p>运算符所信任的证书。</p></td>
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
<td><p><a href="operatorlist.md" data-raw-source="[OperatorList](operatorlist.md)">OperatorList</a></p></td>
<td><p>父元素<a href="apn-xml-schema.md" data-raw-source="[APN XML schema](apn-xml-schema.md)">APN XML 架构</a>。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element ref="TrustedCertificateList" minOccurs="0"/>

<xs:element name="TrustedCertificateList">
  <xs:complexType>
    <xs:sequence>
      <xs:element ref="TrustedCertificate" maxOccurs="unbounded"/>
    </xs:sequence>
  </xs:complexType>
</xs:element>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


TrustedCertificateList 元素是可选的。

 

 





