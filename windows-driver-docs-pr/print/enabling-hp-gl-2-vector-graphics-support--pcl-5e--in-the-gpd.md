---
title: 在 GPD 中启用 HP-GL/2 矢量图形支持 (PCL-5e)
description: 在 GPD 中启用 HP-GL/2 矢量图形支持 (PCL-5e)
ms.assetid: 2ca5a2fe-4c37-4b7f-bd9b-d41240f8843f
keywords:
- HP/2 单色 WDK Unidrv，从而启用支持
- PCL 5e WDK Unidrv，从而启用支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04530d80df3245667c5d904e0c741d4b5a453a8d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378643"
---
# <a name="enabling-hp-gl2-vector-graphics-support-pcl-5e-in-the-gpd"></a>在 GPD 中启用 HP-GL/2 矢量图形支持 (PCL-5e)





若要启用 Windows XP 上的 HP/2 向量支持，必须执行两项操作：

1.  设置**\*个性**归于个性\_HPGL2。

2.  定义具有 HPGL2MODE 选项的 GraphicsMode 自定义的功能。 若要提供光栅图形支持，包括 RASTERMODE 选项。

以这种方式，可以设置个人设置属性：

```cpp
*Personality: =PERSONALITY_HPGL2
```

个性\_HPGL2 常量 stdnames.gpd 中定义。

下面的 GPD 示例演示了如何设置\***个性**属性和定义与矢量图形模式中，以及光栅图形模式 GraphicsMode 自定义的功能。 请注意，整个块受\*Ifdef GPD 编译器指令。

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

WINNT\_51 上述指令中使用的参数适用于版本的 Unidrv，而不是操作系统版本。 Windows 2000，WINNT 上运行的 Windows XP Unidrv 打印机驱动程序\_51 参数定义和编译块。 对于早期 Unidrv 版本，无论何种操作系统版本，此参数是未定义，并且块将不进行编译。

彩色打印机 GPD 文件还应定义 ColorMode 功能，如下面的泛型示例中所示。 请注意，您的打印机的特定详细信息可能需要更改某些值。

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

 

 




