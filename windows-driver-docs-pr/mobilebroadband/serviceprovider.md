---
title: ServiceProvider
description: ServiceProvider
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c04b1ccc552332ff3a087df304b3794b9e6bea8d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837701"
---
# <a name="serviceprovider"></a>ServiceProvider

[!include[MBAE deprecation warning](../includes/mbae-deprecation-warning.md)]

> [!IMPORTANT]
> 在 Windows 10 版本1709及更高版本中，此字段已通过 COSA 的品牌替换。 COSA for 署名中的字段在 [规划桌面 COSA/APN 数据库提交](planning-your-desktop-cosa-apn-database-submission.md)中进行了介绍。 如果在 Windows 10 版本1709之前面向 Windows 版本，则仍将创建此部分中所述的元数据包。 有关 COSA 的详细信息，请参阅 [COSA 概述](cosa-overview.md)。 

ServiceProvider 元素指定服务提供程序的名称。 它显示在 Windows 连接管理器中，用于显示主提供商网络名称。 如果用户位于漫游网络上，则会显示漫游网络名称。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<ServiceProvider>
  text
</ServiceProvider>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


没有特性。

## <a name="span-idtext_valuespanspan-idtext_valuespanspan-idtext_valuespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>文本值


最多包含20个可打印字符的字符串。

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
<xs:element name="ServiceProvider" type="tns:ProviderNameType"/>

<xs:simpleType name="ProviderNameType">
  <xs:restriction base="xs:string">
    <xs:minLength value="1" />
    <xs:maxLength value="20" />
  </xs:restriction>
</xs:simpleType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


当用户漫游时，ServiceProvider 元素不会显示在 Windows 连接管理器中。

ServiceProvider 元素是必需的。

 

 





