---
title: ConditionHistory 元素
description: 可选的 ConditionHistory 元素是 ConditionHistoryEntry 元素的集合，这些元素提供有关扫描仪上的最新条件和错误的详细信息。
keywords:
- ConditionHistory 元素图像设备
topic_type:
- apiref
api_name:
- wscn ConditionHistory
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 404b477259d56fb747c478320858434cdf84ae2a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830497"
---
# <a name="conditionhistory-element"></a>ConditionHistory 元素


可选的 **ConditionHistory** 元素是 [**ConditionHistoryEntry**](conditionhistoryentry.md) 元素的集合，这些元素提供有关扫描仪上的最新条件和错误的详细信息。

<a name="usage"></a>使用情况
-----

```xml
<wscn:ConditionHistory>
  child elements
</wscn:ConditionHistory>
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
<td><p><a href="conditionhistoryentry.md" data-raw-source="[&lt;strong&gt;ConditionHistoryEntry&lt;/strong&gt;](conditionhistoryentry.md)"><strong>ConditionHistoryEntry</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>父元素


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>元素</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="scannerstatus.md" data-raw-source="[&lt;strong&gt;ScannerStatus&lt;/strong&gt;](scannerstatus.md)"><strong>ScannerStatus</strong></a></p></td>
<td><p></p>
<p>ScannerStatus</p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

客户端可以通过调用 [**GetScannerElementsRequest**](getscannerelementsrequest.md)操作来查询扫描程序的 **ConditionHistory** 元素。

条件的严重性因严重性而异。

## <a name="see-also"></a>请参阅


[**ConditionHistoryEntry**](conditionhistoryentry.md)

[**GetScannerElementsRequest**](getscannerelementsrequest.md)

[**ScannerStatus**](scannerstatus.md)

 

 






