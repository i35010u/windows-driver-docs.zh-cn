---
title: ScannerCurrentTime 元素
description: 必需的 ScannerCurrentTime 元素根据扫描仪的内部时钟指示当前日期和时间。
keywords:
- ScannerCurrentTime 元素图像设备
topic_type:
- apiref
api_name:
- wscn ScannerCurrentTime
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 362962e1ea8033e305f93c4909e65857f2abf1f1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832361"
---
# <a name="scannercurrenttime-element"></a>ScannerCurrentTime 元素


必需的 **ScannerCurrentTime** 元素根据扫描仪的内部时钟指示当前日期和时间。

<a name="usage"></a>使用情况
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
<td><p><a href="scannerstatus.md" data-raw-source="[&lt;strong&gt;ScannerStatus&lt;/strong&gt;](scannerstatus.md)"><strong>ScannerStatus</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

扫描仪的内部时钟不必是实时时钟。 时钟可以从零开始 (0001-01-01T00：00： 00Z) 并在设备打开时开始计算。

所有时间都基于启动时的时间，因此，客户端可以通过读取 **ScannerCurrentTime** 元素并将其与上一个时间值进行比较来计算持续时间和相对时间。

## <a name="see-also"></a>请参阅


[**ScannerStatus**](scannerstatus.md)

 

 






