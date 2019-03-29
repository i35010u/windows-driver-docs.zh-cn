---
title: 标识（SoftwareInfo - 特权应用程序）
description: 标识（SoftwareInfo - 特权应用程序）
ms.assetid: 405ec2ee-ea4a-468b-b75b-365ffce03cdb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94396720678c3baf9701ac801379e4a4a5b93a35
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464369"
---
# <a name="identity-softwareinfo---priviliged-applications"></a>标识（SoftwareInfo - 特权应用程序）

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

标识元素指定的发布服务器标识和应用程序清单的应用的名称。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<Identity Name=”tns:AsciiIdentifierType” Publisher=”tns:DistinguishedNameType” AccessCustomDriver=”xs:boolean” />
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
<td><p>“属性”</p></td>
<td><p>tns:AsciiIdentifierType</p></td>
<td><p>是</p></td>
<td><p>应用程序中指定应用程序清单文件。</p></td>
</tr>
<tr class="even">
<td><p>发布者</p></td>
<td><p>tns:DistinguishedNameType</p></td>
<td><p>是</p></td>
<td><p>应用的发布服务器标识。</p></td>
</tr>
<tr class="odd">
<td><p>AccessCustomDriver</p></td>
<td><p>xs:boolean</p></td>
<td><p>否</p></td>
<td><p>如果应用程序应有权访问自定义驱动程序，将此值设置为<strong>，则返回 true</strong>。</p></td>
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
<td><p><a href="package-privapps.md" data-raw-source="[Package](package-privapps.md)">包</a></p></td>
<td><p>指定的应用程序应具有访问权限的特权的移动宽带接口。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="Identity" type="tns:IdentityForPrivilegedApplicationsType" />

<xs:complexType name="IdentityForPrivilegedApplicationsType">
  <xs:attribute name="Name" type="tns:PackageNameType" use="required"/>
  <xs:attribute name="Publisher" type="tns:PublisherType" use="required"/>
  <xs:attribute name="AccessCustomDriver" type="xs:boolean" />
</xs:complexType>

<xs:simpleType name="PackageNameType">
  <xs:restriction base="tns:AsciiIdentifierType">
    <xs:minLength value="3"/>
    <xs:maxLength value="50"/>
  </xs:restriction>
</xs:simpleType>

<xs:simpleType name="PublisherType">
  <xs:restriction base="tns:DistinguishedNameType">
    <xs:maxLength value="8192"/>
  </xs:restriction>
</xs:simpleType>

<xs:simpleType name="AsciiIdentifierType">
  <xs:restriction base="tns:AllowedAsciiCharSetType">
    <xs:pattern value="[^_ ]+"/>
  </xs:restriction>
</xs:simpleType>

<xs:simpleType name="DistinguishedNameType">
  <xs:restriction base="tns:NonEmptyStringType">
    <xs:pattern value="(CN|L|O|OU|E|C|S|STREET|T|G|I|SN|DC|SERIALNUMBER|(OID\.(0|[1-9][0-9]*)(\.(0|[1-9][0-9]*))+))=(([^,+="&lt;&gt;#;])+|".*")(, ((CN|L|O|OU|E|C|S|STREET|T|G|I|SN|DC|SERIALNUMBER|(OID\.(0|[1-9][0-9]*)(\.(0|[1-9][0-9]*))+))=(([^,+="&lt;&gt;#;])+|".*")))*"/>
  </xs:restriction>
</xs:simpleType>

<xs:simpleType name="NonEmptyStringType">
  <xs:restriction base="xs:string">
    <xs:minLength value="1"/>
    <xs:maxLength value="32767"/>
    <xs:pattern value="[^\s]|([^\s].*[^\s])"/>
  </xs:restriction>
</xs:simpleType>

<xs:simpleType name="AllowedAsciiCharSetType">
  <xs:restriction base="tns:NonEmptyStringType">
    <xs:pattern value="[-_. A-Za-z0-9]+"/>
  </xs:restriction>
</xs:simpleType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


标识元素是可选的。

 

 





