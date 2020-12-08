---
title: 时间元素
description: 所需时间元素指定条件发生的时间。
keywords:
- 时间元素图像处理设备
topic_type:
- apiref
api_name:
- wscn Time
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e233c8f459ad7e362189c72c8d165211f02fab9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789855"
---
# <a name="time-element"></a>时间元素


所需 **时间** 元素指定条件发生的时间。

<a name="usage"></a>使用情况
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

必需。 DateTime 类型的任何有效值。 有关日期时间的详细信息，请参阅 XML 架构第2部分：数据类型第二版。**dateTimedateTime**

## <a name="child-elements"></a>子元素


没有任何子元素。

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

指定的 **时间** 取决于扫描仪的内部时钟。

## <a name="see-also"></a>请参阅


[**ConditionHistoryEntry**](conditionhistoryentry.md)

[**DeviceCondition**](devicecondition.md)

 

 






