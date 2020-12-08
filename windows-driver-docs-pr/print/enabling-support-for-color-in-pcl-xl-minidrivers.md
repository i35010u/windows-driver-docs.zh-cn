---
title: 启用对 PCL XL 微型驱动程序中的颜色的支持
description: 启用对 PCL XL 微型驱动程序中的颜色的支持
keywords:
- PCL XL 矢量图形 WDK Unidrv，启用颜色支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9558aea5f0ba53bf647051746c2ca549ab7d4c01
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797129"
---
#  <a name="enabling-support-for-color-in-pcl-xl-minidrivers"></a>启用对 PCL XL 微型驱动程序中的颜色的支持





为彩色 PCL XL 开发 GPD 文件类似于为单色 PCL XL 开发 GPD 文件。 本主题中介绍了主要区别。 此处提供的示例 GPD 条目可能需要针对你的设备进行相应修改。

-   GPD 文件必须指定设备为彩色。

    也就是说，GPD 文件必须包含 ColorMode [标准功能](standard-features.md)。 请注意，PCL XL 的当前实现仅支持24位/像素的颜色。 下面的示例演示具有两个选项项的 ColorMode 功能 \* ： Mono 和24bpp 颜色。

```cpp
*Feature: ColorMode
{
    *rcNameID: =COLOR_PRINTING_MODE_DISPLAY
    *DefaultOption: 24bpp
    *Option: Mono
    {
        *rcNameID: =MONO_DISPLAY
        *DevNumOfPlanes: 1
        *DevBPP: 24
        *DrvBPP: 24
        *Color? : FALSE
        *PaletteSize: 1
        *PaletteProgrammable? : TRUE
        *Command: CmdDefinePaletteEntry { *Cmd: "" }
    }
    *Option: 24bpp
    {
        *rcNameID: =24BPP_DISPLAY
        *DevNumOfPlanes: 1
        *DevBPP: 24
        *DrvBPP: 24
        *PaletteSize: 256
        *PaletteProgrammable? : TRUE
        *Command: CmdDefinePaletteEntry { *Cmd: "" }
    }
}
```

-   有些命令可能需要更改以进行彩色打印。

    例如，如果 GPD 文件允许用户在打印颜色和单色 (之间进行选择，如前面的示例) 中所示，"页面设置" 命令将取决于用户是以单色打印还是以彩色打印。 在这种情况下， **CmdStartPage** 命令 (请参阅 [打印机配置命令](printer-configuration-commands.md)) 必须置于 \* Switch： ColorMode 语句内，如以下示例中所示。  (请注意， \* Order： PAGE \_ SETUP. 4 命令属性中的数字4可能需要修改，具体取决于 GPD 文件和设备。 ) 有关页面设置语法的详细信息 \_ ，请参阅 [命令执行顺序](command-execution-order.md)。

```cpp
*Switch: ColorMode
{
  *Case: Mono
  {
    *Command: CmdStartPage
    {
    *Order: PAGE_SETUP.4
    *Cmd: =real32_xy "<0000803f><0000803f>" =attr_ubyte =PageScale =SetPageScale
+         =ubyte =eGray =attr_ubyte =ColorSpace =SetColorSpace
    }
  }
  *Case: 24bpp
  {
    *Command: CmdStartPage
    {
    *Order: PAGE_SETUP.4
    *Cmd: =real32_xy "<0000803f><0000803f>" =attr_ubyte =PageScale =SetPageScale
+         =ubyte =eRGB =attr_ubyte =ColorSpace =SetColorSpace
    }
  }
}
```

-   可能需要删除或修改 GPD 中用于单色设备的某些命令或信息。

    例如，如果您修改 p6sample GPD 文件以添加颜色信息，则您可能希望删除该 \* 功能：仿色 [自定义功能](customized-features.md) 或对其进行限制，使其仅在单色模式下打印时使用。

 

 




