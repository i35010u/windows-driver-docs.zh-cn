---
title: JobTable 元素
description: 所需的 JobTable 元素包含有关扫描作业的当前和历史信息。
ms.assetid: 349ca443-5296-4200-884d-91fcdb222be4
keywords:
- JobTable 元素成像设备
topic_type:
- apiref
api_name:
- wscn JobTable
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0464a2aab8fed830f5fb0fc65efc987274b729bf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534855"
---
# <a name="jobtable-element"></a>JobTable 元素


所需**JobTable**元素包含有关扫描作业的当前和历史信息。

<a name="usage"></a>用法
-----

```xml
<wscn:JobTable>
  child elements
</wscn:JobTable>
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

WSD 扫描服务使用**JobTable**元素来跟踪所有当前和已完成扫描作业提交到 WSD 扫描服务。 在中跟踪当前作业[ **ActiveJobs** ](activejobs.md)子元素，则可以选择跟踪中的已完成的作业[ **JobHistory** ](jobhistory2.md)子元素。

## <a name="see-also"></a>另请参阅


[**ActiveJobs**](activejobs.md)

[**JobHistory**](jobhistory2.md)

 

 






