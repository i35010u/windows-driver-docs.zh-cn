---
title: JobHistory 元素
description: 所需的 JobHistory 元素包含描述中扫描设备的最近已完成的作业的 JobSummary 元素的列表。
ms.assetid: d1439e56-b2fe-4db8-b063-56537a3346c6
keywords:
- JobHistory 元素成像设备
topic_type:
- apiref
api_name:
- wscn JobHistory
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95af97b65234292312176e43e56c3edcae44db36
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377609"
---
# <a name="jobhistory-element"></a>JobHistory 元素


所需**JobHistory**元素包含一系列[ **JobSummary** ](jobsummary.md)元素描述最近完成扫描设备中的作业。

<a name="usage"></a>用法
-----

```xml
<wscn:JobHistory>
  child elements
</wscn:JobHistory>
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
<td><p><a href="getjobhistoryresponse.md" data-raw-source="[&lt;strong&gt;GetJobHistoryResponse&lt;/strong&gt;](getjobhistoryresponse.md)"><strong>GetJobHistoryResponse</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**JobHistory**元素包含[ **JobSummary** ](jobsummary.md)扫描程序最近完成每个作业的元素。 **JobHistory**如果 WSD 扫描服务不已完成作业的任何记录，则为空。 扫描服务将返回此列表从[ **GetJobHistoryResponse**](getjobhistoryresponse.md)。

作业历史记录的 WSD 扫描服务存储，并返回量是特定于实现的。

## <a name="see-also"></a>请参阅


[**GetJobHistoryResponse**](getjobhistoryresponse.md)

[**JobSummary**](jobsummary.md)

 

 






