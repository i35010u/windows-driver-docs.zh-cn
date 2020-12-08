---
title: JobStateReasons 元素
description: 必需的 JobStateReasons 元素包含有关作业处于其当前状态的所有其他信息。
keywords:
- JobStateReasons 元素图像设备
topic_type:
- apiref
api_name:
- wscn JobStateReasons
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c6c8015bbdc7d7353f4c28a0dcdd757b0af587d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805585"
---
# <a name="jobstatereasons-element"></a>JobStateReasons 元素


必需的 **JobStateReasons** 元素包含有关作业处于其当前状态的所有其他信息。

<a name="usage"></a>使用情况
-----

```xml
<wscn:JobStateReasons>
  child elements
</wscn:JobStateReasons>
```

<a name="attributes"></a>特性
----------

没有特性。

## <a name="child-elements"></a>子元素


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
<td><p><a href="jobstatereason.md" data-raw-source="[&lt;strong&gt;JobStateReason&lt;/strong&gt;](jobstatereason.md)"><strong>JobStateReason</strong></a></p></td>
</tr>
</tbody>
</table>

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
<tr class="even">
<td><p><a href="jobsummary.md" data-raw-source="[&lt;strong&gt;JobSummary&lt;/strong&gt;](jobsummary.md)"><strong>JobSummary</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**JobStateReasons** 元素包含一个 [**JobStateReason**](jobstatereason.md)元素列表，其中每个元素都指定了一个作业处于其当前状态的原因。

## <a name="see-also"></a>请参阅


[**JobStateReason**](jobstatereason.md)

[**JobStatus**](jobstatus.md)

[**JobSummary**](jobsummary.md)

 

 






