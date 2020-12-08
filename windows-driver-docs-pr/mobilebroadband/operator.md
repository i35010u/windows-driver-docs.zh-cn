---
title: 运算符
description: 运算符
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a11245af89dadeaf27785711f49d1912987ae22
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805267"
---
# <a name="operator"></a>运算符


Operator 元素指定 APN 数据库中包含的操作员的详细信息。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<Operator name=”xs:string” AccountExperienceURL=”xs:anyURI” OperatorGUID=”GUID”>
  child elements
</Operator>
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
<th>Attribute</th>
<th>类型</th>
<th>必须</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>“属性”</p></td>
<td><p>xs:string</p></td>
<td><p>是</p></td>
<td><p>操作员的名称和国家/地区。</p>
<p>示例： Contoso (阿根廷) </p></td>
</tr>
<tr class="even">
<td><p>AccountExperienceURL</p></td>
<td><p>xs:anyURI</p></td>
<td><p>否</p></td>
<td><p>用于配置移动宽带的操作员网站的 URL。</p></td>
</tr>
<tr class="odd">
<td><p>OperatorGUID</p></td>
<td><p>GUID</p></td>
<td><p>否</p></td>
<td><p>用于标识运算符的 GUID。</p></td>
</tr>
</tbody>
</table>

 

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
<td><p><a href="hardwareidlist-apnxml.md" data-raw-source="[HardwareIdList](hardwareidlist-apnxml.md)">HardwareIdList</a></p></td>
<td><p>分配给操作员的硬件 Id 列表。</p></td>
</tr>
<tr class="even">
<td><p><a href="connectioninfolist.md" data-raw-source="[ConnectionInfoList](connectioninfolist.md)">ConnectionInfoList</a></p></td>
<td><p>访问字符串的列表。</p></td>
</tr>
<tr class="odd">
<td><p><a href="trustedcertificatelist.md" data-raw-source="[TrustedCertificateList](trustedcertificatelist.md)">TrustedCertificateList</a></p></td>
<td><p>受信任的证书列表，用于验证帐户预配是否由操作员拥有的购买网站提供。</p></td>
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
<td><p><a href="operatorlist.md" data-raw-source="[OperatorList](operatorlist.md)">OperatorList</a></p></td>
<td><p><a href="apn-schema-definition.md" data-raw-source="[APN XML schema](apn-schema-definition.md)">APN XML 架构</a>的父元素。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


``` syntax
<xs:element name="Operator">
  <xs:complexType>
    <xs:sequence>
      <xs:element ref="HardwareIdList"/>
      <xs:element ref="ConnectionInfoList"/>
      <xs:element ref="TrustedCertificateList" minOccurs="0"/>
    </xs:sequence>
    <xs:attribute name="name" type="xs:string" use="required"/>
    <xs:attribute name="AccountExperienceURL" type="xs:anyURI" use="optional"/>
    <xs:attribute name="OperatorGUID" type="GUID" use="optional"/>
  </xs:complexType>
</xs:element>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


Operator 元素是必需的。

 

 





