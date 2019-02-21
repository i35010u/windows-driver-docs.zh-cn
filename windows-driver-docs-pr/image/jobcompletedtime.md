---
title: JobCompletedTime 元素
description: 可选 JobCompletedTime 元素指定在其中完成扫描作业的时间。
ms.assetid: f29449bd-c618-400f-b37c-3df7d955936b
keywords:
- JobCompletedTime 元素成像设备
topic_type:
- apiref
api_name:
- wscn JobCompletedTime
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9079cfc72c1736aaa82e0a8ccc5f390cc33f64e1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546185"
---
# <a name="jobcompletedtime-element"></a>JobCompletedTime 元素


可选**JobCompletedTime**元素指定在其中完成扫描作业的时间。

<a name="usage"></a>用法
-----

```xml
<wscn:JobCompletedTime>
  text
</wscn:JobCompletedTime>
```

<a name="attributes"></a>属性
----------

没有特性。

<a name="text-value"></a>文本值
----------

必需。 DateTime 类型的任何有效的值。 有关日期时间的详细信息，请参阅 XML 架构第 2 部分：数据类型第二版。**dateTimedateTime**

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
<td><p><a href="jobendstate.md" data-raw-source="[&lt;strong&gt;JobEndState&lt;/strong&gt;](jobendstate.md)"><strong>JobEndState</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="jobstatus.md" data-raw-source="[&lt;strong&gt;JobStatus&lt;/strong&gt;](jobstatus.md)"><strong>JobStatus</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

一个扫描作业*完整*时已完成所有处理，因为扫描和文档传输已成功都完成或遇到致命错误。

在指定的时间是指扫描设备的内部时钟，并不需要实时时钟。

## <a name="see-also"></a>另请参阅


[**JobEndState**](jobendstate.md)

[**JobStatus**](jobstatus.md)

 

 






