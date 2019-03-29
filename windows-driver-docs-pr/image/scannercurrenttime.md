---
title: ScannerCurrentTime 元素
description: 所需的 ScannerCurrentTime 元素指示当前日期和时间根据扫描程序的内部时钟。
ms.assetid: 7103fdb4-dfa4-40b0-b20e-022e2a42bf5c
keywords:
- ScannerCurrentTime 元素成像设备
topic_type:
- apiref
api_name:
- wscn ScannerCurrentTime
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4ca5252e639acd9ae6d72c82ed55e1986849c6b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569355"
---
# <a name="scannercurrenttime-element"></a>ScannerCurrentTime 元素


所需**ScannerCurrentTime**元素指示当前日期和时间根据扫描程序的内部时钟。

<a name="usage"></a>用法
-----

```xml
<wscn:ScannerCurrentTime>
  text
</wscn:ScannerCurrentTime>
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
<td><p><a href="scannerstatus.md" data-raw-source="[&lt;strong&gt;ScannerStatus&lt;/strong&gt;](scannerstatus.md)"><strong>ScannerStatus</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

扫描程序的内部时钟不需要实时时钟。 时钟可以从零开始 (0001-01-01T00:00:00Z) 并开始在设备开启时计数。

所有时间都基于在启动时，时间以便在客户端可以通过阅读计算持续时间和相对时间**ScannerCurrentTime**元素并将它与以前的时间值进行比较。

## <a name="see-also"></a>请参阅


[**ScannerStatus**](scannerstatus.md)

 

 






