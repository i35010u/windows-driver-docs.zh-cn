---
title: ADFFront 元素
description: 必需的 ADFFront 元素描述附加到扫描仪的自动文档送纸器 (ADF) 的前端功能。
keywords:
- ADFFront 元素图像设备
topic_type:
- apiref
api_name:
- wscn ADFFront
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1606e8a7bb73cb3f4c495d5c4c89c251561d2e0d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837765"
---
# <a name="adffront-element"></a>ADFFront 元素


必需的 **ADFFront** 元素描述附加到扫描仪的自动文档送纸器 (ADF) 的前端功能。

<a name="usage"></a>使用情况
-----

```xml
<wscn:ADFFront>
  child elements
</wscn:ADFFront>
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
<td><p><a href="adfcolor.md" data-raw-source="[&lt;strong&gt;ADFColor&lt;/strong&gt;](adfcolor.md)"><strong>ADFColor</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="adfmaximumsize.md" data-raw-source="[&lt;strong&gt;ADFMaximumSize&lt;/strong&gt;](adfmaximumsize.md)"><strong>ADFMaximumSize</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="adfminimumsize.md" data-raw-source="[&lt;strong&gt;ADFMinimumSize&lt;/strong&gt;](adfminimumsize.md)"><strong>ADFMinimumSize</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="adfopticalresolution.md" data-raw-source="[&lt;strong&gt;ADFOpticalResolution&lt;/strong&gt;](adfopticalresolution.md)"><strong>ADFOpticalResolution</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="adfresolutions.md" data-raw-source="[&lt;strong&gt;ADFResolutions&lt;/strong&gt;](adfresolutions.md)"><strong>ADFResolutions</strong></a></p></td>
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
<td><p><a href="adf.md" data-raw-source="[&lt;strong&gt;ADF&lt;/strong&gt;](adf.md)"><strong>ADF</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

如果扫描程序具有 ADF，WSD 扫描服务必须在 **ADFFront** 元素中提供其详细信息，而不考虑 ADF 的双工功能。

## <a name="see-also"></a>请参阅


[**ADF**](adf.md)

[**ADFColor**](adfcolor.md)

[**ADFMaximumSize**](adfmaximumsize.md)

[**ADFMinimumSize**](adfminimumsize.md)

[**ADFOpticalResolution**](adfopticalresolution.md)

[**ADFResolutions**](adfresolutions.md)

 

 






