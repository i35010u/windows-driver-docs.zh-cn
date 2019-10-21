---
title: TrustedCertificate (MobileBroadbandInfo)
description: TrustedCertificate (MobileBroadbandInfo)
ms.assetid: d22a488d-445e-4011-b881-f2cf49aa4049
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d1123cb5ca55a004d92254cdd2dcdbc6b9a2f89
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323680"
---
# <a name="trustedcertificate-mobilebroadbandinfo"></a>TrustedCertificate (MobileBroadbandInfo)

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

TrustedCertificate 元素指定可信证书的使用者名称和颁发者名称。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<TrustedCertificate>
  child elements
</TrustedCertificate>
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
<td><p><a href="subjectname.md" data-raw-source="[SubjectName](subjectname.md)">SubjectName</a></p></td>
<td><p>受信任的证书的使用者名称。</p></td>
</tr>
<tr class="even">
<td><p><a href="issuername.md" data-raw-source="[IssuerName](issuername.md)">IssuerName</a></p></td>
<td><p>受信任证书的颁发者名称。</p></td>
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
<td><p><a href="trustedcertificates.md" data-raw-source="[TrustedCertificates](trustedcertificates.md)">TrustedCertificates</a></p></td>
<td><p>指定受信任的证书。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


``` syntax
<xs:element name="TrustedCertificate" type="tns:TrustedCertificateType" minOccurs="0" maxOccurs="256" />

<xs:complexType name="TrustedCertificateType">
  <xs:sequence>
    <xs:element name="SubjectName" type="xs:string" />
    <xs:element name="IssuerName" type="xs:string" />
    <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
  </xs:sequence>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


TrustedCertificate 元素是可选的。

 

 





