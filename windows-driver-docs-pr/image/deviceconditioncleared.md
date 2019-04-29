---
title: DeviceConditionCleared 元素
description: 所需的 DeviceConditionCleared 元素包含有关已清除先前报告 DeviceCondition 条件的信息。
ms.assetid: f4ed3d25-cee0-4532-84aa-d1cdd144ce2a
keywords:
- DeviceConditionCleared 元素成像设备
topic_type:
- apiref
api_name:
- wscn DeviceConditionCleared
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2aab29ddeb8ee49430928f2b4f81dbc8a7c12fa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364555"
---
# <a name="deviceconditioncleared-element"></a>DeviceConditionCleared 元素


所需**DeviceConditionCleared**元素包含有关上次报告的信息[ **DeviceCondition** ](devicecondition.md)已清除的条件。

<a name="usage"></a>用法
-----

```xml
<wscn:DeviceConditionCleared>
  child elements
</wscn:DeviceConditionCleared>
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
<td><p><a href="conditioncleartime.md" data-raw-source="[&lt;strong&gt;ConditionClearTime&lt;/strong&gt;](conditioncleartime.md)"><strong>ConditionClearTime</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="conditionid.md" data-raw-source="[&lt;strong&gt;ConditionId&lt;/strong&gt;](conditionid.md)"><strong>ConditionId</strong></a></p></td>
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
<td><p><a href="scannerstatusconditionevent.md" data-raw-source="[&lt;strong&gt;ScannerStatusConditionEvent&lt;/strong&gt;](scannerstatusconditionevent.md)"><strong>ScannerStatusConditionEvent</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**DeviceConditionCleared**元素包含[ **ConditionId** ](conditionid.md)并[ **ConditionClearTime** ](conditioncleartime.md)元素，用于指定的条件标识符和时间的条件已清除，分别。 WSD 扫描服务发送**DeviceConditionCleared**元素中的客户端[ **ScannerStatusConditionClearedEvent** ](scannerstatusconditionclearedevent.md)事件元素。

## <a name="see-also"></a>请参阅


[**ConditionClearTime**](conditioncleartime.md)

[**ConditionId**](conditionid.md)

[**DeviceCondition**](devicecondition.md)

[**DeviceConditionCleared**](deviceconditioncleared.md)

[**ScannerStatusConditionClearedEvent**](scannerstatusconditionclearedevent.md)

[**ScannerStatusConditionEvent**](scannerstatusconditionevent.md)

 

 






