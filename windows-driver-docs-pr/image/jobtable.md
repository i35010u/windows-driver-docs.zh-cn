---
title: JobTable 元素
description: 必需的 JobTable 元素包含有关扫描作业的当前和历史信息。
keywords:
- JobTable 元素图像设备
topic_type:
- apiref
api_name:
- wscn JobTable
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd02f135befac9342bfbf6dfc4bfffadbc6de972
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824125"
---
# <a name="jobtable-element"></a>JobTable 元素


必需的 **JobTable** 元素包含有关扫描作业的当前和历史信息。

<a name="usage"></a>使用情况
-----

```xml
<wscn:JobTable>
  child elements
</wscn:JobTable>
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
<td><p><a href="activejobs.md" data-raw-source="[&lt;strong&gt;ActiveJobs&lt;/strong&gt;](activejobs.md)"><strong>ActiveJobs</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="jobhistory2.md" data-raw-source="[&lt;strong&gt;JobHistory&lt;/strong&gt;](jobhistory2.md)"><strong>JobHistory</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>父元素


没有父元素。

<a name="remarks"></a>备注
-------

WSD 扫描服务使用 **JobTable** 元素跟踪提交到 WSD 扫描服务的所有当前和已完成的扫描作业。 当前作业是在 [**ActiveJobs**](activejobs.md) 子元素中跟踪的;可以选择在 [**JobHistory**](jobhistory2.md) 子元素中跟踪已完成的作业。

## <a name="see-also"></a>请参阅


[**ActiveJobs**](activejobs.md)

[**JobHistory**](jobhistory2.md)

 

 






