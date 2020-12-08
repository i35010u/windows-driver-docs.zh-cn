---
title: StatusSummary 元素
description: 必需的 StatusSummary 元素包含扫描设备当前状态的摘要。
keywords:
- StatusSummary 元素图像设备
topic_type:
- apiref
api_name:
- wscn StatusSummary
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 661ab8dc3c6ae2b3918e9f2dc4d87f392f7330af
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817325"
---
# <a name="statussummary-element"></a>StatusSummary 元素


必需的 **StatusSummary** 元素包含扫描设备当前状态的摘要。

<a name="usage"></a>使用情况
-----

```xml
<wscn:StatusSummary>
  child elements
</wscn:StatusSummary>
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
<td><p><a href="scannerstate.md" data-raw-source="[&lt;strong&gt;ScannerState&lt;/strong&gt;](scannerstate.md)"><strong>ScannerState</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="scannerstatereasons.md" data-raw-source="[&lt;strong&gt;ScannerStateReasons&lt;/strong&gt;](scannerstatereasons.md)"><strong>ScannerStateReasons</strong></a></p></td>
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
<td><p><a href="scannerstatussummaryevent.md" data-raw-source="[&lt;strong&gt;ScannerStatusSummaryEvent&lt;/strong&gt;](scannerstatussummaryevent.md)"><strong>ScannerStatusSummaryEvent</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

当 WSD 扫描服务将 [**ScannerStatusSummaryEvent**](scannerstatussummaryevent.md)事件元素发送到客户端时，它必须包含 **StatusSummary** 元素。 该扫描程序的当前状态以及其处于此状态的原因可能是分别在 [**ScannerState**](scannerstate.md) 和 [**ScannerStateReasons**](scannerstatereasons.md) 元素中指定的。

## <a name="see-also"></a>请参阅


[**ScannerStateReasons**](scannerstatereasons.md)

[**ScannerState**](scannerstate.md)

**ScannerStateReasons** 
[ **ScannerStatusSummaryEvent**](scannerstatussummaryevent.md)

 

 






