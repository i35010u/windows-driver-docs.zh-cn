---
title: ActiveJobs 元素
description: 所需的 ActiveJobs 元素包含所有当前处于活动状态的扫描作业的列表。
ms.assetid: 90acd196-60d3-43e5-9346-a8514bcf0bb8
keywords:
- ActiveJobs 元素成像设备
topic_type:
- apiref
api_name:
- wscn ActiveJobs
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 699d78e8a7223a1bb6c1d3bd5c52b3045430ccbc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367101"
---
# <a name="activejobs-element"></a>ActiveJobs 元素


所需**ActiveJobs**元素包含所有当前处于活动状态的扫描作业的列表。

<a name="usage"></a>用法
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
<td><p><a href="job.md" data-raw-source="[&lt;strong&gt;Job&lt;/strong&gt;](job.md)"><strong>Job</strong></a></p></td>
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

**ActiveJobs**元素包含尚未完成处理的所有作业。 无法扫描活动作业的状态、 挂起，或已停止。 **ActiveJobs**时没有当前处于活动状态的作业，为空。

客户端可以询问有关的活动作业通过列表[ **GetActiveJobsRequest** ](getactivejobsrequest.md)操作。 WSD 扫描服务返回的列表中[ **GetActiveJobsResponse** ](getactivejobsresponse.md)操作元素。

## <a name="see-also"></a>请参阅


[**GetActiveJobsRequest**](getactivejobsrequest.md)

[**GetActiveJobsResponse**](getactivejobsresponse.md)

[**Job**](job.md)

[**JobSummary**](jobsummary.md)

[**JobTable**](jobtable.md)

 

 






