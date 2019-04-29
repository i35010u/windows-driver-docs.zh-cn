---
title: ActiveConditions 元素
description: 所需的 ActiveConditions 元素是所有的当前处于活动状态的条件或扫描设备上的错误的集合。
ms.assetid: e66196af-d794-4ffe-99e5-c0f8ea4ffe74
keywords:
- ActiveConditions 元素成像设备
topic_type:
- apiref
api_name:
- wscn ActiveConditions
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b556ffc0fa4b75b6b2e7639433e5a62af4d573c6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367108"
---
# <a name="activeconditions-element"></a>ActiveConditions 元素


所需**ActiveConditions**元素是所有的当前处于活动状态的条件或扫描设备上的错误的集合。

<a name="usage"></a>用法
-----

```xml
<wscn:ActiveConditions>
  child elements
</wscn:ActiveConditions>
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
<td><p><a href="devicecondition.md" data-raw-source="[&lt;strong&gt;DeviceCondition&lt;/strong&gt;](devicecondition.md)"><strong>DeviceCondition</strong></a></p></td>
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
<td><p><a href="scannerstatus.md" data-raw-source="[&lt;strong&gt;ScannerStatus&lt;/strong&gt;](scannerstatus.md)"><strong>ScannerStatus</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**ActiveConditions**元素是一系列[ **DeviceCondition** ](devicecondition.md)描述的所有当前处于活动状态的条件或设备中的错误的元素。 设备条件而异中从信息性严重程度上为严重。

## <a name="see-also"></a>请参阅


[**DeviceCondition**](devicecondition.md)

[**ScannerStatus**](scannerstatus.md)

 

 






