---
title: 使用压缩纹理图面
description: 使用压缩纹理图面
ms.assetid: efa7efff-a1ad-49f3-b6e8-f08b520e77ae
keywords:
- 绘制压缩纹理 WDK DirectDraw 有关压缩的纹理图面
- 显示 DirectDraw 压缩纹理 WDK Windows 2000，关于压缩的纹理图面
- 有关压缩的纹理图面压缩的纹理图面 WDK DirectDraw
- WDK DirectDraw，压缩的纹理的图面
- 纹理 WDK DirectDraw 压缩
- 参考光栅器 WDK DirectDraw
- 光栅器 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe7b8cbde8c87ef60cf4f369ff49daad3726bc87
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373569"
---
# <a name="using-compressed-texture-surfaces"></a>使用压缩纹理图面


## <span id="ddk_using_compressed_texture_surfaces_gg"></span><span id="DDK_USING_COMPRESSED_TEXTURE_SURFACES_GG"></span>


DirectDraw 仅调用驱动程序要执行的操作相同的 DXT 类型的两个图面之间 blt DDCAPS2\_中设置 COPYFOURCC 标志**dwCaps2**的成员[ **DDCORECAPS**](https://docs.microsoft.com/windows/desktop/api/ddrawi/ns-ddrawi-_ddcorecaps)结构。 如果未设置此标志，DirectDraw HEL 执行 blt。 这是备份图面显示复制 blts 重要，因为这是从备份 （系统内存） 图面以显示内存来下载纹理的机制。 因此，有效地公开 DXT 纹理图面需要您的驱动程序以支持 DDCAPS2\_COPYFOURCC 标志。

DDCAPS2\_COPYFOURCC 标志会影响某些其他。 您的驱动程序必须能够执行 blt FOURCC 格式具有至少包含这些属性之间：

-   源和目标格式是相同的 FOURCC 格式。

-   源和目标的图面是不同的。

-   源和目标矩形都构成整个图面 （即，没有任何拉伸和有无 subrectangles）。

-   这两个面是显示内存中。

-   该驱动程序必须能够为每个 FOURCC 格式，它支持显示内存中执行这些 blts。

**请注意**   Microsoft DirectShow 使用 DDCAPS2\_COPYFOURCC 标志，用于加速某些视频功能; 此标志要求意味着，可以复制所有 FOURCC 格式。

 

如果 blt 操作需要为 DXT 格式的压缩，DirectDraw HEL 始终执行 blt。 这意味着 DirectDraw 永远不请求要为其执行 blt 的驱动程序：

-   目标面具有 DXT 格式。

-   源和目标曲面的格式不相同。

DirectDraw DDCAPS 语义\_CANBLTSYSMEM 功能位表示为所有 blts 调用显示器驱动程序，从系统内存，无法显示内存。 因此，该驱动程序不能调用的此类 blts 从 DXT 图面到非 DXT 表面。 在这种情况下的唯一要求是驱动程序返回 DDHAL\_驱动程序\_NOTHANDLED 不能执行解压缩。 这将导致 DirectDraw 传播 DDERR\_到应用程序不受支持的错误代码。 可接受实现解压缩的 blts 从系统内存，无法显示内存中您的驱动程序，但这不是必需的 DirectX 6.0 及更高版本。

DirectDraw 显示内存分配例程不处理像素格式的注意事项。 [**HeapVidMemAllocAligned**](https://docs.microsoft.com/windows/desktop/api/dmemmgr/nf-dmemmgr-heapvidmemallocaligned)，例如，需要作为其输入参数的字节计数。 同样，DDHAL\_PLEASEALLOC\_BLOCKSIZE (请参阅**fpVidMem**的成员[ **DD\_面\_全局**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_surface_global)结构) 表示**dwBlockSizeX**并**dwBlockSizeY** DD 的成员\_图面\_全局结构不的字节数和行的计数分别。 因此，如果您的驱动程序使用这些机制之一来分配通过 DirectDraw 分配器的显示内存，您的驱动程序必须能够计算的内存消耗，以字节为单位，单独的 DXT 表面。 下面的示例显示了执行此计算的一种方法：

```cpp
DWORD dx, dy;
DWORD blksize, surfsize;
LPVOID pmem;

/*
 * Determine how much memory to allocate for the FOURCC format.
 */
switch ((int)pDDPF->dwFourCC)
{
  case MAKEFOURCC('D','X','T','1'):
    blksize = 8; // The size of a DXT1 4x4 pixel block. 
    break;
  case MAKEFOURCC('D','X','T','2'):    // premultiplied alpha
  case MAKEFOURCC('D','X','T','3'):    // non-premultiplied alpha
    blksize = 16; //The size of a DXT2,3 4x4 pixel block 
    break;
  case MAKEFOURCC('D','X','T','4'):    // premultiplied alpha
  case MAKEFOURCC('D','X','T','5'):    // non-premultiplied alpha
    blksize = 16; //The size of a DXT4,5 4x4 pixel block.
  break;

  default:
    DDASSERT(0);
}

/*
 * Calculate the number of blocks in the x and y dimensions.
 */
dx = (nWidth  + 3) >> 2;
dy = (nHeight + 3) >> 2;
surfsize = dx * dy * blksize;
```

当应用程序调用**IDirect3DVertexBuffer7::Lock**或**IDirectDrawSurface7::GetSurfaceDesc**方法 （在 Direct3D 和 DirectDraw SDK 文档集，分别介绍）该驱动程序必须在压缩的面上，设置 DDSD\_LINEARSIZE 标志**dwFlags**的成员[ **DDSURFACEDESC2** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550340(v=vs.85))结构。 此外，驱动程序必须设置分配包含中的图面上压缩的数据的字节数**dwLinearSize**相同的结构的成员。 ( **DwLinearSize**驻留在具有联合的成员**lPitch**成员，因此这些成员是互相排斥，因为是 DDSD\_LINEARSIZE 和 DDSD\_音调标记。)

你的硬件或驱动程序可以转换，并将压缩的纹理存储选择 （通常重新排序到硬件效率布局） 的任何格式。 但是，你的硬件或驱动程序必须能够将压缩的纹理转换回其原始 DXT 代码格式，只要 DirectDraw 需要它，也就是说，每当应用程序调用**IDirect3DVertexBuffer7::Lock**方法.

### <a name="span-idwindows2000notespanspan-idwindows2000notespanwindows-2000-note"></a><span id="windows_2000_note"></span><span id="WINDOWS_2000_NOTE"></span>Windows 2000 Note

在 Windows 2000 系统内存 DXT 图面已得到了一些内存分配用于映射及其字段。 映射为：

```cpp
wWidth = lPitch = dx * blksize;
wHeight         = dy;
dwRGBBitCount   = 8;
```

该驱动程序在遇到时系统内存 DXT 图面，例如在[ **D3dCreateSurfaceEx**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)，它必须返回之前进行的字段映射使用它们。 返回映射是：

```cpp
realWidth        = (wWidth  << 2) / blksize;
realHeight       =  wHeight << 2;
realLinearSize   = dwLinearSize * wHeight;
realRGBBitCount  = 0
```

### <a name="span-idreferencerasterizernotesspanspan-idreferencerasterizernotesspanreference-rasterizer-notes"></a><span id="reference_rasterizer_notes"></span><span id="REFERENCE_RASTERIZER_NOTES"></span>参考光栅器说明

实现参考光栅器 (RefRast) 代码时，应遵循以下三个项：

1.  标题部分*3 位线性 Alpha 内插 （DXT4 和 DXT5 格式）* DirectDraw SDK 文档显示了依据增加 DXT4 和 DXT5 格式的 Alpha 值的正确顺序。

2.  参考光栅器代码应具有以下逻辑防护颜色比较逻辑。
    ```cpp
    if ((color_0 > color_1) OR !DXT1) {
    /*  color comparison logic */
    }
    ```

3.  由于硬件实现的参考光栅器可以执行的计算，以更好地估计略有不同的方式的原始值舍入，测试应允许进行细微的变体中的颜色和 alpha 值来自解压缩逻辑。

 

 





