---
title: JobCreatedTime 元素
description: 可选 JobCreatedTime 元素指定在其中创建作业的时间。
ms.assetid: 34107c3a-d02a-4b86-be1e-cd91e2887479
keywords:
- JobCreatedTime 元素成像设备
topic_type:
- apiref
api_name:
- wscn JobCreatedTime
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 230892171a1f54640a0a0994bb45ab27b449795d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521801"
---
# <a name="jobcreatedtime-element"></a>JobCreatedTime 元素


可选**JobCreatedTime**元素指定在其中创建作业的时间。

<a name="usage"></a>用法
-----

```xml
<wscn:JobCreatedTime>
  text
</wscn:JobCreatedTime>
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
<td><p><a href="jobstatus.md" data-raw-source="[&lt;strong&gt;JobStatus&lt;/strong&gt;](jobstatus.md)"><strong>JobStatus</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

作业是*创建*时将作业提交到系统。

在指定的时间是指扫描设备的内部时钟，并不需要实时时钟。

## <a name="see-also"></a>另请参阅


[**JobStatus**](jobstatus.md)

 

 






