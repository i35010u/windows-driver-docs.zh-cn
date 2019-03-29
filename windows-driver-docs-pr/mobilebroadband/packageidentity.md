---
title: PackageIdentity
description: PackageIdentity
ms.assetid: b5533962-ea42-416e-bbd8-ce9dce1a9a40
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb842736555a1b824dcefd98ee0bd1590179cba5
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349446"
---
# <a name="packageidentity"></a>PackageIdentity

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

PackageIdentity 元素指定当用户插入设备时应显示为建议的自动播放操作的 UWP 设备应用程序。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<PackageIdentity Name=”tns:PackageNameType” Publisher=”tns:PublisherType” />
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
<td><p>tns:PackageNameType</p></td>
<td><p>是</p></td>
<td><p>从备注中描述的应用程序清单的标识元素的 Name 属性中复制此元素。</p></td>
</tr>
<tr class="even">
<td><p>发布者</p></td>
<td><p>tns:PublisherType</p></td>
<td><p>是</p></td>
<td><p>从应用程序清单的标识元素，在备注中所述的发布服务器属性中复制此元素。</p></td>
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
<td><p><a href="autoplayhandler.md" data-raw-source="[AutoplayHandler](autoplayhandler.md)">AutoplayHandler</a></p></td>
<td><p>指定当用户插入设备时应显示为建议的自动播放操作的 UWP 设备应用程序。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="PackageIdentity" type="tns:PackageIdentityType" />

  <xs:complexType name="PackageIdentityType">
    <xs:attribute name="Name" type="tns:PackageNameType" use="required" />
    <xs:attribute name="Publisher" type="tns:PublisherType" use="required" />
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
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


从应用程序清单中复制名称和发布服务器属性&lt;标识&gt;元素后已与 Microsoft Store 中，关联应用程序，因为关联您的应用程序的过程将更新应用程序清单。

下面是如何的示例&lt;标识&gt;元素可能看起来在应用程序清单。

``` syntax
<Identity Name="64022FABRIKAM.FabrikamDeviceApp" Publisher="CN=05558413-FFF6-4AA5-8176-AD43036533FA" Version="1.0.0.0" />
```

PackageIdentity 元素是可选的。

 

 





