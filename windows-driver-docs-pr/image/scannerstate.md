---
title: ScannerState 元素
description: 必需的 ScannerState 元素标识扫描设备扫描部分的当前状态。
keywords:
- ScannerState 元素图像设备
topic_type:
- apiref
api_name:
- wscn ScannerState
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94cd0eb9ba6d26a799dcdb4fc9f21b8b1284aa87
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816205"
---
# <a name="scannerstate-element"></a>ScannerState 元素


必需的 **ScannerState** 元素标识扫描设备扫描部分的当前状态。

<a name="usage"></a>使用情况
-----

```xml
<wscn:ScannerState>
  text
</wscn:ScannerState>
```

<a name="attributes"></a>特性
----------

没有特性。

<a name="text-value"></a>文本值
----------

必需。 以下字符串值之一。

| “值”      | 描述                                                  |
|------------|--------------------------------------------------------------|
| 闲置       | 扫描仪可用，可以开始处理新作业。 |
| 处理 | 扫描仪当前正在处理作业。                    |
| 已停止    | 不能处理作业并且不需要进行干预。         |

 

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
<tr class="even">
<td><p><a href="statussummary.md" data-raw-source="[&lt;strong&gt;StatusSummary&lt;/strong&gt;](statussummary.md)"><strong>StatusSummary</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

[**GetScannerElementsRequest**](getscannerelementsrequest.md)

WSD 扫描服务通过发送 [**ScannerStatusSummaryEvent**](scannerstatussummaryevent.md) 事件向客户端通知扫描程序状态的更改。 客户端可以通过调用 [**GetScannerElementsRequest**](getscannerelementsrequest.md) 操作直接查询扫描程序的状态。

可以扩展和子集化此元素的允许值。

## <a name="see-also"></a>请参阅


[**GetScannerElementsRequest**](getscannerelementsrequest.md)

[**ScannerStatus**](scannerstatus.md)

[**ScannerStatusSummaryEvent**](scannerstatussummaryevent.md)

[**StatusSummary**](statussummary.md)

 

 






