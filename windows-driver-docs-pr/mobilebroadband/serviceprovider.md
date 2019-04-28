---
title: ServiceProvider
description: ServiceProvider
ms.assetid: 6fa22f4d-9be9-4d02-b610-e20bed4958e9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d170aa38f54eaf91340aa8d9c02ffc6765eae6b4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335400"
---
# <a name="serviceprovider"></a>ServiceProvider

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

> [!IMPORTANT]
> 在 Windows 10 版本 1709年及更高版本，此字段已替换为通过 COSA 品牌。 品牌 COSA 中的字段上的说明[规划你的桌面 COSA/APN 数据库提交](planning-your-desktop-cosa-apn-database-submission.md)。 如果你面向的 Windows 10，版本 1709 之前, 的 Windows 版本仍会创建元数据包在本部分中所述。 有关 COSA 详细信息，请参阅[COSA 概述](cosa-overview.md)。 

服务提供商处元素指定服务提供程序的名称。 它是显示在 Windows 连接管理器中显示的家用供应商网络名称。 如果用户是漫游网络上漫游的网络名称改为显示。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<ServiceProvider>
  text
</ServiceProvider>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


没有特性。

## <a name="span-idtextvaluespanspan-idtextvaluespanspan-idtextvaluespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>文本值


最多 20 个可打印字符的字符串。

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
<td><p><a href="serviceinfo.md" data-raw-source="[ServiceInfo](serviceinfo.md)">ServiceInfo</a></p></td>
<td><p><a href="serviceinfo.md" data-raw-source="[ServiceInfo](serviceinfo.md)">ServiceInfo</a>元素是父元素<a href="serviceinfo-xml-schema.md" data-raw-source="[ServiceInfo XML schema](serviceinfo-xml-schema.md)">ServiceInfo XML 架构</a>。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


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


漫游用户时的服务提供商处元素不会显示 Windows 连接管理器中。

服务提供商处元素是必需的。

 

 





