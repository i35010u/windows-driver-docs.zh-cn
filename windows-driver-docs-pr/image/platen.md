---
title: 影印元素
description: 可选的 "影印" 元素说明扫描仪上可用的平板影印功能。
keywords:
- 影印元素图像设备
topic_type:
- apiref
api_name:
- wscn Platen
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 615e4dbde2fb9c3c0d18c124f8f8adcd2fd761d1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841083"
---
# <a name="platen-element"></a>影印元素


可选的 " **影印** " 元素说明扫描仪上可用的平板影印功能。

<a name="usage"></a>使用情况
-----

```xml
<wscn:Platen>
  child elements
</wscn:Platen>
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
<td><p><a href="platencolor.md" data-raw-source="[&lt;strong&gt;PlatenColor&lt;/strong&gt;](platencolor.md)"><strong>PlatenColor</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="platenmaximumsize.md" data-raw-source="[&lt;strong&gt;PlatenMaximumSize&lt;/strong&gt;](platenmaximumsize.md)"><strong>PlatenMaximumSize</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="platenminimumsize.md" data-raw-source="[&lt;strong&gt;PlatenMinimumSize&lt;/strong&gt;](platenminimumsize.md)"><strong>PlatenMinimumSize</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="platenopticalresolution.md" data-raw-source="[&lt;strong&gt;PlatenOpticalResolution&lt;/strong&gt;](platenopticalresolution.md)"><strong>PlatenOpticalResolution</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="platenresolutions.md" data-raw-source="[&lt;strong&gt;PlatenResolutions&lt;/strong&gt;](platenresolutions.md)"><strong>PlatenResolutions</strong></a></p></td>
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
<td><p><a href="scannerconfiguration.md" data-raw-source="[&lt;strong&gt;ScannerConfiguration&lt;/strong&gt;](scannerconfiguration.md)"><strong>ScannerConfiguration</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

如果扫描设备有平板影印，则 WSD 扫描服务必须 **提供所有子** 元素的配置信息。

## <a name="see-also"></a>请参阅


[**PlatenColor**](platencolor.md)

[**PlatenMaximumSize**](platenmaximumsize.md)

[**PlatenMinimumSize**](platenminimumsize.md)

[**PlatenOpticalResolution**](platenopticalresolution.md)

[**PlatenResolutions**](platenresolutions.md)

[**ScannerConfiguration**](scannerconfiguration.md)

 

 






