---
title: DeviceConditionCleared 元素
description: 必需的 DeviceConditionCleared 元素包含有关以前报告的已清除 DeviceCondition 条件的信息。
keywords:
- DeviceConditionCleared 元素图像设备
topic_type:
- apiref
api_name:
- wscn DeviceConditionCleared
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d51521348b097105dbda504926b98d2c8f3e16e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824551"
---
# <a name="deviceconditioncleared-element"></a>DeviceConditionCleared 元素


必需的 **DeviceConditionCleared** 元素包含有关以前报告的已清除 [**DeviceCondition**](devicecondition.md) 条件的信息。

<a name="usage"></a>使用情况
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

**DeviceConditionCleared** 元素包含 [**ConditionId**](conditionid.md)和 [**ConditionClearTime**](conditioncleartime.md)元素，这些元素分别指定条件标识符和清除条件的时间。 WSD 扫描服务将 **DeviceConditionCleared** 元素发送到 [**ScannerStatusConditionClearedEvent**](scannerstatusconditionclearedevent.md) 事件元素中的客户端。

## <a name="see-also"></a>请参阅


[**ConditionClearTime**](conditioncleartime.md)

[**ConditionId**](conditionid.md)

[**DeviceCondition**](devicecondition.md)

[**DeviceConditionCleared**](deviceconditioncleared.md)

[**ScannerStatusConditionClearedEvent**](scannerstatusconditionclearedevent.md)

[**ScannerStatusConditionEvent**](scannerstatusconditionevent.md)

 

 






