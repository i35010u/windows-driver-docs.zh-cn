---
title: JobCreatedTime 元素
description: 可选的 JobCreatedTime 元素指定创建作业的时间。
keywords:
- JobCreatedTime 元素图像设备
topic_type:
- apiref
api_name:
- wscn JobCreatedTime
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7002b10bc3f51226c0eb0afd02ea918628f2cc8f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840091"
---
# <a name="jobcreatedtime-element"></a>JobCreatedTime 元素


可选的 **JobCreatedTime** 元素指定创建作业的时间。

<a name="usage"></a>使用情况
-----

```xml
<wscn:JobCreatedTime>
  text
</wscn:JobCreatedTime>
```

<a name="attributes"></a>特性
----------

没有特性。

<a name="text-value"></a>文本值
----------

必需。 DateTime 类型的任何有效值。 有关日期时间的详细信息，请参阅 XML 架构第2部分：数据类型第二版。**dateTimedateTime**

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
<td><p><a href="jobstatus.md" data-raw-source="[&lt;strong&gt;JobStatus&lt;/strong&gt;](jobstatus.md)"><strong>JobStatus</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

作业提交到系统时，会 *创建* 一个作业。

指定的时间是指扫描设备的内部时钟，无需是实时时钟。

## <a name="see-also"></a>请参阅


[**JobStatus**](jobstatus.md)

 

 






