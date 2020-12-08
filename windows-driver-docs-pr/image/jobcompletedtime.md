---
title: JobCompletedTime 元素
description: 可选的 JobCompletedTime 元素指定扫描作业的完成时间。
keywords:
- JobCompletedTime 元素图像设备
topic_type:
- apiref
api_name:
- wscn JobCompletedTime
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 644653358505bfc3af7e2f61f5af4cb0895b758d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820257"
---
# <a name="jobcompletedtime-element"></a>JobCompletedTime 元素


可选的 **JobCompletedTime** 元素指定扫描作业的完成时间。

<a name="usage"></a>使用情况
-----

```xml
<wscn:JobCompletedTime>
  text
</wscn:JobCompletedTime>
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
<td><p><a href="jobendstate.md" data-raw-source="[&lt;strong&gt;JobEndState&lt;/strong&gt;](jobendstate.md)"><strong>JobEndState</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="jobstatus.md" data-raw-source="[&lt;strong&gt;JobStatus&lt;/strong&gt;](jobstatus.md)"><strong>JobStatus</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

所有处理都完成后，扫描作业就会 *完成* ，因为扫描和文档传输已成功完成或遇到致命错误。

指定的时间是指扫描设备的内部时钟，无需是实时时钟。

## <a name="see-also"></a>请参阅


[**JobEndState**](jobendstate.md)

[**JobStatus**](jobstatus.md)

 

 






