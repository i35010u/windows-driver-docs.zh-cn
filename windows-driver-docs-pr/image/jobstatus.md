---
title: JobStatus 元素
description: 必需的 JobStatus 元素包含当前扫描作业状态的所有相关信息。
keywords:
- JobStatus 元素图像设备
topic_type:
- apiref
api_name:
- wscn JobStatus
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 261f472f23a2a10aa81dd45b115ac9ab095d65a6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805560"
---
# <a name="jobstatus-element"></a>JobStatus 元素


必需的 **JobStatus** 元素包含当前扫描作业状态的所有相关信息。

<a name="usage"></a>使用情况
-----

```xml
<wscn:JobStatus>
  child elements
</wscn:JobStatus>
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
<td><p><a href="jobcompletedtime.md" data-raw-source="[&lt;strong&gt;JobCompletedTime&lt;/strong&gt;](jobcompletedtime.md)"><strong>JobCompletedTime</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="jobcreatedtime.md" data-raw-source="[&lt;strong&gt;JobCreatedTime&lt;/strong&gt;](jobcreatedtime.md)"><strong>JobCreatedTime</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="jobid.md" data-raw-source="[&lt;strong&gt;JobId&lt;/strong&gt;](jobid.md)"><strong>JobId</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="jobstate.md" data-raw-source="[&lt;strong&gt;JobState&lt;/strong&gt;](jobstate.md)"><strong>JobState</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="jobstatereasons.md" data-raw-source="[&lt;strong&gt;JobStateReasons&lt;/strong&gt;](jobstatereasons.md)"><strong>JobStateReasons</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="scanscompleted.md" data-raw-source="[&lt;strong&gt;ScansCompleted&lt;/strong&gt;](scanscompleted.md)"><strong>ScansCompleted</strong></a></p></td>
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
<td><p><a href="job.md" data-raw-source="[&lt;strong&gt;Job&lt;/strong&gt;](job.md)"><strong>作业</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**JobStatus** 子元素通过自动机时出错维护。 WSD 扫描服务应在处理作业时相应地更新 **JobStatus** 元素。 诸如 [**CancelJobRequest**](canceljobrequest.md)之类的客户端操作可以间接影响作业状态。

WSD 扫描服务通过 [**JobStatusEvent**](jobstatusevent.md) 事件元素向客户端通知作业状态的更改。 对于所有 **JobStatus** 子元素的每个更改，WSD 扫描服务应生成一个 **JobStatusEvent** 元素。

客户端可以通过 [**GetJobElementsRequest**](getjobelementsrequest.md) 操作查询作业状态。

## <a name="see-also"></a>请参阅


[**CancelJobRequest**](canceljobrequest.md)

[**GetJobElementsRequest**](getjobelementsrequest.md)

[**作业**](job.md)

[**JobCompletedTime**](jobcompletedtime.md)

[**JobCreatedTime**](jobcreatedtime.md)

[**JobId**](jobid.md)

[**JobState**](jobstate.md)

[**JobStateReasons**](jobstatereasons.md)

[**JobStatusEvent**](jobstatusevent.md)

[**ScansCompleted**](scanscompleted.md)

 

 






