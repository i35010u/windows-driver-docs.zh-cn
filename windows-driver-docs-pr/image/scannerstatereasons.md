---
title: ScannerStateReasons 元素
description: 所需的 ScannerStateReasons 元素是描述所有扫描程序是在其当前状态的原因 ScannerStateReason 元素的列表。
ms.assetid: 1b4e6537-4175-4bed-9af3-7887a2737784
keywords:
- ScannerStateReasons 元素成像设备
topic_type:
- apiref
api_name:
- wscn ScannerStateReasons
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ff69c1bf009a1dd31f474d949589aa7ef16ffed
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565149"
---
# <a name="scannerstatereasons-element"></a>ScannerStateReasons 元素


所需**ScannerStateReasons**元素是一系列[ **ScannerStateReason** ](scannerstatereason.md)元素描述所有扫描程序是在其当前状态的原因。

<a name="usage"></a>用法
-----

```xml
<wscn:ScannerStateReasons>
  child elements
</wscn:ScannerStateReasons>
```

<a name="attributes"></a>特性
----------

没有特性。

<a name="text-value"></a>文本值
----------

无

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
<td><p><a href="scannerstatereason.md" data-raw-source="[&lt;strong&gt;ScannerStateReason&lt;/strong&gt;](scannerstatereason.md)"><strong>ScannerStateReason</strong></a></p></td>
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
<tr class="even">
<td><p><a href="statussummary.md" data-raw-source="[&lt;strong&gt;StatusSummary&lt;/strong&gt;](statussummary.md)"><strong>StatusSummary</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**ScannerStateReasons**元素是一系列**ScannerStateReason**元素，其中每个描述扫描程序处于其当前状态的原因。

WSD 扫描服务将通过发送有关扫描程序的状态更改通知客户端[ **ScannerStatusSummaryEvent** ](scannerstatussummaryevent.md)事件。 客户端可以直接查询扫描程序的状态，通过调用[ **GetScannerElementsRequest** ](getscannerelementsrequest.md)操作。

## <a name="see-also"></a>请参阅


[**GetScannerElementsRequest**](getscannerelementsrequest.md)

[**ScannerStateReason**](scannerstatereason.md)

[**ScannerStatus**](scannerstatus.md)

[**ScannerStatusSummaryEvent**](scannerstatussummaryevent.md)

[**StatusSummary**](statussummary.md)

 

 






