---
title: 优化的纹理
description: 优化的纹理
keywords:
- 纹理管理 WDK Direct3D，优化纹理
- Direct3D WDK Windows 2000 显示，纹理管理
- 优化纹理 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0cd237f2e76d300f36ae22782f4743225bcd8ae4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837295"
---
# <a name="optimized-textures"></a>优化的纹理


## <span id="ddk_optimized_textures_gg"></span><span id="DDK_OPTIMIZED_TEXTURES_GG"></span>


为了提高性能，某些硬件供应商已从标准 Microsoft DirectDraw 表面格式更改了其纹理格式。 一种方法是将像素平铺，使其在内存中按引用的2D 位置排列。 例如，不是按如下所示扫描行来排列扫描行：

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>3</p></td>
<td align="left"><p>... <em>宽度</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><em>宽度</em>+ 1</p></td>
<td align="left"><p><em>宽度</em>+ 2</p></td>
<td align="left"><p><em>宽度</em>+ 3</p></td>
<td align="left"><p><em>宽度</em>+ 4</p></td>
<td align="left"><p>...</p></td>
</tr>
</tbody>
</table>

 

像素排列在 Dword 的4x8 块中：

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>3</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>5</p></td>
<td align="left"><p>6</p></td>
<td align="left"><p>7</p></td>
</tr>
</tbody>
</table>

 

因此，单个连续32字节的内存引用会拉入4x8 的像素块，以供光栅程序使用。 此布局更好地映射到通常由光栅化程序生成的内存引用模式，而不是标准 DirectDraw 布局。 此类方案称为 "swizzling" 或 "修补" 纹理。 这些操作的执行速度相对较快，而且不会影响分配的内存图面的大小。 但是，应用程序必须控制的此操作还引入了大量延迟。

另一种方法是将纹理压缩为视频内存，并将其解压缩到加速器上的本地缓存中。 这会减少保持光栅化以全速运行所需的视频内存带宽。 在 DirectX 5.0 中，驱动程序也可以执行此操作，但这是一项很慢的操作，它会影响应用程序的视频内存分配视图，因为生成的小纹理。

为适应硬件供应商，DirectX 6.0 和更高版本启用了 "优化" 的纹理，使驱动程序有机会在使用纹理时将表面转换为专用格式。 优化后，该表面将无法锁定，且可能更小或更大。

市场上很多3D 加速器芯片集都有一种专用格式，这种格式不能使用标准 DirectDraw 机制进行描述。 此功能旨在涵盖所有具有此类表面类型的硬件。

目前，应用程序有一些纹理需要经常更新，还有一些纹理在应用程序持续时间内保持不变。 由于增加了生成的填充率，因此从修补中获益。 " [优化的纹理 API](optimized-texture-api.md) " 部分中显示的标志允许应用程序将此使用方案指定给驱动程序，以便它能够相应地优化性能。

 

 





