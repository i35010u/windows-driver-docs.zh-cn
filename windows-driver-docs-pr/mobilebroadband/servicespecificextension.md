---
title: ServiceSpecificExtension
description: ServiceSpecificExtension
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c34ac5c0dedde29453d103bf71b5bf8439554213
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828489"
---
# <a name="servicespecificextension"></a>ServiceSpecificExtension

[!include[MBAE deprecation warning](../includes/mbae-deprecation-warning.md)]

ServiceSpecificExtension 元素指定 MobileBroadbandInfo.xml 文件的相对位置。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<ServiceSpecificExtension 
  name = “xs:anyURI”>
  text
</ServiceSpecificExtension>
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
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>命名空间</p></td>
<td><p>xs:anyURI</p></td>
<td><p>是</p></td>
<td><p>用于 MobileBroadbandInfo.xml 文件的命名空间的 URI。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idtext_valuespanspan-idtext_valuespanspan-idtext_valuespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>文本值


包含 MobileBroadbandInfo 架构的 XML 文件的名称。

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
<td><p><a href="serviceinfo.md" data-raw-source="[ServiceInfo](serviceinfo.md)">ServiceInfo</a></p></td>
<td><p><a href="serviceinfo.md" data-raw-source="[ServiceInfo](serviceinfo.md)">ServiceInfo</a>元素是<a href="serviceinfo-xml-schema.md" data-raw-source="[ServiceInfo XML schema](serviceinfo-xml-schema.md)">ServiceInfo XML 架构</a>的父元素。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


``` syntax
<xs:element name="ServiceSpecificExtension" type="tns:ServiceSpecificExtensionType" minOccurs="0" />

<xs:complexType name="ServiceSpecificExtensionType">
  <xs:simpleContent>
    <xs:extension base="xs:string">
      <xs:attribute name="namespace" type="xs:anyURI" use="required" />
    </xs:extension>
  </xs:simpleContent>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


ServiceSpecificExtension 元素是必需的。

 

 





