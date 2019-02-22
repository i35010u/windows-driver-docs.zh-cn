---
title: ConditionHistory 元素
description: 可选 ConditionHistory 元素是在扫描仪提供有关最新的条件和错误的详细信息的 ConditionHistoryEntry 元素的集合。
ms.assetid: 3725a635-6571-4a34-b8f9-9fe6881bd6da
keywords:
- ConditionHistory 元素成像设备
topic_type:
- apiref
api_name:
- wscn ConditionHistory
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9c0438c690d72dcbc166f0756b8d3019e3b5ca2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554345"
---
# <a name="conditionhistory-element"></a>ConditionHistory 元素


可选**ConditionHistory**元素包含一系列[ **ConditionHistoryEntry** ](conditionhistoryentry.md)提供了有关最新的条件和错误的详细信息，扫描程序的元素.

<a name="usage"></a>用法
-----

```xml
<wscn:ConditionHistory>
  child elements
</wscn:ConditionHistory>
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

客户端可以查询的扫描程序**ConditionHistory**元素通过调用[ **GetScannerElementsRequest** ](getscannerelementsrequest.md)操作。

在从信息性严重程度上为严重不同条件。

## <a name="see-also"></a>另请参阅


[**ConditionHistoryEntry**](conditionhistoryentry.md)

[**GetScannerElementsRequest**](getscannerelementsrequest.md)

[**ScannerStatus**](scannerstatus.md)

 

 






