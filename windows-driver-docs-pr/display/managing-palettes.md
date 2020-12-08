---
title: 管理调色板
description: 管理调色板
keywords:
- GDI WDK Windows 2000 显示，颜色
- 图形驱动程序 WDK Windows 2000 显示，颜色
- 颜色管理 WDK GDI
- 调色板 WDK Windows 2000 显示
- 绘制 WDK GDI，颜色
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7137534189e2ff618cbe0b67b70d6e91fb5b4898
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793901"
---
# <a name="managing-palettes"></a>管理调色板

如 GDI 对图形驱动程序管理的支持工作中所述。 当 GDI 调用函数 [**DrvEnablePDEV**](/windows/win32/api/winddi/nf-winddi-drvenablepdev)时，驱动程序必须将其默认调色板提供给 [**lnk-devinfo**](/windows/win32/api/winddi/ns-winddi-devinfo)结构中的 gdi。 此时，驱动程序应使用对 GDI 服务函数 [**EngCreatePalette**](/windows/win32/api/winddi/nf-winddi-engcreatepalette)的调用来创建默认调色板。

如 [gdi 对图形驱动程序的支持](gdi-support-for-graphics-drivers.md)中所述，gdi 处理很多 *调色板* 管理工作。 当 GDI 调用函数 [**DrvEnablePDEV**](/windows/win32/api/winddi/nf-winddi-drvenablepdev)时，驱动程序必须将其默认调色板提供给 [**lnk-devinfo**](/windows/win32/api/winddi/ns-winddi-devinfo)结构中的 gdi。 此时，驱动程序应使用对 GDI 服务函数 [**EngCreatePalette**](/windows/win32/api/winddi/nf-winddi-engcreatepalette)的调用来创建默认调色板。

支持可设置调色板的驱动程序也必须支持 [**DrvSetPalette**](/windows/win32/api/winddi/nf-winddi-drvsetpalette) 函数。 此函数由显示驱动程序以独占方式使用。

 

