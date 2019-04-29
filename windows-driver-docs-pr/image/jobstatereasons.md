---
title: JobStateReasons 元素
description: 所需的 JobStateReasons 元素包含有关作业处于其当前状态的所有其他信息。
ms.assetid: 52d6519e-2392-4fa4-bac0-f1bf60eccc99
keywords:
- JobStateReasons 元素成像设备
topic_type:
- apiref
api_name:
- wscn JobStateReasons
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b469b2b198fa6cc45a62f7a2a41f1072985a794
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363061"
---
# <a name="jobstatereasons-element"></a>JobStateReasons 元素


所需**JobStateReasons**元素包含有关作业处于其当前状态的所有其他信息。

<a name="usage"></a>用法
-----

```xml
<wscn:JobStateReasons>
  child elements
</wscn:JobStateReasons>
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
<td><p><a href="jobstatereason.md" data-raw-source="[&lt;strong&gt;JobStateReason&lt;/strong&gt;](jobstatereason.md)"><strong>JobStateReason</strong></a></p></td>
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
<td><p><a href="jobstatus.md" data-raw-source="[&lt;strong&gt;JobStatus&lt;/strong&gt;](jobstatus.md)"><strong>JobStatus</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="jobsummary.md" data-raw-source="[&lt;strong&gt;JobSummary&lt;/strong&gt;](jobsummary.md)"><strong>JobSummary</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**JobStateReasons**元素包含一系列[ **JobStateReason** ](jobstatereason.md)元素，其中每个指定作业处于其当前状态的一个原因。

## <a name="see-also"></a>请参阅


[**JobStateReason**](jobstatereason.md)

[**JobStatus**](jobstatus.md)

[**JobSummary**](jobsummary.md)

 

 






