---
title: LanguageNeutralIdentifier
description: LanguageNeutralIdentifier
ms.assetid: 38713565-464c-4b12-9076-331ae43e01e8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce4ea9d3ace366695c79f423281f3c98bc7ab7ba
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525097"
---
# <a name="languageneutralidentifier"></a>LanguageNeutralIdentifier

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

LanguageNeutralIdentifier 元素指定一个 GUID，它标识独立于其区域设置的服务元数据包。 LanguageNeutralIdentifier 元素可用于相同的 GUID 用于标识的服务元数据包的同一服务的一个或多个本地化的版本。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<LanguageNeutralIdentifier>
  text
</LanguageNeutralIdentifier>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


没有特性。

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
<td><p><a href="relationships.md" data-raw-source="[Relationships](relationships.md)">关系</a></p></td>
<td><p><a href="relationships.md" data-raw-source="[Relationships](relationships.md)">关系</a>元素指定用于跟踪设备元数据包设备元数据缓存中的数据。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="LanguageNeutralIdentifier" type="tns:GUIDType" minOccurs="0" />
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


LanguageNeutralIdentifier 元素允许相同的 GUID，若要在一个或多个本地化版本的设备元数据包中使用的同一个设备。

例如，如果在发布三个区域设置的设备 (如 EN-US、 JA-JP、 和 AR-SA)，可以创建单独的元数据适用于每个区域设置的设备的包。 通过使用这些包中的 LanguageNeutralIdentifier 元素共同的 GUID，您可以轻松地搜索设备元数据包通过浏览其 PackageInfo XML 文档。

**重要**   LanguageNeutralIdentifier 元素未由操作系统的任何组件。 它保留供 OEM、 独立硬件供应商 (IHV) 和独立软件供应商 (ISV)。\]

 

LanguageNeutralIdentifier 元素是可选的。

 

 





