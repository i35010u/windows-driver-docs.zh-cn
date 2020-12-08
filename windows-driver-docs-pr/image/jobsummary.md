---
title: JobSummary 元素
description: 可选的 JobSummary 元素包含有关扫描作业的摘要。
keywords:
- JobSummary 元素图像设备
topic_type:
- apiref
api_name:
- wscn JobSummary
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8fb878c8789b1cb0f4a4216fd1469395ad290c60
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824129"
---
# <a name="jobsummary-element"></a>JobSummary 元素


可选的 **JobSummary** 元素包含有关扫描作业的摘要。

<a name="usage"></a>使用情况
-----

```xml
<wscn:JobSummary>
  child elements
</wscn:JobSummary>
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
<td><p><a href="jobid.md" data-raw-source="[&lt;strong&gt;JobId&lt;/strong&gt;](jobid.md)"><strong>JobId</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="jobname.md" data-raw-source="[&lt;strong&gt;JobName&lt;/strong&gt;](jobname.md)"><strong>JobName</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="joboriginatingusername.md" data-raw-source="[&lt;strong&gt;JobOriginatingUserName&lt;/strong&gt;](joboriginatingusername.md)"><strong>JobOriginatingUserName</strong></a></p></td>
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
<td><p><a href="activejobs.md" data-raw-source="[&lt;strong&gt;ActiveJobs&lt;/strong&gt;](activejobs.md)"><strong>ActiveJobs</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="jobhistory.md" data-raw-source="[&lt;strong&gt;JobHistory&lt;/strong&gt;](jobhistory.md)"><strong>JobHistory</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

如果 **JobSummary** 元素的父元素是 [**ActiveJobs**](activejobs.md)，则 **JobSummary** 将包含扫描设备中当前活动的一个作业的相关信息摘要。

如果父元素为 [**JobHistory**](jobhistory.md)，则 **JobSummary** 包含有关扫描设备中单个最近完成的作业的信息摘要。

## <a name="see-also"></a>请参阅


[**ActiveJobs**](activejobs.md)

[**JobHistory**](jobhistory.md)

[**JobId**](jobid.md)

[**JobName**](jobname.md)

[**JobOriginatingUserName**](joboriginatingusername.md)

[**JobState**](jobstate.md)

[**JobStateReasons**](jobstatereasons.md)

[**ScansCompleted**](scanscompleted.md)

 

 






