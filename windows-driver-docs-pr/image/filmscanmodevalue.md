---
title: FilmScanModeValue 元素
description: 所需的 FilmScanModeValue 元素标识电影扫描选项支持的特定电影公开类型。
ms.assetid: 62d72190-f1c5-4b2f-af6a-a3c530cc51ed
keywords:
- FilmScanModeValue 元素成像设备
topic_type:
- apiref
api_name:
- wscn FilmScanModeValue
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9435d1dc06ef9147e22444d4479dfc9c4d110fa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358040"
---
# <a name="filmscanmodevalue-element"></a>FilmScanModeValue 元素


所需**FilmScanModeValue**元素标识电影扫描选项支持的特定电影公开类型。

<a name="usage"></a>用法
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
<td><p>默认扫描输入的源不再是电影胶片选项;因此，FilmScanModeValue 不再是 DefaultScanTicket 元素适用的值。 NotApplicable 是仅在 DefaultScanTicket 元素中有效。</p></td>
</tr>
<tr class="even">
<td><p><span id="ColorSlideFilm"></span><span id="colorslidefilm"></span><span id="COLORSLIDEFILM"></span>ColorSlideFilm</p></td>
<td><p>电影映像是普通的颜色空间中。</p></td>
</tr>
<tr class="odd">
<td><p><span id="ColorNegativeFilm"></span><span id="colornegativefilm"></span><span id="COLORNEGATIVEFILM"></span>ColorNegativeFilm</p></td>
<td><p>电影胶片图像是假负的正常颜色空间。</p></td>
</tr>
<tr class="even">
<td><p><span id="BlackandWhiteNegativeFilm"></span><span id="blackandwhitenegativefilm"></span><span id="BLACKANDWHITENEGATIVEFILM"></span>BlackandWhiteNegativeFilm</p></td>
<td><p>电影胶片图像是黑白假负的捕获的映像。</p></td>
</tr>
</tbody>
</table>

 

## <a name="child-elements"></a>子元素


没有子元素。

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

您都可以扩展和子集的允许的值为此元素。

## <a name="see-also"></a>请参阅


[**DefaultScanTicket**](defaultscanticket.md)

[**FilmScanModesSupported**](filmscanmodessupported.md)

 

 






