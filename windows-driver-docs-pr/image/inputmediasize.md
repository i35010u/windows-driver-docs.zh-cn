---
title: InputMediaSize 元素
description: 所需的 InputMediaSize 元素指定要进行扫描当前作业的媒体的大小。
ms.assetid: f1fcb152-96c5-469c-8989-a2c4328a5f68
keywords:
- InputMediaSize 元素成像设备
topic_type:
- apiref
api_name:
- wscn InputMediaSize
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b80a5c97766d360dafd2670c78cef7bf4418198
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360053"
---
# <a name="inputmediasize-element"></a>InputMediaSize 元素


所需**InputMediaSize**元素指定要进行扫描当前作业的媒体的大小。

<a name="usage"></a>用法
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
<td><p><a href="height.md" data-raw-source="[&lt;strong&gt;Height&lt;/strong&gt;](height.md)"><strong>Height</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="width.md" data-raw-source="[&lt;strong&gt;Width&lt;/strong&gt;](width.md)"><strong>Width</strong></a></p></td>
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

**InputMediaSize**元素包含的宽度和高度要扫描的输入媒体中指定[**宽度**](width.md)并[**高度** ](height.md)元素，分别。

**宽度**元素包含在快速扫描方向，原始介质的宽度和**高度**元素包含的原始媒体中进行慢扫描方向的高度。 这两**宽度**并**高度**必须介于 1 到 2147483648 和为一个千分之几秒为单位 (1/1000) 的英寸为单位。

## <a name="see-also"></a>请参阅


[**Height**](height.md)

[**InputSize**](inputsize.md)

[**Width**](width.md)

 

 






