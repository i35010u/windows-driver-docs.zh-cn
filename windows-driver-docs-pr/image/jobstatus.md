---
title: JobStatus 元素
description: 所需的 JobStatus 元素包含有关状态的当前扫描作业的所有信息。
ms.assetid: e3eb2cc7-70a4-4ae0-8569-4a91f2b42228
keywords:
- JobStatus 元素成像设备
topic_type:
- apiref
api_name:
- wscn JobStatus
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f35d316dce2ee7103f6cb74432ce6acaa772c6b1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519114"
---
# <a name="jobstatus-element"></a>JobStatus 元素


所需**JobStatus**元素包含有关状态的当前扫描作业的所有信息。

<a name="usage"></a>用法
-----

```xml
<wscn:JobStatus>
  child elements
</wscn:JobStatus>
```

<a name="attributes"></a>属性
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
<td><p><a href="job.md" data-raw-source="[&lt;strong&gt;Job&lt;/strong&gt;](job.md)"><strong>Job</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**JobStatus**通过自动机时进行维护，子元素。 WSD 扫描服务应更新**JobStatus**元素，相应地处理作业。 客户端操作，如[ **CancelJobRequest**](canceljobrequest.md)，可以间接影响作业状态。

WSD 扫描服务通知客户端有关通过作业的状态将变为[ **JobStatusEvent** ](jobstatusevent.md)事件元素。 WSD 扫描服务应生成**JobStatusEvent**为每个更改对所有元素**JobStatus**子元素。

客户端可以查询通过作业状态[ **GetJobElementsRequest** ](getjobelementsrequest.md)操作。

## <a name="see-also"></a>另请参阅


[**CancelJobRequest**](canceljobrequest.md)

[**GetJobElementsRequest**](getjobelementsrequest.md)

[**Job**](job.md)

[**JobCompletedTime**](jobcompletedtime.md)

[**JobCreatedTime**](jobcreatedtime.md)

[**JobId**](jobid.md)

[**JobState**](jobstate.md)

[**JobStateReasons**](jobstatereasons.md)

[**JobStatusEvent**](jobstatusevent.md)

[**ScansCompleted**](scanscompleted.md)

 

 






