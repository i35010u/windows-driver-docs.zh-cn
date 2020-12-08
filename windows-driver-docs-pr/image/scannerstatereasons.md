---
title: ScannerStateReasons 元素
description: 必需的 ScannerStateReasons 元素是一个 ScannerStateReason 元素列表，其中描述了扫描程序处于其当前状态的所有原因。
keywords:
- ScannerStateReasons 元素图像设备
topic_type:
- apiref
api_name:
- wscn ScannerStateReasons
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff6d72ec2b19889ac32e607390aab423a29f774c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816203"
---
# <a name="scannerstatereasons-element"></a>ScannerStateReasons 元素


必需的 **ScannerStateReasons** 元素是一个 [**ScannerStateReason**](scannerstatereason.md) 元素列表，其中描述了扫描程序处于其当前状态的所有原因。

<a name="usage"></a>使用情况
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

**ScannerStateReasons** 元素是 **ScannerStateReason** 元素的列表，其中每个元素都描述了扫描程序处于其当前状态的原因。

WSD 扫描服务通过发送 [**ScannerStatusSummaryEvent**](scannerstatussummaryevent.md) 事件向客户端通知扫描程序状态的更改。 客户端可以通过调用 [**GetScannerElementsRequest**](getscannerelementsrequest.md) 操作直接查询扫描程序的状态。

## <a name="see-also"></a>请参阅


[**GetScannerElementsRequest**](getscannerelementsrequest.md)

[**ScannerStateReason**](scannerstatereason.md)

[**ScannerStatus**](scannerstatus.md)

[**ScannerStatusSummaryEvent**](scannerstatussummaryevent.md)

[**StatusSummary**](statussummary.md)

 

 






