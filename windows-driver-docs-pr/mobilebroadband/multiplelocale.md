---
title: MultipleLocale
description: MultipleLocale
ms.assetid: 95590875-2797-4a73-a211-6102305098f9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d21291b9e41d76e14ce03e5f5dd7e60096a57027
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566366"
---
# <a name="multiplelocale"></a>MultipleLocale

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

MultipleLocale 元素指定是否服务元数据包是否支持多个区域设置。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<MultipleLocale>
  text
</MultipleLocale>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


没有特性。

## <a name="span-idtextvaluespanspan-idtextvaluespanspan-idtextvaluespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>文本值


一个布尔值，如果服务元数据包支持多个区域设置为 true。

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
<td><p><a href="metadatakey.md" data-raw-source="[MetadataKey](metadatakey.md)">MetadataKey</a></p></td>
<td><p><a href="metadatakey.md" data-raw-source="[MetadataKey](metadatakey.md)">MetadataKey</a>元素指定设备元数据包的特性。 例如：</p>
<ul>
<li><p>每个设备支持的硬件函数的标识符。</p></li>
<li><p>特定于语言的区域设置的包中的文本字符串。</p></li>
</ul></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="MultipleLocale" type ="xs:boolean" />
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


-   若要在服务元数据包中支持多个区域设置，请将 MultipleLocale 元素设置为 **，则返回 true**。 在 Windows 7 上不支持此元素。 如果未指定此元素，则默认值为 true。

-   如果没有单一区域设置服务元数据包和用户的计算机上多个区域设置服务元数据包，Windows 将使用多个区域设置服务元数据包，如果所有其他排名值是相同的。

 

 





