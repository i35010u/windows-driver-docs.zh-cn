---
title: 优化的纹理
description: 优化的纹理
ms.assetid: 2c1af9c0-f15a-426a-b861-09f3e1c8899e
keywords:
- 纹理管理 WDK Direct3D，优化纹理
- Direct3D WDK Windows 2000 显示，纹理管理
- 优化的纹理 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 673a90cce1884e6e1809fc45465f04cd638e472e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379849"
---
# <a name="optimized-textures"></a>优化的纹理


## <span id="ddk_optimized_textures_gg"></span><span id="DDK_OPTIMIZED_TEXTURES_GG"></span>


为了提高性能，有些硬件供应商已从标准的 Microsoft DirectDraw 图面上格式更改它们的纹理格式。 一种方法是磁贴的像素为单位，以便在内存中使用 2D 引用地址的排列。 例如，而不是排列像素扫描行扫描行如下：

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
<td align="left"><p>... <em>width</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><em>width</em>+1</p></td>
<td align="left"><p><em>width</em>+2</p></td>
<td align="left"><p><em>width</em>+3</p></td>
<td align="left"><p><em>width</em>+4</p></td>
<td align="left"><p>...</p></td>
</tr>
</tbody>
</table>

 

像素排列在 4 x 8 块的 dword 值：

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

 

因此，单个连续 32 字节的内存引用提取使用像素为单位的 4 x 8 块的光栅化程序。 此布局将映射到内存引用通常比标准 DirectDraw 布局由光栅化程序生成的模式要好得多。 此类方案称为 swizzling 或修补纹理。 这些操作是相对较执行，也不会影响内存图面的大小分配更快。 但是，没有大量所引入的应用程序必须控制此操作的延迟。

另一种方法是将纹理压缩成视频内存并将它解压缩到加速器上的本地缓存。 这将减少全速运行光栅化程序所需的视频内存带宽。 在 DirectX 5.0 中，驱动程序可以执行此操作，但很多慢影响由于生成较小的纹理的视频内存分配的应用程序的视图。

若要适应硬件供应商，DirectX 6.0 及更高版本，请启用使驱动程序可以在转换为专用格式的图面，使用纹理时的"优化"纹理。 一旦进行了优化，在图面不能被锁定，且可能会小于或大于原始。

市场上的多个三维 accelerator 芯片集具有专有格式，不能使用标准的 DirectDraw 机制所述。 此功能旨在涵盖所有硬件，但是此类图面类型。

当前应用程序具有必须经常，更新一些纹理和其他人可以在单独的应用程序的持续时间。 这些后一种受益于修补由于改进了生成的填充率。 中所示的标志[优化纹理 API](optimized-texture-api.md)部分允许应用程序指定驱动程序的这种用法中，以便它可以相应地优化性能。

 

 





