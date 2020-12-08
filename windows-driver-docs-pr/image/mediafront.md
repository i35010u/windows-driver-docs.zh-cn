---
title: MediaFront 元素
description: 必需的 MediaFront 元素包含特定于对物理介质的前一层扫描的所有参数。
keywords:
- MediaFront 元素图像设备
topic_type:
- apiref
api_name:
- wscn MediaFront
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b0a7edc4736b95cad44f8619e8800027cd790b08
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840975"
---
# <a name="mediafront-element"></a>MediaFront 元素


必需的 **MediaFront** 元素包含特定于对物理介质的前一层扫描的所有参数。

<a name="usage"></a>使用情况
-----

```xml
<wscn:MediaFront>
  child elements
</wscn:MediaFront>
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

如果 **MediaFront** 元素不包含 [**ScanRegion**](scanregion.md) 元素，则 WSD 扫描服务应使用0作为偏移量，并使用 [**InputMediaSize**](inputmediasize.md)的宽度和高度（如果给定）。 如果缺少 **ScanRegion** ，但未指定 **InputMediaSize** 或扫描设备无法确定，可以确定实现。

## <a name="see-also"></a>请参阅


[**ColorProcessing**](colorprocessing.md)

[**InputMediaSize**](inputmediasize.md)

[**MediaBack**](mediaback.md)

[**MediaSides**](mediasides.md)

[**解决方法**](resolution.md)

[**ScanRegion**](scanregion.md)

 

 






