---
title: 文档名元素
description: 所需的文档名元素包含客户端提供的文档的名称。
ms.assetid: 7d6d7dcd-db5d-420d-9e5f-3badeb0a511c
keywords:
- 文档名元素成像设备
topic_type:
- apiref
api_name:
- wscn DocumentName
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e62b401098c43f8a516d950f3d020a50c1ca1a1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526773"
---
# <a name="documentname-element"></a>文档名元素


所需**文档名**元素包含客户端提供的文档的名称。

<a name="usage"></a>用法
-----

```xml
<wscn:DocumentName>
  text
</wscn:DocumentName>
```

<a name="attributes"></a>属性
----------

没有特性。

<a name="text-value"></a>文本值
----------

必需。 任何字符的字符串。

## <a name="child-elements"></a>子元素


没有子元素。

## <a name="parent-elements"></a>父元素


<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th>元素</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="documentdescription.md" data-raw-source="[&lt;strong&gt;DocumentDescription&lt;/strong&gt;](documentdescription.md)"><strong>DocumentDescription</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

WSD 扫描服务必须提供一个值，以将文档存储在客户端上。

## <a name="see-also"></a>另请参阅


[**DocumentDescription**](documentdescription.md)

 

 






