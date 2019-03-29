---
title: ScanRegion 元素
description: 可选 ScanRegion 元素指定要扫描的输入的文档边界内的区域。
ms.assetid: 29b94df7-503d-4bbd-99a8-9092140c6629
keywords:
- ScanRegion 元素成像设备
topic_type:
- apiref
api_name:
- wscn ScanRegion
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3978b3e780aa2a2b778819dceb42ec4dfdbc366
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568748"
---
# <a name="scanregion-element"></a>ScanRegion 元素


可选**ScanRegion**元素指定要扫描的输入的文档边界内的区域。

<a name="usage"></a>用法
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

所有**ScanRegion**值表示一个千分之几秒 (1/1000) 的英寸为单位。

如果扫描作业的请求的扫描区域会完全不属于扫描设备的受支持的获取区域，则应拒绝扫描操作。

[**ScanRegionXOffset**](scanregionxoffset.md) + [**ScanRegionWidth** ](scanregionwidth.md)必须等于或小于比[ **InputSize** ](inputsize.md)宽度。

[**ScanRegionYOffset**](scanregionyoffset.md) + [**ScanRegionHeight** ](scanregionheight.md)必须等于或小于比**InputSize**高度。

如果它不能满足指定的尺寸，WSD 扫描服务可以调整请求的扫描区域。 中应该报告对扫描区域的任何更改[ **DocumentFinalParameters** ](documentfinalparameters.md)扫描作业中的元素。

## <a name="see-also"></a>请参阅


[**DocumentFinalParameters**](documentfinalparameters.md)

[**InputSize**](inputsize.md)

[**MediaBack**](mediaback.md)

[**MediaFront**](mediafront.md)

[**ScanRegionHeight**](scanregionheight.md)

[**ScanRegionWidth**](scanregionwidth.md)

[**ScanRegionXOffset**](scanregionxoffset.md)

[**ScanRegionYOffset**](scanregionyoffset.md)

 

 






