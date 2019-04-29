---
title: 管理和优化字体
description: 管理和优化字体
ms.assetid: 5cfc2174-c605-4399-97a6-62f51df21c16
keywords:
- 字体 WDK 图形管理和优化
- GDI WDK Windows 2000 显示、 字体、 管理和优化
- 显示图形驱动程序 WDK Windows 2000，字体，管理和优化
- 生成者 WDK 图形
- 使用者 WDK GDI
- WDK 图形的标志符号信息
- GDI WDK Windows 2000 显示、 文本输出，管理和优化
- 显示图形驱动程序 WDK Windows 2000，文本输出，管理和优化字体
- 绘制 WDK GDI，字体、 管理和优化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58ba536fe67dddf0d32c34adb166744fa70aeb82
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380407"
---
# <a name="managing-and-optimizing-fonts"></a>管理和优化字体


## <span id="ddk_managing_and_optimizing_fonts_gg"></span><span id="DDK_MANAGING_AND_OPTIMIZING_FONTS_GG"></span>


一个*制造者*是可以生成字体的驱动程序。 它将生成输出，包括标志符号度量值、 位图和轮廓的标志符号信息。 一个*使用者*是使用字体的驱动程序。 它接受标志符号信息作为输入用于生成文本输出，并必须绘制其自己的字体或硬件的设备管理的图面上。 驱动程序可以生成者和使用者。 例如，打印机驱动程序可以充当生成者时维护[ **DrvQueryFontData** ](https://msdn.microsoft.com/library/windows/hardware/ff556264)调用，以作为处理时的使用者提供字形度量值和更高版本的 act [ **DrvTextOut** ](https://msdn.microsoft.com/library/windows/hardware/ff557277)调用。

驱动程序需要它时字体生成者或字体使用者处理字体。 如果硬件具有常驻字体，驱动程序必须提供到 GDI 此字体，包括中的字体指标有关的信息[ **IFIMETRICS** ](https://msdn.microsoft.com/library/windows/hardware/ff567418)结构，从 Unicode 到单个标志符号的映射标识、 单个标志符号属性和字距调整表。 也有该驱动程序必须支持的函数。 某些函数所需字体驱动程序和驱动程序使用特定于驱动程序或特定于设备的字体。 其他人只需要字体驱动程序。

字体函数的支持取决于驱动程序的功能。 常规类型包括：

[度量值的函数](font-metric-functions.md)

[标志符号函数](font-driver-functions.md)

[TrueType 函数](truetype-font-driver-functions.md)

 

 





