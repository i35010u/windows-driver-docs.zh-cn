---
title: JobState 元素
description: 所需的 JobState 元素指定作业的当前状态。
ms.assetid: 7198feea-ce6c-4827-a3b4-c248c6f62e37
keywords:
- JobState 元素成像设备
topic_type:
- apiref
api_name:
- wscn JobState
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e3b0ffa831de96553bfd3067c1edb65a71f5b1f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524277"
---
# <a name="jobstate-element"></a>JobState 元素


所需**JobState**元素指定作业的当前状态。

<a name="usage"></a>用法
-----

```xml
<wscn:JobState>
  text
</wscn:JobState>
```

<a name="attributes"></a>属性
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
<td><p><span id="Aborted"></span><span id="aborted"></span><span id="ABORTED"></span>已中止</p></td>
<td><p>系统中止作业。</p></td>
</tr>
<tr class="even">
<td><p><span id="Canceled"></span><span id="canceled"></span><span id="CANCELED"></span>已取消</p></td>
<td><p>通过使用 CancelJobRequest 操作的客户端或 WSD 扫描服务的作用域之外的方式，该作业已取消。</p></td>
</tr>
<tr class="odd">
<td><p><span id="Completed"></span><span id="completed"></span><span id="COMPLETED"></span>已完成</p></td>
<td><p>作业是映像的已完成的处理及其所有数据已发送到客户端。</p></td>
</tr>
<tr class="even">
<td><p><span id="Creating"></span><span id="creating"></span><span id="CREATING"></span>创建</p></td>
<td><p>正在初始化作业。</p></td>
</tr>
<tr class="odd">
<td><p><span id="Held"></span><span id="held"></span><span id="HELD"></span>保存</p></td>
<td><p>作业正在等待处理，但无法对计划。 仅通过 WSD 扫描服务的作用域之外的方法，该作业可以达到此状态。</p></td>
</tr>
<tr class="even">
<td><p><span id="Pending"></span><span id="pending"></span><span id="PENDING"></span>挂起</p></td>
<td><p>作业已初始化，并且正在等待处理。</p></td>
</tr>
<tr class="odd">
<td><p><span id="Processing"></span><span id="processing"></span><span id="PROCESSING"></span>处理</p></td>
<td><p>该作业的数据是被数字化，转换后，或传输。</p></td>
</tr>
<tr class="even">
<td><p><span id="Started"></span><span id="started"></span><span id="STARTED"></span>已启动</p></td>
<td><p>扫描设备已开始处理该作业。 此状态是一个暂时性状态，并通常会看到仅与 JobStatusEvent 事件。</p></td>
</tr>
<tr class="odd">
<td><p><span id="Terminating"></span><span id="terminating"></span><span id="TERMINATING"></span>终止</p></td>
<td><p>作业是由任一客户端启动 CancelJobRequest 操作已取消或中止的 WSD 扫描服务的作用域之外的方法。</p></td>
</tr>
</tbody>
</table>

 

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
<tr class="even">
<td><p><a href="jobsummary.md" data-raw-source="[&lt;strong&gt;JobSummary&lt;/strong&gt;](jobsummary.md)"><strong>JobSummary</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

当**JobState**元素包含在[ **JobEndStateEvent** ](jobendstateevent.md)事件或[ **JobHistory** ](jobhistory2.md)元素， **JobState**表示已完成的作业的状态。 否则为**JobState**指定作业的当前状态。

您都可以扩展和子集的允许的值为此元素。

## <a name="see-also"></a>另请参阅


[**CancelJobRequest**](canceljobrequest.md)

[**JobEndStateEvent**](jobendstateevent.md)

[**JobHistory**](jobhistory2.md)

[**JobStatus**](jobstatus.md)

[**JobStatusEvent**](jobstatusevent.md)

[**JobSummary**](jobsummary.md)

 

 






