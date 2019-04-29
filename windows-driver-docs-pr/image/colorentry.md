---
title: ColorEntry 元素
description: 所需的 ColorEntry 元素描述上扫描程序的输入的源支持的单一颜色处理模式。
ms.assetid: a25c6da6-058e-4d10-895c-4507f0562ee8
keywords:
- ColorEntry 元素成像设备
topic_type:
- apiref
api_name:
- wscn ColorEntry
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 922af823ba1849dba65dc99846dbbe6493d16fea
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373190"
---
# <a name="colorentry-element"></a>ColorEntry 元素


所需**ColorEntry**元素描述上扫描程序的输入的源支持的单一颜色处理模式。

<a name="usage"></a>用法
-----

```xml
<wscn:ColorEntry>
  text
</wscn:ColorEntry>
```

<a name="attributes"></a>特性
----------

没有特性。

<a name="text-value"></a>文本值
----------

必需。 以下关键字之一：

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
<td><p><span id="BlackAndWhite1"></span><span id="blackandwhite1"></span><span id="BLACKANDWHITE1"></span>BlackAndWhite1</p></td>
<td><p>黑色和白色图像;1 位 / 像素 (bpp) 的一条通道</p></td>
</tr>
<tr class="even">
<td><p><span id="Grayscale4"></span><span id="grayscale4"></span><span id="GRAYSCALE4"></span>Grayscale4</p></td>
<td><p>灰度图像;4 个 bpp 和单个通道</p></td>
</tr>
<tr class="odd">
<td><p><span id="Grayscale8"></span><span id="grayscale8"></span><span id="GRAYSCALE8"></span>Grayscale8</p></td>
<td><p>灰度图像;8 bpp 和单个通道</p></td>
</tr>
<tr class="even">
<td><p><span id="Grayscale16"></span><span id="grayscale16"></span><span id="GRAYSCALE16"></span>Grayscale16</p></td>
<td><p>灰度图像;16 bpp 和单个通道</p></td>
</tr>
<tr class="odd">
<td><p><span id="RGB24"></span><span id="rgb24"></span>RGB24</p></td>
<td><p>RGB 编码彩色图像;24 bpp 分开存储的 8 位的三个通道</p></td>
</tr>
<tr class="even">
<td><p><span id="RGB48"></span><span id="rgb48"></span>RGB48</p></td>
<td><p>RGB 编码彩色图像;48 bpp 划分的 16 位的三个通道之间</p></td>
</tr>
<tr class="odd">
<td><p><span id="RGBa32"></span><span id="rgba32"></span><span id="RGBA32"></span>RGBa32</p></td>
<td><p>具有 alpha 通道; RGB 编码彩色图像32 位 bpp 分开存储的 8 位的四个通道</p></td>
</tr>
<tr class="even">
<td><p><span id="RGBa64"></span><span id="rgba64"></span><span id="RGBA64"></span>RGBa64</p></td>
<td><p>具有 alpha 通道; RGB 编码彩色图像64 bpp 划分的 16 位的四个通道之间</p></td>
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
<td><p><a href="adfcolor.md" data-raw-source="[&lt;strong&gt;ADFColor&lt;/strong&gt;](adfcolor.md)"><strong>ADFColor</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="filmcolor.md" data-raw-source="[&lt;strong&gt;FilmColor&lt;/strong&gt;](filmcolor.md)"><strong>FilmColor</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="platencolor.md" data-raw-source="[&lt;strong&gt;PlatenColor&lt;/strong&gt;](platencolor.md)"><strong>PlatenColor</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

每个值的关键字描述的颜色数据类型和编码，位深度和每个通道的位。 下表显示了如何将值关键字映射到处理属性的扫描程序的颜色。

| 关键字        | 像素位深度 | 每个通道的位 |
|----------------|-----------------|------------------|
| BlackAndWhite1 | 1               | 1                |
| Grayscale4     | 4               | {4}              |
| Grayscale8     | 8               | {8}              |
| Grayscale16    | 16              | {16}             |
| RGB24          | 24              | {8,8,8}          |
| RGB48          | 48              | {16,16,16}       |
| RGBa32         | 32              | {8,8,8,8}        |
| RGBa64         | 64              | {16,16,16,16}    |

 

您都可以扩展和子集的允许的值为此元素。

## <a name="see-also"></a>请参阅


[**ADFColor**](adfcolor.md)

[**FilmColor**](filmcolor.md)

[**PlatenColor**](platencolor.md)

 

 






