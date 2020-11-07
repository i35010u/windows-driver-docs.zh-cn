---
title: 管理调色板
description: 管理调色板
ms.assetid: 7917b01f-f57d-4262-80b6-9e11e797e3b5
keywords:
- GDI WDK Windows 2000 显示，颜色
- 图形驱动程序 WDK Windows 2000 显示，颜色
- 颜色管理 WDK GDI
- 调色板 WDK Windows 2000 显示
- 绘制 WDK GDI，颜色
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb60d44d7add782c52857372dc1c370b8c7cef6c
ms.sourcegitcommit: a44ade167cdfb541cf1818e9f9e3726f23f90b66
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2020
ms.locfileid: "94361397"
---
# <a name="managing-palettes"></a>管理调色板

如 GDI 对图形驱动程序管理的支持工作中所述。 当 GDI 调用函数 [**DrvEnablePDEV**](/windows/win32/api/winddi/nf-winddi-drvenablepdev)时，驱动程序必须将其默认调色板提供给 [**lnk-devinfo**](/windows/win32/api/winddi/ns-winddi-devinfo)结构中的 gdi。 此时，驱动程序应使用对 GDI 服务函数 [**EngCreatePalette**](/windows/win32/api/winddi/nf-winddi-engcreatepalette)的调用来创建默认调色板。

如 [gdi 对图形驱动程序的支持](gdi-support-for-graphics-drivers.md)中所述，gdi 处理很多 *调色板* 管理工作。 当 GDI 调用函数 [**DrvEnablePDEV**](/windows/win32/api/winddi/nf-winddi-drvenablepdev)时，驱动程序必须将其默认调色板提供给 [**lnk-devinfo**](/windows/win32/api/winddi/ns-winddi-devinfo)结构中的 gdi。 此时，驱动程序应使用对 GDI 服务函数 [**EngCreatePalette**](/windows/win32/api/winddi/nf-winddi-engcreatepalette)的调用来创建默认调色板。

支持可设置调色板的驱动程序也必须支持 [**DrvSetPalette**](/windows/win32/api/winddi/nf-winddi-drvsetpalette) 函数。 此函数由显示驱动程序以独占方式使用。

 

