---
title: 使用压缩纹理图面
description: 使用压缩纹理图面
ms.assetid: efa7efff-a1ad-49f3-b6e8-f08b520e77ae
keywords:
- 绘制压缩纹理 WDK DirectDraw，关于压缩纹理图面
- DirectDraw 压缩纹理 WDK Windows 2000 显示，关于压缩纹理图面
- 压缩纹理面 WDK DirectDraw，关于压缩纹理图面
- 表面 WDK DirectDraw，压缩纹理
- 纹理 WDK DirectDraw，压缩
- 引用 rasterizers WDK DirectDraw
- rasterizers WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56b5723d57cb4f612b22f3becc659c9841d5ba32
ms.sourcegitcommit: f8619f20a0903dd64f8641a5266ecad6df5f1d57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/29/2020
ms.locfileid: "91423494"
---
# <a name="using-compressed-texture-surfaces"></a>使用压缩纹理图面


## <span id="ddk_using_compressed_texture_surfaces_gg"></span><span id="DDK_USING_COMPRESSED_TEXTURE_SURFACES_GG"></span>


如果在 \_ [**dwCaps2**](/windows/win32/api/ddrawi/ns-ddrawi-ddcorecaps)结构的**DDCORECAPS**成员中设置 DDCAPS2 COPYFOURCC 标志，则 DirectDraw 仅调用驱动程序在同一 DXT 类型的两个表面之间执行 blt。 如果未设置此标志，则 DirectDraw HEL 将执行 blt。 这对于实现表面到显示复制 blts 非常重要，因为这是一种机制，通过该机制，可以从 (系统内存) 表面下载纹理以显示内存。 因此，公开 DXT 纹理图面的实际要求您的驱动程序支持 DDCAPS2 \_ COPYFOURCC 标志。

DDCAPS2 \_ COPYFOURCC 标志有一些其他含义。 你的驱动程序必须能够在 FOURCC 格式之间执行至少具有以下属性的 blt：

-   源和目标格式是相同的 FOURCC 格式。

-   源和目标面不同。

-   源和目标矩形都构成了整个表面 (也就是说，没有拉伸，也没有 subrectangles) 。

-   这两个图面都在显示内存中。

-   驱动程序必须能够在显示内存中为其支持的每个 FOURCC 格式执行这些 blts。

**注意**   Microsoft DirectShow 使用 DDCAPS2 \_ COPYFOURCC 标志来加速某些视频功能; 此标志的要求表示可以复制所有 FOURCC 格式。

 

如果 blt 操作要求压缩为 DXT 格式，则 DirectDraw HEL 始终执行 blt。 这意味着 DirectDraw 从不请求驱动程序执行以下操作的 blt：

-   目标图面的格式为 DXT。

-   源和目标曲面的格式不相同。

DirectDraw DDCAPS \_ CANBLTSYSMEM 功能位的语义意味着从系统内存中的所有 blts 调用显示驱动程序以显示内存。 因此，可以将此类 blts 的驱动程序从 DXT 表面调用到非 DXT 图面。 在这种情况下，唯一的要求是驱动程序返回 DDHAL \_ driver \_ NOTHANDLED （如果它无法执行解压缩）。 这会导致 DirectDraw 将 \_ 不支持的 DDERR 错误代码传播到应用程序。 可以从系统内存中实现 blts 的解压缩，以显示驱动程序中的内存，但这对于 DirectX 6.0 和更高版本不是必需的。

DirectDraw 显示内存分配例程不处理像素格式注意事项。 例如， [**HeapVidMemAllocAligned**](/windows/win32/api/dmemmgr/nf-dmemmgr-heapvidmemallocaligned)需要字节计数作为其输入参数。 同样，DDHAL \_ PLEASEALLOC \_ 块 (查看[**dd \_ Surface \_ 全局**](/windows/win32/api/ddrawint/ns-ddrawint-dd_surface_global)结构的**fpVidMem**成员) 表示 dd surface global 结构的**dwBlockSizeX**和**dwBlockSizeY**成员分别为 \_ \_ 字节和行计数。 因此，如果您的驱动程序使用这两种机制来通过 DirectDraw 分配器分配显示内存，则您的驱动程序必须能够自行计算 DXT 的内存消耗量（以字节为单位）。 下面的示例演示了执行此计算的一种方法：

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

当应用程序调用 Direct3D 和 DirectDraw SDK 文档) 集中 (中所述的**IDirect3DVertexBuffer7：： Lock**或**IDirectDrawSurface7：： GetSurfaceDesc**方法时，该驱动程序必须 \_ 在[**LINEARSIZE**](/previous-versions/windows/hardware/drivers/ff550340(v=vs.85))结构的**dwFlags**成员中设置 DDSD DDSURFACEDESC2 标志。 此外，驱动程序必须将分配的字节数设置为包含同一结构的 **dwLinearSize** 成员中的压缩的图面数据。  (**dwLinearSize** 成员位于具有 **lPitch** 成员的联合中，因此这些成员是互相排斥的，如 DDSD \_ LINEARSIZE 和 DDSD \_ 螺距标志。 ) 

你的硬件或驱动程序可以采用你选择的任何格式来转换和存储压缩纹理 (通常会将其重新排序为更具硬件效率的布局) 。 但是，无论何时，如果应用程序调用 **IDirect3DVertexBuffer7：： Lock** 方法，你的硬件或驱动程序都必须能够将压缩纹理转换回其原始 DXT 代码格式。

### <a name="span-idwindows_2000_notespanspan-idwindows_2000_notespanwindows-2000-note"></a><span id="windows_2000_note"></span><span id="WINDOWS_2000_NOTE"></span>Windows 2000 说明

在 Windows 2000 下，系统内存 DXT 表面已为内存分配目的映射了一些字段。 映射为：

```cpp
wWidth = lPitch = dx * blksize;
wHeight         = dy;
dwRGBBitCount   = 8;
```

当驱动程序遇到系统内存 DXT 表面（例如在 [**D3dCreateSurfaceEx**](/windows/win32/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)中）时，必须先将这些字段映射回来，然后才能使用这些字段。 反向映射为：

```cpp
realWidth        = (wWidth  << 2) / blksize;
realHeight       =  wHeight << 2;
realLinearSize   = dwLinearSize * wHeight;
realRGBBitCount  = 0
```

### <a name="span-idreference_rasterizer_notesspanspan-idreference_rasterizer_notesspanreference-rasterizer-notes"></a><span id="reference_rasterizer_notes"></span><span id="REFERENCE_RASTERIZER_NOTES"></span>参考光栅化说明

 (RefRast) 代码时，应遵循以下三个项目：

1.  DirectDraw SDK 文档中 * (DXT4 和 DXT5) 格式的第三位线性 Alpha 插值 * 部分显示了为 DXT4 和 DXT5 格式增加 Alpha 值的正确顺序。

2.  引用光栅化代码应有以下逻辑来保护颜色比较逻辑。
    ```cpp
    if ((color_0 > color_1) OR !DXT1) {
    /*  color comparison logic */
    }
    ```

3.  由于引用 rasterizers 的硬件实现可以对计算进行舍入，从而以略微不同的方式更好地估计原始值，因此测试应允许从解压缩逻辑获得的颜色和 alpha 值中稍微变大。

 

