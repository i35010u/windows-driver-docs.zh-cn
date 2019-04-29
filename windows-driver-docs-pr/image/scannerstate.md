---
title: ScannerState 元素
description: 所需的 ScannerState 元素标识扫描设备的扫描部分的当前状态。
ms.assetid: 64cd5319-a52d-4ff3-976c-060886381d11
keywords:
- ScannerState 元素成像设备
topic_type:
- apiref
api_name:
- wscn ScannerState
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5a7268352d44d6b2f012dcaaa5d41020aa57d32
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370048"
---
# <a name="scannerstate-element"></a>ScannerState 元素


所需**ScannerState**元素标识扫描设备的扫描部分的当前状态。

<a name="usage"></a>用法
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

| ReplTest1      | 描述                                                  |
|------------|--------------------------------------------------------------|
| 空闲       | 扫描程序可用，可以开始处理新作业。 |
| 正在处理 | 扫描程序当前正在处理作业。                    |
| 已停止    | 没有作业可以处理，并且需要干预。         |

 

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
<tr class="even">
<td><p><a href="statussummary.md" data-raw-source="[&lt;strong&gt;StatusSummary&lt;/strong&gt;](statussummary.md)"><strong>StatusSummary</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

[**GetScannerElementsRequest**](getscannerelementsrequest.md)

WSD 扫描服务将通过发送有关扫描程序的状态更改通知客户端[ **ScannerStatusSummaryEvent** ](scannerstatussummaryevent.md)事件。 客户端可以直接查询扫描程序的状态，通过调用[ **GetScannerElementsRequest** ](getscannerelementsrequest.md)操作。

您都可以扩展和子集的允许的值为此元素。

## <a name="see-also"></a>请参阅


[**GetScannerElementsRequest**](getscannerelementsrequest.md)

[**ScannerStatus**](scannerstatus.md)

[**ScannerStatusSummaryEvent**](scannerstatussummaryevent.md)

[**StatusSummary**](statussummary.md)

 

 






