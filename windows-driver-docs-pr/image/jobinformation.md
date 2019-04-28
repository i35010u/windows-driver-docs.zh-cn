---
title: JobInformation 元素
description: 可选 JobInformation 元素描述作业的预期的用途。
ms.assetid: 0e5d41a0-49df-43db-a2e6-3639e60d2378
keywords:
- JobInformation 元素成像设备
topic_type:
- apiref
api_name:
- wscn JobInformation
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 698fd1680e7b21b69f4a952b6178565c1a837bf6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348810"
---
# <a name="jobinformation-element"></a>JobInformation 元素


可选**JobInformation**元素描述作业的预期的用途。

<a name="usage"></a>用法
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

必需。 任何有效字符的字符串。

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
<td><p><a href="jobdescription.md" data-raw-source="[&lt;strong&gt;JobDescription&lt;/strong&gt;](jobdescription.md)"><strong>JobDescription</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**JobInformation**值时，可以在客户端将重复使用用于创建作业的扫描票证。

## <a name="see-also"></a>请参阅


[**JobDescription**](jobdescription.md)

 

 






