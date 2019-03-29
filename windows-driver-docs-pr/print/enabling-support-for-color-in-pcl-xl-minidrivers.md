---
title: 启用对 PCL XL 微型驱动程序中的颜色的支持
description: 启用对 PCL XL 微型驱动程序中的颜色的支持
ms.assetid: 3287b070-76e3-4a28-a516-aa58905af224
keywords:
- PCL XL 矢量图形 WDK Unidrv，从而启用颜色的支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6310152a031f798dcec7035d6a5e759a3fee3c98
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562149"
---
#  <a name="enabling-support-for-color-in-pcl-xl-minidrivers"></a>启用对 PCL XL 微型驱动程序中的颜色的支持





开发颜色 PCL XL GPD 文件将类似于开发单色 PCL XL GPD 文件。 本主题所述的主要区别。 此处介绍的示例 GPD 条目可能需要针对你的设备进行适当地修改。

-   GPD 文件必须指定设备为颜色。

    也就是说，GPD 文件必须包含 ColorMode[标准功能](standard-features.md)。 请注意，PCL XL 的当前实现支持仅每像素 24 位的颜色。 下面的示例演示具有两个的 ColorMode 功能\*选项条目：Mono 和 24bpp 颜色。

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

-   某些命令可能需要更改对于彩色打印。

    例如，如果 GPD 文件允许用户打印颜色和单色 （如在前面的示例） 之间进行选择，页面设置命令将依赖于用户是否打印单色或颜色。 在这种情况下**CmdStartPage**命令 (请参阅[打印机配置命令](printer-configuration-commands.md)) 必须放在\*开关：ColorMode 语句，如以下示例所示。 (请注意，在数字 4\*顺序：页上\_SETUP.4 命令特性可能需要进行修改，具体取决于 GPD 文件和设备。)有关页的详细信息\_安装程序的语法，请参阅[命令执行顺序](command-execution-order.md)。

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

-   某些命令或单色设备满足你 GPD 中的信息可能需要删除或修改。

    例如，如果修改 p6sample.gpd 示例 GPD 文件以添加颜色信息时，你可能想要删除\*功能：抖动[自定义的功能](customized-features.md)或将其约束，以便仅当打印单色模式下时使用它。

 

 




