---
title: ScansCompleted 元素
description: 所需的 ScansCompleted 元素指定扫描的映像的数量。
ms.assetid: 71634b6b-1c61-46a0-8cde-01a975c09270
keywords:
- ScansCompleted 元素成像设备
topic_type:
- apiref
api_name:
- wscn ScansCompleted
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81013fd6a543b9bfbccb98665afadb346d9cdb18
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356227"
---
# <a name="scanscompleted-element"></a>ScansCompleted 元素


所需**ScansCompleted**元素指定的扫描的映像数量。

<a name="usage"></a>用法
-----

```xml
<wscn:ScansCompleted>
  text
</wscn:ScansCompleted>
```

<a name="attributes"></a>特性
----------

没有特性。

<a name="text-value"></a>文本值
----------

必需。 介于 1 到 2147483648 的整数值。

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
<tr class="odd">
<td><p><a href="jobsummary.md" data-raw-source="[&lt;strong&gt;JobSummary&lt;/strong&gt;](jobsummary.md)"><strong>JobSummary</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

WSD 扫描服务多个时间扫描一张纸的媒体时，必须递增**ScansCompleted**每次进行计数。 在双工模式下，生成两个扫描中的扫描媒体表的每一侧**ScansCompleted**计数。

**ScansCompleted**可能不知道计数，直到扫描程序已完成处理该作业。 WSD 扫描服务必须更新**ScansCompleted**元素时更多具体信息不可用。

## <a name="see-also"></a>请参阅


[**JobEndState**](jobendstate.md)

[**JobStatus**](jobstatus.md)

[**JobSummary**](jobsummary.md)

 

 






