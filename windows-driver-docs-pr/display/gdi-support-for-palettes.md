---
title: 调色板的 GDI 支持
description: 调色板的 GDI 支持
keywords:
- DrvEnablePDEV
- GDI WDK Windows 2000 显示，颜色
- 图形驱动程序 WDK Windows 2000 显示，颜色
- 颜色管理 WDK GDI
- 调色板 WDK Windows 2000 显示
- 绘制 WDK GDI，颜色
- DrvSetPalette
- 颜色索引 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37168bfe108ead2e46656b81a371e5831c3b7a3c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819147"
---
# <a name="gdi-support-for-palettes"></a>调色板的 GDI 支持

GDI 可以完成与调色板管理有关的大部分工作。 当 GDI 调用 [**DrvEnablePDEV**](/windows/win32/api/winddi/nf-winddi-drvenablepdev) 函数时，驱动程序会将其默认调色板作为 [**lnk-devinfo**](/windows/win32/api/winddi/ns-winddi-devinfo) 结构的一部分返回到 GDI。 驱动程序必须使用 [**EngCreatePalette**](/windows/win32/api/winddi/nf-winddi-engcreatepalette) 函数创建此调色板。

调色板有效地将32位 *颜色索引* 映射为24位 RGB 颜色值，这是 GDI 使用调色板的方式。 驱动程序指定其调色板，以便 GDI 可以确定不同的颜色索引在设备上的显示方式。

驱动程序无需处理大多数调色板操作和计算，只要它使用 GDI 提供的 [**XLATEOBJ**](/windows/win32/api/winddi/ns-winddi-xlateobj) 。

如果设备支持可修改的调色板，则它应实现函数 [**DrvSetPalette**](/windows/win32/api/winddi/nf-winddi-drvsetpalette)。 当应用程序更改设备的调色板并将生成的新调色板传递到驱动程序时，GDI 将调用 *DrvSetPalette* 。 驱动程序应设置其内部硬件调色板，使其尽可能与新调色板匹配。

可以使用下表中列出的两种不同格式之一为 GDI 定义调色板。

| 调色板格式 | 描述 |
| -------------- | ----------- |
| 已编制索引        | 颜色索引是 RGB 值数组的索引。 数组可以很小，例如16色索引或大，其中包含4096颜色索引或更多。 |
| 位域     | 颜色索引中的位域在每种颜色的 R、G 和 B 的数量方面指定颜色。 例如，5位可用于每个，并为每种颜色提供一个介于0到31之间的值。 转换为 RGB 时，5位值会向上扩展，以涵盖每个组件的范围为0到255。  (通常由位域定义的 RGB 表示形式本身。 )  |

GDI 通常会反向使用调色板映射。 也就是说，应用程序为绘图和 GDI 指定 RGB 颜色必须找到导致设备显示该颜色的颜色索引。 正如下表中所示，GDI 提供了两个主要的调色板服务函数用于创建和删除调色板，还提供了一些与 [**PALOBJ**](/windows/win32/api/winddi/ns-winddi-palobj) 和 [**XLATEOBJ**](/windows/win32/api/winddi/ns-winddi-xlateobj) 相关的服务功能，用于在两个调色板之间转换颜色索引。

| 函数 | 描述 |
| -------- | ----------- |
| [**EngCreatePalette**](/windows/win32/api/winddi/nf-winddi-engcreatepalette) | 创建调色板。 驱动程序通过在 [**lnk-devinfo**](/windows/win32/api/winddi/ns-winddi-devinfo) 结构中返回调色板的句柄，将调色板与设备相关联。 |
| [**EngDeletePalette**](/windows/win32/api/winddi/nf-winddi-engdeletepalette) | 删除给定的调色板。 |
| [**EngDitherColor**](/windows/win32/api/winddi/nf-winddi-engdithercolor) | 返回近似于指定 RGB 颜色的标准8x8 仿色。 |
| [**EngQueryPalette**](/windows/win32/api/winddi/nf-winddi-engquerypalette) | 在调色板中查询其特性。 |
| [**PALOBJ_cGetColors**](/windows/win32/api/winddi/nf-winddi-palobj_cgetcolors) | 允许驱动程序从索引调色板下载 RGB 颜色。 由 [**DrvSetPalette**](/windows/win32/api/winddi/nf-winddi-drvsetpalette) 函数中的显示驱动程序调用。 |
| [**XLATEOBJ_cGetPalette**](/windows/win32/api/winddi/nf-winddi-xlateobj_cgetpalette) | 检索索引源调色板中颜色的24位 RGB 颜色或位域格式。 驱动程序可以使用此函数从调色板获取信息以执行颜色混合。 |
| [**XLATEOBJ_hGetColorTransform**](/windows/win32/api/winddi/nf-winddi-xlateobj_hgetcolortransform) | 返回指定的翻译对象的颜色转换。 |
| [**XLATEOBJ_iXlate**](/windows/win32/api/winddi/nf-winddi-xlateobj_ixlate) | 将单个源颜色索引转换为目标颜色索引。 |
[**XLATEOBJ_piVector**](/windows/win32/api/winddi/nf-winddi-xlateobj_pivector) | 从索引源调色板中检索转换向量。 驱动程序可以使用此向量执行其自己的源索引到目标索引的翻译。 |
