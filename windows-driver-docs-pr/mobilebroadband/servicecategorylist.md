---
title: ServiceCategoryList
description: ServiceCategoryList
ms.assetid: 69ea35aa-c658-49ed-86bd-815392d157f6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b49386c37c64f7064f9a072061682d78aa3d39a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521256"
---
# <a name="servicecategorylist"></a>ServiceCategoryList

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

ServiceCategoryList 元素指定适用于服务的一个或多个功能类别。 通过指定每个功能类别[ServiceCategory](servicecategory.md)元素。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<ServiceCategorylist>
  child element
</ServiceCategorylist>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


没有特性。

## <a name="span-idtextvaluespanspan-idtextvaluespanspan-idtextvaluespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>文本值


必须包含一个[ServiceCategory](servicecategory.md)元素。

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
<td><p><a href="servicecategory.md" data-raw-source="[ServiceCategory](servicecategory.md)">ServiceCategory</a></p></td>
<td><p>指定适用于服务的一个或多个功能类别。</p></td>
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
<td><p><a href="serviceinfo.md" data-raw-source="[ServiceInfo](serviceinfo.md)">ServiceInfo</a></p></td>
<td><p><a href="serviceinfo.md" data-raw-source="[ServiceInfo](serviceinfo.md)">ServiceInfo</a>元素是父元素<a href="serviceinfo-xml-schema.md" data-raw-source="[ServiceInfo XML schema](serviceinfo-xml-schema.md)">ServiceInfo XML 架构</a>。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="ServiceCategoryList" type="tns:ServiceCategoryListType" />

<xs:complexType name="ServiceCategoryListType">
  <xs:sequence>
    <xs:element name="ServiceCategory" type="tns:ServiceCategoryType" maxOccurs="unbounded" />
    <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
  </xs:sequence>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


以下介绍如何使用服务元数据包中的 ServiceCategoryList 元素：

-   第一个[ServiceCategory](servicecategory.md) ServiceCategoryList 元素中的元素指定服务的主要功能类别。 如何服务是播发、 打包、 出售，并最终由标识用户，则应与匹配的主要功能类别。

-   由于仅通过其主功能类别定义了服务，应指定的一个实例[ServiceCategory](servicecategory.md) ServiceCategoryList 元素中的元素。

-   [ServiceCategory](servicecategory.md)服务元数据的包必须是以下值之一：

    -   Network.MobileBroadband

    -   Network.MobileBroadband.CDMA

    -   Network.MobileBroadband.GSM

ServiceCategoryList 元素是必需的。

 

 





