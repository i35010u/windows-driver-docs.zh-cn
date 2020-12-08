---
title: 作业元素
description: 必需的作业元素包含与扫描作业关联的所有元素。
keywords:
- 作业元素图像处理设备
topic_type:
- apiref
api_name:
- wscn Job
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d694b04ac5217b515d4582ed12f70a9467baa058
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799549"
---
# <a name="job-element"></a>作业元素


必需的 **作业** 元素包含与扫描作业关联的所有元素。

<a name="usage"></a>使用情况
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

**作业** 元素表示的扫描作业 () 可以包含一个或多个文档。 作业和其文档的 WSD 扫描服务的处理指令在 **作业** 级别执行。

## <a name="see-also"></a>请参阅


[**ActiveJobs**](activejobs.md)

[**文档**](documents.md)

[**JobStatus**](jobstatus.md)

[**ScanTicket**](scanticket.md)

 

 






