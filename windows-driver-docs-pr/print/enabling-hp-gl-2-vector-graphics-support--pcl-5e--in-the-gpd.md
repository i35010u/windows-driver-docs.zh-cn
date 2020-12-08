---
title: 在 GPD 中启用 HP-GL/2 矢量图形支持 (PCL-5e)
description: 在 GPD 中启用 HP-GL/2 矢量图形支持 (PCL-5e)
keywords:
- HP-GL/2 单色 WDK Unidrv，启用支持
- PCL-5e WDK Unidrv，支持支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ce1626815debfa51dd9a877c8d02c472314870b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797131"
---
# <a name="enabling-hp-gl2-vector-graphics-support-pcl-5e-in-the-gpd"></a>在 GPD 中启用 HP-GL/2 矢量图形支持 (PCL-5e)





若要在 Windows XP 上启用 HP-UX/2 向量支持，必须执行以下两项操作：

1.  将 " **\* 个性** 属性" 设置为 "个性 \_ HPGL2"。

2.  定义具有 HPGL2MODE 选项的 GraphicsMode 自定义功能。 若要同时提供光栅图形支持，请包含 RASTERMODE 选项。

可以通过以下方式设置 "个性" 属性：

```cpp
*Personality: =PERSONALITY_HPGL2
```

\_在 stdnames 中定义了个性 HPGL2 常量。

下面的 GPD 示例演示如何设置 " \* **个性**" 特性并使用矢量图形模式以及光栅图形模式定义 GraphicsMode 自定义功能。 请注意，整个块受 \* IFDEF GPD 编译器指令保护。

```cpp
*Ifdef: WINNT_51
*Personality: =PERSONALITY_HPGL2
*Feature: GraphicsMode
{
    *rcNameID: =GRAPHICSMODE_DISPLAY
    *FeatureType: DOC_PROPERTY
    *HelpIndex: 12000
    *DefaultOption: HPGL2MODE
    *Option: HPGL2MODE
    {
        *rcNameID: =GRAPHICSMODE_HPGL2_DISPLAY
    }
    *Option: RASTERMODE
    {
        *rcNameID: =GRAPHICSMODE_RASTER_DISPLAY
    }
}
*Endif:
```

\_以上指令中使用的 WINNT 51 参数适用于 Unidrv 的版本，而不是操作系统版本。 对于在 Windows 2000 上运行的 Windows XP Unidrv 打印机驱动程序，将 \_ 定义 WINNT 51 参数并编译块。 对于早期版本的 Unidrv，无论操作系统版本如何，此参数均未定义，并且不编译块。

彩色打印机的 GPD 文件还应定义 ColorMode 功能，如下面的泛型示例中所示。 请注意，打印机的特定详细信息可能需要更改某些值。

```cpp
*Feature: ColorMode
{
  *rcNameID: =COLOR_PRINTING_MODE_DISPLAY
  *HelpIndex: 12004
  *DefaultOption: 24bpp
  *Option: Mono
   {
     *rcNameID: =MONO_DISPLAY
     *DevNumOfPlanes: 1
     *DevBPP: 1
     *Color?: FALSE
     *Command: CmdSelect
      {
        *Order: PAGE_SETUP.16 
        *Cmd: "<1B>&b1M"
      }
   }
  *Option: 24bpp
   {
     *rcNameID: =24BPP_DISPLAY
     *DevNumOfPlanes: 1
     *DevBPP: 24
     *DrvBPP: 24
     *PaletteSize: 256
     *PaletteProgrammable?: TRUE
     *Command: CmdDefinePaletteEntry
      {
        *Cmd : "<1B>*v" %d{RedValue}"a"
+                       %d{GreenValue}"b"
+                       %d{BlueValue}"c"
+                       %d{PaletteIndexToProgram}"I"
 }
     *Command: CmdSelectPaletteEntry { *Cmd : "<1B>*v" 
+                        %d{CurrentPaletteIndex}"S" }
     *Command: CmdSetSrcBmpWidth { *Cmd : "<1B>*r" 
+                        %d{RasterDataWidthInBytes / 3}"S" }
     *Command: CmdSelect
      {
        *Order: PAGE_SETUP.16
        *Cmd: "<1B>*v1N<1B>*v1O<1B>*l184O<1B>*v6W<000308080808>
+              <1B>*v0a0b0c7i255a255b255c"
      }
   }
}
```

 

 




