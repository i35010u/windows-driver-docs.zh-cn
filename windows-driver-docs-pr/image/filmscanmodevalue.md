---
title: FilmScanModeValue 元素
description: 必需的 FilmScanModeValue 元素标识胶卷扫描选项支持的特定胶片曝光类型。
keywords:
- FilmScanModeValue 元素图像设备
topic_type:
- apiref
api_name:
- wscn FilmScanModeValue
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f5639ea333acb3ee1807ea6e9291e5eb37f1b96
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808265"
---
# <a name="filmscanmodevalue-element"></a>FilmScanModeValue 元素


必需的 **FilmScanModeValue** 元素标识胶卷扫描选项支持的特定胶片曝光类型。

<a name="usage"></a>使用情况
-----

```xml
<wscn:FilmScanModeValue>
  text
</wscn:FilmScanModeValue>
```

<a name="attributes"></a>特性
----------

没有特性。

<a name="text-value"></a>文本值
----------

必需。 以下值之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>术语</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><span id="NotApplicable"></span><span id="notapplicable"></span><span id="NOTAPPLICABLE"></span>NotApplicable</p></td>
<td><p>默认扫描输入源不再是胶片选项;因此，FilmScanModeValue 不再是适用于 DefaultScanTicket 元素的值。 NotApplicable 仅在 DefaultScanTicket 元素中有效。</p></td>
</tr>
<tr class="even">
<td><p><span id="ColorSlideFilm"></span><span id="colorslidefilm"></span><span id="COLORSLIDEFILM"></span>ColorSlideFilm</p></td>
<td><p>胶片图像处于正常颜色空间。</p></td>
</tr>
<tr class="odd">
<td><p><span id="ColorNegativeFilm"></span><span id="colornegativefilm"></span><span id="COLORNEGATIVEFILM"></span>ColorNegativeFilm</p></td>
<td><p>胶片图像是正常颜色空间的负片。</p></td>
</tr>
<tr class="even">
<td><p><span id="BlackandWhiteNegativeFilm"></span><span id="blackandwhitenegativefilm"></span><span id="BLACKANDWHITENEGATIVEFILM"></span>BlackandWhiteNegativeFilm</p></td>
<td><p>胶片图像是捕获的映像的黑色和白色负片。</p></td>
</tr>
</tbody>
</table>

 

## <a name="child-elements"></a>子元素


没有任何子元素。

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
<td><p><a href="filmscanmodessupported.md" data-raw-source="[&lt;strong&gt;FilmScanModesSupported&lt;/strong&gt;](filmscanmodessupported.md)"><strong>FilmScanModesSupported</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

可以扩展和子集化此元素的允许值。

## <a name="see-also"></a>请参阅


[**DefaultScanTicket**](defaultscanticket.md)

[**FilmScanModesSupported**](filmscanmodessupported.md)

 

 






