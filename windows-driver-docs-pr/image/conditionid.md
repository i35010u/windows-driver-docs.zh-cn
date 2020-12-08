---
title: ConditionId 元素
description: 所需的 ConditionId 元素唯一标识刚刚清除的设备条件。
keywords:
- ConditionId 元素图像设备
topic_type:
- apiref
api_name:
- wscn ConditionId
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9b26358325614705446849f2e47533e5b63efb1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833513"
---
# <a name="conditionid-element"></a>ConditionId 元素


所需的 **ConditionId** 元素唯一标识刚刚清除的设备条件。

<a name="usage"></a>使用情况
-----

```xml
<wscn:ConditionId>
  text
</wscn:ConditionId>
```

<a name="attributes"></a>特性
----------

没有特性。

<a name="text-value"></a>文本值
----------

必需。 一个整数值，它等效于先前报告的 DeviceCondition 元素的 Id 属性。

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
<td><p><a href="deviceconditioncleared.md" data-raw-source="[&lt;strong&gt;DeviceConditionCleared&lt;/strong&gt;](deviceconditioncleared.md)"><strong>DeviceConditionCleared</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**ConditionId** 元素必须是 WSD 扫描服务先前通过 [**ScannerStatusConditionEvent**](scannerstatusconditionevent.md)报告的 **DeviceCondition** 元素的 **Id** 属性。

## <a name="see-also"></a>请参阅


[**DeviceCondition**](devicecondition.md)

[**DeviceConditionCleared**](deviceconditioncleared.md)

[**ScannerStatusConditionEvent**](scannerstatusconditionevent.md)

 

 






