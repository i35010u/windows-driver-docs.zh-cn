---
title: ADFFront 元素
description: 所需的 ADFFront 元素描述的自动文档送纸器 (ADF) 附加到扫描程序前端的功能。
ms.assetid: 6b49f5da-6866-4ec6-8973-7c582bd3a1a1
keywords:
- ADFFront 元素成像设备
topic_type:
- apiref
api_name:
- wscn ADFFront
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: eda5373bd855dc0d2108174e36c6fb100c43194a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367085"
---
# <a name="adffront-element"></a>ADFFront 元素


所需**ADFFront**元素描述的自动文档送纸器 (ADF) 附加到扫描程序前端的功能。

<a name="usage"></a>用法
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

如果扫描仪具有 ADF WSD 扫描服务必须中为其提供详细信息**ADFFront**元素，而不考虑的 ADF 进行双面打印功能。

## <a name="see-also"></a>请参阅


[**ADF**](adf.md)

[**ADFColor**](adfcolor.md)

[**ADFMaximumSize**](adfmaximumsize.md)

[**ADFMinimumSize**](adfminimumsize.md)

[**ADFOpticalResolution**](adfopticalresolution.md)

[**ADFResolutions**](adfresolutions.md)

 

 






