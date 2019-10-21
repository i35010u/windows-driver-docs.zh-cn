---
title: LanguageNeutralIdentifier
description: LanguageNeutralIdentifier
ms.assetid: 38713565-464c-4b12-9076-331ae43e01e8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce4ea9d3ace366695c79f423281f3c98bc7ab7ba
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323658"
---
# <a name="languageneutralidentifier"></a>LanguageNeutralIdentifier

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

LanguageNeutralIdentifier 元素指定一个 GUID，该 GUID 标识服务元数据包（独立于其区域设置）。 LanguageNeutralIdentifier 元素允许使用同一 GUID 来标识同一服务的服务元数据包的一个或多个本地化版本。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<LanguageNeutralIdentifier>
  text
</LanguageNeutralIdentifier>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


没有特性。

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
<td><p><a href="relationships.md" data-raw-source="[Relationships](relationships.md)">关系</a></p></td>
<td><p><a href="relationships.md" data-raw-source="[Relationships](relationships.md)">关系</a>元素指定用于在设备元数据缓存中跟踪设备元数据包的数据。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


``` syntax
<xs:element name="LanguageNeutralIdentifier" type="tns:GUIDType" minOccurs="0" />
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


LanguageNeutralIdentifier 元素允许在同一设备的设备元数据包的一个或多个本地化版本中使用相同的 GUID。

例如，如果您为三个区域设置（例如 EN-US、JA-JP 和 AR-SA）发布一个设备，则可以为每个区域设置的设备创建单独的元数据包。 通过对这些包中的 LanguageNeutralIdentifier 元素使用公共 GUID，可以通过浏览其 PackageInfo XML 文档轻松搜索设备的元数据包。

**重要**   LanguageNeutralIdentifier 元素不由操作系统的任何组件使用。 它保留供 OEM、独立硬件供应商（IHV）和独立软件供应商（ISV）使用。\]

 

LanguageNeutralIdentifier 元素是可选的。

 

 





