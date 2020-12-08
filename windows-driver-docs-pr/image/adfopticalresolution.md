---
title: ADFOpticalResolution 元素
description: Required ADFOpticalResolution 元素指定自动文档送纸器的前端或背面 (ADF) 可以扫描的最大光学分辨率。
keywords:
- ADFOpticalResolution 元素图像设备
topic_type:
- apiref
api_name:
- wscn ADFOpticalResolution
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d9d118a7352d1c4b9ddd27489eb7d91c4478614
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837761"
---
# <a name="adfopticalresolution-element"></a>ADFOpticalResolution 元素


Required **ADFOpticalResolution** 元素指定自动文档送纸器的前端或背面 (ADF) 可以扫描的最大光学分辨率。

<a name="usage"></a>使用情况
-----

```xml
<wscn:ADFOpticalResolution>
  child elements
</wscn:ADFOpticalResolution>
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
<td><p><a href="adfback.md" data-raw-source="[&lt;strong&gt;ADFBack&lt;/strong&gt;](adfback.md)"><strong>ADFBack</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="adffront.md" data-raw-source="[&lt;strong&gt;ADFFront&lt;/strong&gt;](adffront.md)"><strong>ADFFront</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

分辨率指定为 [**宽度**](width.md) × [**高度**](height.md) 对，其中的 **宽度** 和 **高度** 均以每英寸像素数来指定。

如果 **ADFOpticalResolution** 元素的父元素为 [**ADFFront**](adffront.md)，则指定的光学分辨率适用于 ADF 的正面;否则，父元素为 [**ADFBack**](adfback.md) ，光盘分辨率适用于 ADF 的背面。

## <a name="see-also"></a>请参阅


[**ADFBack**](adfback.md)

[**ADFFront**](adffront.md)

[**高度**](height.md)

[**宽度**](width.md)

 

 






