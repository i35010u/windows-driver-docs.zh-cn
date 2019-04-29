---
title: 管理显示调色板
description: 管理显示调色板
ms.assetid: a0ff1a9c-82dc-4317-a0ec-c387027a52ba
keywords:
- 显示驱动程序 WDK Windows 2000 中，调色板
- 显示颜色查找表 WDK Windows 2000
- 显示调色板 WDK Windows 2000
- 显示调色板 WDK Windows 2000
- 颜色索引 WDK Windows 2000 显示
- 可设置调色板 WDK Windows 2000 显示
- 显示索引的调色板 WDK Windows 2000
- RGB 颜色 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6bf6ad08d2da00edec66311c5428a3c5b89e750f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380401"
---
# <a name="managing-display-palettes"></a>管理显示调色板


## <span id="ddk_managing_display_palettes_gg"></span><span id="DDK_MANAGING_DISPLAY_PALETTES_GG"></span>


如果视频硬件支持可以设置的颜色，它维护一个名为颜色查找表*调色板*。 GDI 每个 RGB 值，并将其转换到设备*颜色索引*，以便它可以显示。 GDI 使用预先计算和缓存表的翻译。 这些表都可以访问驱动程序是作为用户对象[ **XLATEOBJ**](https://msdn.microsoft.com/library/windows/hardware/ff570634)。 因此，它接受源颜色，并将其移动到目标设备的每个 GDI 图形函数使用 XLATEOBJ 结构来转换颜色。 有关调色板和 GDI 如何处理它们的详细信息，请参阅[调色板的 GDI 支持](gdi-support-for-palettes.md)。

如果视频硬件支持可以设置的调色板，调用 GDI **DrvSetPalette**应用程序请求。 GDI 显示驱动程序和驱动程序查询到传递新的调色板**PALOBJ**。

*DrvSetPalette*函数提供的句柄*PDEV*向驱动程序，并请求驱动程序以实现设备的调色板。 该驱动程序应设置硬件调色板以尽可能接近地匹配给定调色板中的条目。

如果设备支持，可以设置，否则不应提供的调色板，则需要此入口点。 显示驱动程序指定其设备通过设置 GCAPS 具有可设置调色板\_PALMANAGED 位**flGraphicsCaps**字段[ **DEVINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff552835)结构中返回[ **DrvEnablePDEV**](https://msdn.microsoft.com/library/windows/hardware/ff556211)。

服务例程[ **PALOBJ\_cGetColors** ](https://msdn.microsoft.com/library/windows/hardware/ff568845)是可用于显示驱动程序。 此函数从索引面板中，下载 RGB 颜色，并应从调用的实现内*DrvSetPalette*。

 

 





