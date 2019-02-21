---
title: StatusSummary 元素
description: 所需的 StatusSummary 元素包含扫描设备的当前状态的摘要。
ms.assetid: cb361b3b-bd73-449d-9f31-0c1aea882330
keywords:
- StatusSummary 元素成像设备
topic_type:
- apiref
api_name:
- wscn StatusSummary
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d62094720d99017ad9597c84ad3b7f3d24224c7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555771"
---
# <a name="statussummary-element"></a>StatusSummary 元素


所需**StatusSummary**元素包含扫描设备的当前状态的摘要。

<a name="usage"></a>用法
-----

```xml
<wscn:StatusSummary>
  child elements
</wscn:StatusSummary>
```

<a name="attributes"></a>属性
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

WSD 扫描服务必须包括**StatusSummary**元素会在发送时[ **ScannerStatusSummaryEvent** ](scannerstatussummaryevent.md)事件元素到客户端。 中指定扫描程序的当前状态以及为何处于此状态的原因[ **ScannerState** ](scannerstate.md)并[ **ScannerStateReasons** ](scannerstatereasons.md)元素，分别。

## <a name="see-also"></a>另请参阅


[**ScannerStateReasons**](scannerstatereasons.md)

[**ScannerState**](scannerstate.md)

**ScannerStateReasons**
[**ScannerStatusSummaryEvent**](scannerstatussummaryevent.md)

 

 






