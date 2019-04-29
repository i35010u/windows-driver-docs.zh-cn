---
title: ClearTime 元素
description: 所需的 ClearTime 元素指定一个条件已被清除的时间。
ms.assetid: 9b5fe054-f3fa-402a-8337-8fd181679080
keywords:
- ClearTime 元素成像设备
topic_type:
- apiref
api_name:
- wscn ClearTime
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e746ab7ee87f023eeb3ad4c3b42308c776cb8680
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373227"
---
# <a name="cleartime-element"></a>ClearTime 元素


所需**ClearTime**元素指定一个条件已被清除的时间。

<a name="usage"></a>用法
-----

```xml
<wscn:ClearTime>
  text
</wscn:ClearTime>
```

<a name="attributes"></a>特性
----------

没有特性。

<a name="text-value"></a>文本值
----------

必需。 DateTime 类型的任何有效的值。 有关日期时间的详细信息，请参阅 XML 架构第 2 部分：数据类型第二版。**dateTimedateTime**

## <a name="child-elements"></a>子元素


没有子元素。

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
<td><p><a href="conditionhistoryentry.md" data-raw-source="[&lt;strong&gt;ConditionHistoryEntry&lt;/strong&gt;](conditionhistoryentry.md)"><strong>ConditionHistoryEntry</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

在指定的时间取决于扫描程序的内部时钟。

## <a name="see-also"></a>请参阅


[**ConditionHistoryEntry**](conditionhistoryentry.md)

 

 






