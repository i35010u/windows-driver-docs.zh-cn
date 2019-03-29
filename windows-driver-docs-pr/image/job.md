---
title: 作业元素
description: 所需的作业元素包含与扫描作业相关联的所有元素。
ms.assetid: c5622ea6-c57a-4c80-a6ef-e6b9014b2b59
keywords:
- 作业元素成像设备
topic_type:
- apiref
api_name:
- wscn Job
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1608d20448afa736b8c0f69f965776e423810ab
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576465"
---
# <a name="job-element"></a>作业元素


所需**作业**元素包含与扫描作业相关联的所有元素。

<a name="usage"></a>用法
-----

```xml
<wscn:Job>
  child elements
</wscn:Job>
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
<td><p><a href="documents.md" data-raw-source="[&lt;strong&gt;Documents&lt;/strong&gt;](documents.md)"><strong>文档</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="jobstatus.md" data-raw-source="[&lt;strong&gt;JobStatus&lt;/strong&gt;](jobstatus.md)"><strong>JobStatus</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="scanticket.md" data-raw-source="[&lt;strong&gt;ScanTicket&lt;/strong&gt;](scanticket.md)"><strong>ScanTicket</strong></a></p></td>
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
</tbody>
</table>

<a name="remarks"></a>备注
-------

扫描作业 (其**作业**元素表示) 可以包含一个或多个文档。 WSD 扫描服务的处理指令，两个作业，其文档在执行**作业**级别。

## <a name="see-also"></a>请参阅


[**ActiveJobs**](activejobs.md)

[**文档**](documents.md)

[**JobStatus**](jobstatus.md)

[**ScanTicket**](scanticket.md)

 

 






