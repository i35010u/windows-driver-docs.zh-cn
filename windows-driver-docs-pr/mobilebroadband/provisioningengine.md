---
title: ProvisioningEngine
description: ProvisioningEngine
ms.assetid: b6b10145-d554-43be-8682-1355145b3241
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49ce5c65436e9da9d14496c32ec90b32b007bbcd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335270"
---
# <a name="provisioningengine"></a>ProvisioningEngine

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

ProvisioningEngine 元素指定受信任的证书。 这使操作员可以预配 PC 的使用受信任的证书进行签名的包。

有关预配的详细信息，请参阅[帐户预配](account-provisioning.md)。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<ProvisioningEngine>
  child element
</ProvisioningEngine>
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
<td><p><a href="trustedcertificates.md" data-raw-source="[TrustedCertificates](trustedcertificates.md)">TrustedCertificates</a></p></td>
<td><p>指定受信任的证书。</p></td>
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
<td><p><a href="mobilebroadbandinfo.md" data-raw-source="[MobileBroadbandInfo](mobilebroadbandinfo.md)">MobileBroadbandInfo</a></p></td>
<td><p><a href="mobilebroadbandinfo.md" data-raw-source="[MobileBroadbandInfo](mobilebroadbandinfo.md)">MobileBroadbandInfo</a>元素是父元素<a href="mobilebroadbandinfo-xml-schema.md" data-raw-source="[MobileBroadbandInfo XML schema](mobilebroadbandinfo-xml-schema.md)">MobileBroadbandInfo XML 架构</a>。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="ProvisioningEngine" type="tns:ProvisioningEngineType" minOccurs="0" />

<xs:complexType name="ProvisioningEngineType">
  <xs:sequence>
    <xs:element name="TrustedCertificates" type="tns:TrustedCertificateListType" minOccurs="0" />
    <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
  </xs:sequence>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


-   Windows 8、 Windows 8.1 和 Windows 10 允许移动网络运营商可以提供对名为预配包的用户的移动宽带网络设置进行更新的包。

-   若要确保这些预配包来自移动网络运营商，Windows 将验证颁发者名称和从用于预配包进行签名的证书的使用者名称匹配服务元数据包中的描述。

ProvisioningEngine 元素是可选的。

 

 





