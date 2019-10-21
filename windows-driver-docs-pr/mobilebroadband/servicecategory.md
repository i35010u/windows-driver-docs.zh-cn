---
title: ServiceCategory
description: ServiceCategory
ms.assetid: 770cb127-808f-4d77-905e-66064553d3d7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d1a3b6977ae653396ba2c78986d32e570ae63db
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323650"
---
# <a name="servicecategory"></a>ServiceCategory

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

ServiceCategory 元素指定适用于服务的功能类别。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<ServiceCategory>
  text
</ServiceCategory>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


没有特性。

## <a name="span-idtext_valuespanspan-idtext_valuespanspan-idtext_valuespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>文本值


必须包含一个 ServiceCategory 元素。

## <a name="span-idchild_elementsspanspan-idchild_elementsspanspan-idchild_elementsspanchild-elements"></a><span id="Child_elements"></span><span id="child_elements"></span><span id="CHILD_ELEMENTS"></span>子元素


没有子元素。

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
<td><p><a href="servicecategorylist.md" data-raw-source="[ServiceCategoryList](servicecategorylist.md)">ServiceCategoryList</a></p></td>
<td><p><a href="servicecategorylist.md" data-raw-source="[ServiceCategoryList](servicecategorylist.md)">ServiceCategoryList</a>元素指定应用于服务的功能类别。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


``` syntax
<xs:element name="ServiceCategory" type="tns:ServiceCategoryType" maxOccurs="unbounded" />

<xs:simpleType name="ServiceCategoryType">
    <xs:union memberTypes="tns:ServiceCategoryTypeEnumeration xs:string"/>
</xs:simpleType>

<xs:simpleType name="ServiceCategoryTypeEnumeration">
  <xs:restriction base="xs:string">
    <xs:enumeration value="Network"/>
    <xs:enumeration value="Network.MobileBroadband"/>
    <xs:enumeration value="Other"/>
  </xs:restriction>
</xs:simpleType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


下面讨论了如何在服务元数据包中使用[ServiceCategoryList](servicecategorylist.md)元素：

-   [ServiceCategoryList](servicecategorylist.md)元素中的第一个 ServiceCategory 元素指定服务的主要功能类别。 主要功能类别应该与服务的播发、打包、销售和最终标识方式匹配。

-   由于服务只能由其主要功能类别定义，因此，只应在[ServiceCategoryList](servicecategorylist.md)元素中指定 ServiceCategory 元素的一个实例。

-   服务元数据包的 ServiceCategory 必须是以下各项之一：

    -   Network.MobileBroadband

    -   MobileBroadband. CDMA

    -   MobileBroadband

ServiceCategory 元素是必需的。

 

 





