---
title: Time 元素
description: 所需的时间元素指定一个条件发生的时间。
ms.assetid: 1a10f6b4-1fcd-4697-9eb4-d58cca9c4a23
keywords:
- Time 元素成像设备
topic_type:
- apiref
api_name:
- wscn Time
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: faa632366a8f5496e896493d6866f450dd93fa94
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325395"
---
# <a name="time-element"></a>Time 元素


所需**时间**元素指定一个条件发生的时间。

<a name="usage"></a>用法
-----

```xml
<wscn:Time>
  text
</wscn:Time>
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
<tr class="even">
<td><p><a href="devicecondition.md" data-raw-source="[&lt;strong&gt;DeviceCondition&lt;/strong&gt;](devicecondition.md)"><strong>DeviceCondition</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

指定**时间**取决于扫描程序的内部时钟。

## <a name="see-also"></a>请参阅


[**ConditionHistoryEntry**](conditionhistoryentry.md)

[**DeviceCondition**](devicecondition.md)

 

 






