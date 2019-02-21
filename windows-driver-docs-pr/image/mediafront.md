---
title: MediaFront 元素
description: 所需的 MediaFront 元素不包含特定于扫描的物理介质的前端的所有参数。
ms.assetid: 1bde587b-4057-4368-b075-c22561ee45cc
keywords:
- MediaFront 元素成像设备
topic_type:
- apiref
api_name:
- wscn MediaFront
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22cf7082d4a2693be3830c7962fcb8a3b09b337f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534410"
---
# <a name="mediafront-element"></a>MediaFront 元素


所需**MediaFront**元素不包含特定于扫描的物理介质的前端的所有参数。

<a name="usage"></a>用法
-----

```xml
<wscn:MediaFront>
  child elements
</wscn:MediaFront>
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

如果**MediaFront**元素不包含[ **ScanRegion** ](scanregion.md)元素，WSD 扫描服务应使用 0，作为偏移量的宽度和高度[**InputMediaSize**](inputmediasize.md)，如果给定。 如果**ScanRegion**缺少和**InputMediaSize**未指定或不能由扫描设备，你可以确定实现。

## <a name="see-also"></a>另请参阅


[**ColorProcessing**](colorprocessing.md)

[**InputMediaSize**](inputmediasize.md)

[**MediaBack**](mediaback.md)

[**MediaSides**](mediasides.md)

[**解决方法**](resolution.md)

[**ScanRegion**](scanregion.md)

 

 






