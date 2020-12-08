---
title: ScansCompleted 元素
description: 必需的 ScansCompleted 元素指定要扫描的映像数。
keywords:
- ScansCompleted 元素图像设备
topic_type:
- apiref
api_name:
- wscn ScansCompleted
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49c449708517261215558d58a1123fc473949955
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785175"
---
# <a name="scanscompleted-element"></a>ScansCompleted 元素


必需的 **ScansCompleted** 元素指定要扫描的映像数。

<a name="usage"></a>使用情况
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

必需。 1到2147483648之间的一个整数值。

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
<tr class="odd">
<td><p><a href="jobsummary.md" data-raw-source="[&lt;strong&gt;JobSummary&lt;/strong&gt;](jobsummary.md)"><strong>JobSummary</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

如果多次扫描媒体工作表，则 WSD 扫描服务每次都必须递增 **ScansCompleted** 计数。 媒体工作表的每一侧都在双工模式下扫描，并在 **ScansCompleted** 计数中生成两次扫描。

在扫描程序完成作业处理之前， **ScansCompleted** 计数可能未知。 当更准确的信息可用时，WSD 扫描服务必须更新 **ScansCompleted** 元素。

## <a name="see-also"></a>请参阅


[**JobEndState**](jobendstate.md)

[**JobStatus**](jobstatus.md)

[**JobSummary**](jobsummary.md)

 

 






