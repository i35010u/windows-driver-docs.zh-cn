---
title: JobState 元素
description: 必需的 JobState 元素指定作业的当前状态。
keywords:
- JobState 元素图像设备
topic_type:
- apiref
api_name:
- wscn JobState
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91b2d3da28e50eb22341430b94055e0d529f1c7d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789857"
---
# <a name="jobstate-element"></a>JobState 元素


必需的 **JobState** 元素指定作业的当前状态。

<a name="usage"></a>使用情况
-----

```xml
<wscn:JobState>
  text
</wscn:JobState>
```

<a name="attributes"></a>特性
----------

没有特性。

<a name="text-value"></a>文本值
----------

必需。 以下值之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>术语</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><span id="Aborted"></span><span id="aborted"></span><span id="ABORTED"></span>被</p></td>
<td><p>系统中止了该作业。</p></td>
</tr>
<tr class="even">
<td><p><span id="Canceled"></span><span id="canceled"></span><span id="CANCELED"></span>放弃</p></td>
<td><p>作业已被使用 CancelJobRequest 操作的客户端取消，或在 WSD 扫描服务的范围之外。</p></td>
</tr>
<tr class="odd">
<td><p><span id="Completed"></span><span id="completed"></span><span id="COMPLETED"></span>完成</p></td>
<td><p>作业已完成处理，所有图像数据都已发送到客户端。</p></td>
</tr>
<tr class="even">
<td><p><span id="Creating"></span><span id="creating"></span><span id="CREATING"></span>制定</p></td>
<td><p>正在初始化作业。</p></td>
</tr>
<tr class="odd">
<td><p><span id="Held"></span><span id="held"></span><span id="HELD"></span>暂停</p></td>
<td><p>作业正在等待处理，但不适用于计划。 作业只能通过 WSD 扫描服务范围以外的方法达到此状态。</p></td>
</tr>
<tr class="even">
<td><p><span id="Pending"></span><span id="pending"></span><span id="PENDING"></span>未</p></td>
<td><p>该作业已初始化并等待处理。</p></td>
</tr>
<tr class="odd">
<td><p><span id="Processing"></span><span id="processing"></span><span id="PROCESSING"></span>字处理</p></td>
<td><p>正在对作业数据进行数字化、转换或传输。</p></td>
</tr>
<tr class="even">
<td><p><span id="Started"></span><span id="started"></span><span id="STARTED"></span>首先</p></td>
<td><p>扫描设备已开始处理作业。 此状态为暂时性状态，通常只会在 JobStatusEvent 事件中出现。</p></td>
</tr>
<tr class="odd">
<td><p><span id="Terminating"></span><span id="terminating"></span><span id="TERMINATING"></span>因</p></td>
<td><p>作业已被客户端启动的 CancelJobRequest 操作取消，或在 WSD 扫描服务范围以外的时间中止。</p></td>
</tr>
</tbody>
</table>

 

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
<tr class="even">
<td><p><a href="jobsummary.md" data-raw-source="[&lt;strong&gt;JobSummary&lt;/strong&gt;](jobsummary.md)"><strong>JobSummary</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

当 **JobState** 元素包含在 [**JobEndStateEvent**](jobendstateevent.md) 事件或 [**JobHistory**](jobhistory2.md) 元素中时， **JobState** 表示作业的已完成状态。 否则， **JobState** 指定作业的当前状态。

可以扩展和子集化此元素的允许值。

## <a name="see-also"></a>请参阅


[**CancelJobRequest**](canceljobrequest.md)

[**JobEndStateEvent**](jobendstateevent.md)

[**JobHistory**](jobhistory2.md)

[**JobStatus**](jobstatus.md)

[**JobStatusEvent**](jobstatusevent.md)

[**JobSummary**](jobsummary.md)

 

 






