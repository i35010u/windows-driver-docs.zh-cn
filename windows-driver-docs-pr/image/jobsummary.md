---
title: JobSummary 元素
description: 可选 JobSummary 元素包含有关扫描作业的摘要。
ms.assetid: db81cad5-d157-403c-b3a4-1e5f91f858da
keywords:
- JobSummary 元素成像设备
topic_type:
- apiref
api_name:
- wscn JobSummary
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b3fcd642a6fc31146f9f0d7abb4b5c2cbf1ce60a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520872"
---
# <a name="jobsummary-element"></a>JobSummary 元素


可选**JobSummary**元素包含有关扫描作业的摘要。

<a name="usage"></a>用法
-----

```xml
<wscn:JobSummary>
  child elements
</wscn:JobSummary>
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

如果父元素的**JobSummary**元素是[ **ActiveJobs**](activejobs.md)， **JobSummary**包含一个作业的相关信息的摘要这是在扫描设备中当前处于活动状态。

如果父元素是[ **JobHistory**](jobhistory.md)， **JobSummary**包含有关单一、 最近已完成作业内扫描设备的信息的摘要。

## <a name="see-also"></a>另请参阅


[**ActiveJobs**](activejobs.md)

[**JobHistory**](jobhistory.md)

[**JobId**](jobid.md)

[**JobName**](jobname.md)

[**JobOriginatingUserName**](joboriginatingusername.md)

[**JobState**](jobstate.md)

[**JobStateReasons**](jobstatereasons.md)

[**ScansCompleted**](scanscompleted.md)

 

 






