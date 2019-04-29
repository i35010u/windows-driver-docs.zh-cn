---
title: ConditionId 元素
description: 所需的 ConditionId 元素唯一地标识只是清除设备条件。
ms.assetid: 4b154fb3-625e-478d-9bb4-92fd7cae0530
keywords:
- ConditionId 元素成像设备
topic_type:
- apiref
api_name:
- wscn ConditionId
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e49396c39e20c72640ae8d1be573bc0f6184856
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368589"
---
# <a name="conditionid-element"></a>ConditionId 元素


所需**ConditionId**元素唯一地标识只是清除设备条件。

<a name="usage"></a>用法
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

必需。 一个整数值，它等效于先前报告 DeviceCondition 元素的 Id 属性。

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
<td><p><a href="deviceconditioncleared.md" data-raw-source="[&lt;strong&gt;DeviceConditionCleared&lt;/strong&gt;](deviceconditioncleared.md)"><strong>DeviceConditionCleared</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**ConditionId**元素必须**Id**的属性**DeviceCondition** WSD 扫描服务通过以前报告的元素[ **ScannerStatusConditionEvent**](scannerstatusconditionevent.md)。

## <a name="see-also"></a>请参阅


[**DeviceCondition**](devicecondition.md)

[**DeviceConditionCleared**](deviceconditioncleared.md)

[**ScannerStatusConditionEvent**](scannerstatusconditionevent.md)

 

 






