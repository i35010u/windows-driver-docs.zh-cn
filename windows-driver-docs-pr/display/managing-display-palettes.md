---
title: 管理显示调色板
description: 管理显示调色板
ms.assetid: a0ff1a9c-82dc-4317-a0ec-c387027a52ba
keywords:
- 显示驱动程序 WDK Windows 2000，调色板
- 颜色查找表 WDK Windows 2000 显示
- 调色板 WDK Windows 2000 显示
- 调色板 WDK Windows 2000 显示
- 颜色索引 WDK Windows 2000 显示
- 可设置调色板 WDK Windows 2000 显示
- 索引调色板 WDK Windows 2000 显示
- RGB 颜色 WDK Windows 2000 显示
ms.date: 10/11/2019
ms.localizationpriority: medium
ms.openlocfilehash: 391c70be7d828f2d5db4c2dfaed9c14f3b0b2817
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715308"
---
# <a name="managing-display-palettes"></a>管理显示调色板

如果视频硬件支持可设置的颜色，它会保留名为 *调色板*的颜色查找表。 GDI 采用每个 RGB 值，并将其转换为设备 *颜色索引* ，以便能够显示。 GDI 使用预先计算的和缓存的表进行翻译。 这些表可作为用户对象 [*XLATEOBJ*](/windows/win32/api/winddi/ns-winddi-xlateobj)的驱动程序来访问。 因此，采用源颜色并将其移动到目标设备的每个 GDI 图形函数都使用 XLATEOBJ 结构来转换颜色。 有关调色板以及 GDI 如何处理它们的详细信息，请参阅 [调色板的 Gdi 支持](gdi-support-for-palettes.md)。

如果视频硬件支持可设置的调色板，则 GDI 将调用应用程序请求的 [**DrvSetPalette**](/windows/win32/api/winddi/nf-winddi-drvsetpalette) 。 GDI 将新调色板传递到显示驱动程序，驱动程序将查询 [PALOBJ](/windows/win32/api/winddi/ns-winddi-palobj)。

**DrvSetPalette**函数向驱动程序提供*PDEV*的句柄，并请求驱动程序实现该设备的调色板。 驱动程序应设置硬件调色板，使其与给定调色板中的条目尽可能匹配。

如果设备支持可以设置的调色板，则此入口点是必需的，否则不应提供此入口点。 显示驱动程序通过在 \_ [**DrvEnablePDEV**](/windows/win32/api/winddi/nf-winddi-drvenablepdev)中返回的[lnk-devinfo](/windows/win32/api/winddi/ns-winddi-devinfo)结构的**flGraphicsCaps**字段中设置 GCAPS PALMANAGED 位，来指定其设备具有可设置的调色板。

服务例程 [PALOBJ_cGetColors](/windows/win32/api/winddi/nf-winddi-palobj_cgetcolors) 可用于显示驱动程序。 此函数从索引调色板下载 RGB 颜色，应从 *DrvSetPalette*的实现中调用。