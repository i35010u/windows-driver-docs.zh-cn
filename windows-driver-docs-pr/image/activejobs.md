---
title: ActiveJobs 元素
description: 必需的 ActiveJobs 元素包含当前活动扫描作业的列表。
keywords:
- ActiveJobs 元素图像设备
topic_type:
- apiref
api_name:
- wscn ActiveJobs
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16f5e0ab27951b9ea2b400da7e78fae5aa2ac208
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808287"
---
# <a name="activejobs-element"></a>ActiveJobs 元素


必需的 **ActiveJobs** 元素包含当前活动扫描作业的列表。

<a name="usage"></a>使用情况
-----

```xml
<wscn:ActiveJobs>
  child elements
</wscn:ActiveJobs>
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
<td><p><a href="job.md" data-raw-source="[&lt;strong&gt;Job&lt;/strong&gt;](job.md)"><strong>作业</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="jobsummary.md" data-raw-source="[&lt;strong&gt;JobSummary&lt;/strong&gt;](jobsummary.md)"><strong>JobSummary</strong></a></p></td>
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
<td><p><a href="getactivejobsresponse.md" data-raw-source="[&lt;strong&gt;GetActiveJobsResponse&lt;/strong&gt;](getactivejobsresponse.md)"><strong>GetActiveJobsResponse</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="jobtable.md" data-raw-source="[&lt;strong&gt;JobTable&lt;/strong&gt;](jobtable.md)"><strong>JobTable</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**ActiveJobs** 元素包含尚未完成处理的所有作业。 活动作业的状态可能为 "正在扫描"、"挂起" 或 "已停止"。 当前没有活动的作业时， **ActiveJobs** 为空。

客户端可以通过 [**GetActiveJobsRequest**](getactivejobsrequest.md) 操作请求活动作业的列表。 WSD 扫描服务返回 [**GetActiveJobsResponse**](getactivejobsresponse.md) 操作元素中的列表。

## <a name="see-also"></a>请参阅


[**GetActiveJobsRequest**](getactivejobsrequest.md)

[**GetActiveJobsResponse**](getactivejobsresponse.md)

[**作业**](job.md)

[**JobSummary**](jobsummary.md)

[**JobTable**](jobtable.md)

 

 






