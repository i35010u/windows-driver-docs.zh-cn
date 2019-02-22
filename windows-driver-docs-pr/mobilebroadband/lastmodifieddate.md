---
title: LastModifiedDate
description: LastModifiedDate
ms.assetid: e0ef7ca0-0c3d-4e71-af2e-ead90013e561
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f688bf5d02d98787157e897488532211244c7f7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541220"
---
# <a name="lastmodifieddate"></a>LastModifiedDate

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

LastModifiedDate 元素指定服务元数据包的上次更改的时间戳。 根据此信息，操作系统将选择并加载最新的服务元数据包版本。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<LastModifiedDate>
  text
</LastModifiedDate>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


没有特性。

## <a name="span-idtextvaluespanspan-idtextvaluespanspan-idtextvaluespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>文本值


以协调世界时 (UTC) 格式表示的时间戳值。

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
<xs:element name="LastModifiedDate" type="xs:dateTime" />
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


-   LastModifiedDate 元素的值必须表示上次更改的元数据包的实际时间。

-   每次提交服务元数据包通过 Windows 元数据和 Internet 服务 (WMIS) 分发 Windows 硬件开发人员中心仪表板后验证包更新 LastModifiedDate 元素。

LastModifiedDate 元素是必需的。

 

 





