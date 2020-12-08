---
title: ClearTime 元素
description: 必需的 ClearTime 元素指定清除条件的时间。
keywords:
- ClearTime 元素图像设备
topic_type:
- apiref
api_name:
- wscn ClearTime
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 013fc47d2c3134a769a9cd7b60cc741bfe2d533e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838905"
---
# <a name="cleartime-element"></a>ClearTime 元素


必需的 **ClearTime** 元素指定清除条件的时间。

<a name="usage"></a>使用情况
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
</tbody>
</table>

<a name="remarks"></a>备注
-------

指定的时间取决于扫描仪的内部时钟。

## <a name="see-also"></a>请参阅


[**ConditionHistoryEntry**](conditionhistoryentry.md)

 

 






