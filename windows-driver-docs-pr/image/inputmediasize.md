---
title: InputMediaSize 元素
description: 必需的 InputMediaSize 元素指定要为当前作业扫描的媒体的大小。
keywords:
- InputMediaSize 元素图像设备
topic_type:
- apiref
api_name:
- wscn InputMediaSize
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28e221c0fcb03bb081810ae975e0c9df985699c2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793667"
---
# <a name="inputmediasize-element"></a>InputMediaSize 元素


必需的 **InputMediaSize** 元素指定要为当前作业扫描的媒体的大小。

<a name="usage"></a>使用情况
-----

```xml
<wscn:InputMediaSize>
  child elements
</wscn:InputMediaSize>
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
<td><p><a href="height.md" data-raw-source="[&lt;strong&gt;Height&lt;/strong&gt;](height.md)"><strong>高度</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="width.md" data-raw-source="[&lt;strong&gt;Width&lt;/strong&gt;](width.md)"><strong>宽度</strong></a></p></td>
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
<td><p><a href="inputsize.md" data-raw-source="[&lt;strong&gt;InputSize&lt;/strong&gt;](inputsize.md)"><strong>InputSize</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**InputMediaSize** 元素包含要扫描的输入媒体的宽度和高度（分别在 [**width**](width.md)和 [**height**](height.md)元素中指定）。

**Width** 元素按快速扫描方向包含原始媒体的宽度，而 **Height** 元素则以慢速扫描方向包含原始媒体的高度。 **宽度** 和 **高度** 都必须介于1到2147483648的范围内，单位为1到1分之 (1/1000) 英寸。

## <a name="see-also"></a>请参阅


[**高度**](height.md)

[**InputSize**](inputsize.md)

[**宽度**](width.md)

 

 






