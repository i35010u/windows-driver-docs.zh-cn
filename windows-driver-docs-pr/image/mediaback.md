---
title: MediaBack 元素
description: 可选 MediaBack 元素包含特定于物理介质的后端的扫描的所有参数。
ms.assetid: d736c76f-7ea7-49ca-9ad9-df35924fc7b4
keywords:
- MediaBack 元素成像设备
topic_type:
- apiref
api_name:
- wscn MediaBack
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e149509b47163193ad9e2f3bd10d08eb69f78b2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380354"
---
# <a name="mediaback-element"></a>MediaBack 元素


可选**MediaBack**元素不包含特定于物理介质的后端的扫描的所有参数。

<a name="usage"></a>用法
-----

```xml
<wscn:MediaBack>
  child elements
</wscn:MediaBack>
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
<td><p><a href="colorprocessing.md" data-raw-source="[&lt;strong&gt;ColorProcessing&lt;/strong&gt;](colorprocessing.md)"><strong>ColorProcessing</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="resolution.md" data-raw-source="[&lt;strong&gt;Resolution&lt;/strong&gt;](resolution.md)"><strong>解决方法</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="scanregion.md" data-raw-source="[&lt;strong&gt;ScanRegion&lt;/strong&gt;](scanregion.md)"><strong>ScanRegion</strong></a></p></td>
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
<td><p><a href="mediasides.md" data-raw-source="[&lt;strong&gt;MediaSides&lt;/strong&gt;](mediasides.md)"><strong>MediaSides</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**MediaBack**元素是有效的扫描程序仅从时支持双工扫描和当前中定义的输入的源[ **InputSource** ](inputsource.md)元素，是**ADFDuplex**。

如果**MediaBack**元素不包含[ **ScanRegion** ](scanregion.md)元素，WSD 扫描服务应使用 0，作为偏移量的宽度和高度[**InputMediaSize**](inputmediasize.md)，如果给定。 如果**ScanRegion**缺少和**InputMediaSize**未指定或不能由扫描设备，你可以确定实现。

如果输入的源**ADFDuplex**并**MediaBack**缺少元素，在中指定的所有参数[ **MediaFront** ](mediafront.md)将适用于扫描以及在后端。

## <a name="see-also"></a>请参阅


[**ColorProcessing**](colorprocessing.md)

[**InputMediaSize**](inputmediasize.md)

[**InputSource**](inputsource.md)

[**MediaFront**](mediafront.md)

[**MediaSides**](mediasides.md)

[**解决方法**](resolution.md)

[**ScanRegion**](scanregion.md)

 

 






