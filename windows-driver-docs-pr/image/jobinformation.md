---
title: JobInformation 元素
description: 可选的 JobInformation 元素描述作业的预期用途。
keywords:
- JobInformation 元素图像设备
topic_type:
- apiref
api_name:
- wscn JobInformation
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6530b26b82e75d467f28dad8bad588ab813339c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789873"
---
# <a name="jobinformation-element"></a>JobInformation 元素


可选的 **JobInformation** 元素描述作业的预期用途。

<a name="usage"></a>使用情况
-----

```xml
<wscn:JobInformation>
  text
</wscn:JobInformation>
```

<a name="attributes"></a>特性
----------

没有特性。

<a name="text-value"></a>文本值
----------

必需。 任何有效的字符串。

## <a name="child-elements"></a>子元素


没有任何子元素。

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
<td><p><a href="jobdescription.md" data-raw-source="[&lt;strong&gt;JobDescription&lt;/strong&gt;](jobdescription.md)"><strong>JobDescription</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

当客户端将重新使用用于创建作业的扫描票证时， **JobInformation** 值非常有用。

## <a name="see-also"></a>请参阅


[**JobDescription**](jobdescription.md)

 

 






