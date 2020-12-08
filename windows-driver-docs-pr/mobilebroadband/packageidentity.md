---
title: PackageIdentity
description: PackageIdentity
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78c81fc3771d700a8221e4752860170eea8dffe3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786243"
---
# <a name="packageidentity"></a>PackageIdentity

[!include[MBAE deprecation warning](../includes/mbae-deprecation-warning.md)]

PackageIdentity 元素指定在用户插入设备时应显示为建议的自动播放操作的 UWP 设备应用。

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
<th>Attribute</th>
<th>类型</th>
<th>必须</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>“属性”</p></td>
<td><p>tns： PackageNameType</p></td>
<td><p>是</p></td>
<td><p>从应用程序清单的标识元素的 "名称" 属性中复制此元素，如 "备注" 中所述。</p></td>
</tr>
<tr class="even">
<td><p>Publisher</p></td>
<td><p>tns： PublisherType</p></td>
<td><p>是</p></td>
<td><p>从应用程序清单的标识元素的发行者特性复制此元素，如 "备注" 中所述。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idchild_elementsspanspan-idchild_elementsspanspan-idchild_elementsspanchild-elements"></a><span id="Child_elements"></span><span id="child_elements"></span><span id="CHILD_ELEMENTS"></span>子元素


没有任何子元素。

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
<td><p><a href="autoplayhandler.md" data-raw-source="[AutoplayHandler](autoplayhandler.md)">AutoplayHandler</a></p></td>
<td><p>指定当用户插入设备时应显示为建议的自动播放操作的 UWP 设备应用。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


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


在应用程序与 Microsoft Store 相关联后，从应用程序清单的标识元素中复制 Name 和 Publisher 属性 &lt; &gt; ，因为关联应用程序的过程将更新应用程序清单。

下面的示例演示如何在 &lt; &gt; 应用程序清单内查看标识元素。

``` syntax
<Identity Name="64022FABRIKAM.FabrikamDeviceApp" Publisher="CN=05558413-FFF6-4AA5-8176-AD43036533FA" Version="1.0.0.0" />
```

PackageIdentity 元素是可选的。

 

 





