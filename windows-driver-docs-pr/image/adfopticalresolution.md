---
title: ADFOpticalResolution 元素
description: 所需的 ADFOpticalResolution 元素指定的最大的光学分辨率自动文档送纸器 (ADF) 的前端或后端可以从该处进行扫描。
ms.assetid: 2000dbe4-9733-4a69-9e4e-c53c5a1c24c0
keywords:
- ADFOpticalResolution 元素成像设备
topic_type:
- apiref
api_name:
- wscn ADFOpticalResolution
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2c2e683281d2a3073a4d950a3a78dfee2aa466b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367083"
---
# <a name="adfopticalresolution-element"></a>ADFOpticalResolution 元素


所需**ADFOpticalResolution**元素指定的最大的光学分辨率自动文档送纸器 (ADF) 的前端或后端可以从该处进行扫描。

<a name="usage"></a>用法
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
<td><p><a href="adfback.md" data-raw-source="[&lt;strong&gt;ADFBack&lt;/strong&gt;](adfback.md)"><strong>ADFBack</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="adffront.md" data-raw-source="[&lt;strong&gt;ADFFront&lt;/strong&gt;](adffront.md)"><strong>ADFFront</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

解决方法指定为[**宽度**](width.md) × [**高度**](height.md)对，其中同时**宽度**和**高度**以每英寸点数的像素为单位指定。

如果父元素的**ADFOpticalResolution**元素是[ **ADFFront**](adffront.md)，指定光学分辨率适用于前面端 ADF 的; 否则为父元素是[ **ADFBack** ](adfback.md)和光学分辨率适用于 ADF 的后端。

## <a name="see-also"></a>请参阅


[**ADFBack**](adfback.md)

[**ADFFront**](adffront.md)

[**Height**](height.md)

[**Width**](width.md)

 

 






