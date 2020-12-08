---
title: ScanRegion 元素
description: 可选的 ScanRegion 元素指定要在输入文档边界内扫描的区域。
keywords:
- ScanRegion 元素图像设备
topic_type:
- apiref
api_name:
- wscn ScanRegion
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e41d86c09e946af32fb3e2a12a3a022a10b13cd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826845"
---
# <a name="scanregion-element"></a>ScanRegion 元素


可选的 **ScanRegion** 元素指定要在输入文档边界内扫描的区域。

<a name="usage"></a>使用情况
-----

```xml
<wscn:ScanRegion>
  child elements
</wscn:ScanRegion>
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
<td><p><a href="scanregionheight.md" data-raw-source="[&lt;strong&gt;ScanRegionHeight&lt;/strong&gt;](scanregionheight.md)"><strong>ScanRegionHeight</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="scanregionwidth.md" data-raw-source="[&lt;strong&gt;ScanRegionWidth&lt;/strong&gt;](scanregionwidth.md)"><strong>ScanRegionWidth</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="scanregionxoffset.md" data-raw-source="[&lt;strong&gt;ScanRegionXOffset&lt;/strong&gt;](scanregionxoffset.md)"><strong>ScanRegionXOffset</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="scanregionyoffset.md" data-raw-source="[&lt;strong&gt;ScanRegionYOffset&lt;/strong&gt;](scanregionyoffset.md)"><strong>ScanRegionYOffset</strong></a></p></td>
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
<td><p><a href="mediaback.md" data-raw-source="[&lt;strong&gt;MediaBack&lt;/strong&gt;](mediaback.md)"><strong>MediaBack</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="mediafront.md" data-raw-source="[&lt;strong&gt;MediaFront&lt;/strong&gt;](mediafront.md)"><strong>MediaFront</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

所有 **ScanRegion** 值都代表一 (1/1000) 英寸。

如果扫描作业的请求扫描区域完全超出了扫描设备支持的购置区域，则应拒绝扫描操作。

[**ScanRegionXOffset**](scanregionxoffset.md)  + [**ScanRegionWidth**](scanregionwidth.md)必须等于或小于 [**InputSize**](inputsize.md)宽度。

[**ScanRegionYOffset**](scanregionyoffset.md)  + [**ScanRegionHeight**](scanregionheight.md)必须等于或小于 **InputSize** 高度。

如果 WSD 扫描服务无法满足指定的维度，则可以调整请求的扫描区域。 扫描区域中的任何更改都应在扫描作业的 [**DocumentFinalParameters**](documentfinalparameters.md) 元素中报告。

## <a name="see-also"></a>请参阅


[**DocumentFinalParameters**](documentfinalparameters.md)

[**InputSize**](inputsize.md)

[**MediaBack**](mediaback.md)

[**MediaFront**](mediafront.md)

[**ScanRegionHeight**](scanregionheight.md)

[**ScanRegionWidth**](scanregionwidth.md)

[**ScanRegionXOffset**](scanregionxoffset.md)

[**ScanRegionYOffset**](scanregionyoffset.md)

 

 






