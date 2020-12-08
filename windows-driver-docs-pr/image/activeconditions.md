---
title: ActiveConditions 元素
description: 必需的 ActiveConditions 元素是扫描设备上所有当前活动的条件或错误的集合。
keywords:
- ActiveConditions 元素图像设备
topic_type:
- apiref
api_name:
- wscn ActiveConditions
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f087f339b252ff0d3fb5ab7c0759100f4c88c723
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808291"
---
# <a name="activeconditions-element"></a>ActiveConditions 元素


必需的 **ActiveConditions** 元素是扫描设备上所有当前活动的条件或错误的集合。

<a name="usage"></a>使用情况
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

**ActiveConditions** 元素是描述设备中所有当前活动的条件或错误的 [**DeviceCondition**](devicecondition.md)元素列表。 设备条件在严重性上可能因严重性而异。

## <a name="see-also"></a>请参阅


[**DeviceCondition**](devicecondition.md)

[**ScannerStatus**](scannerstatus.md)

 

 






