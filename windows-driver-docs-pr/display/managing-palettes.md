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
ms.openlocfilehash: a895a1723ba4dd01b88f6395a3a679354f9d029e
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715304"
---
# <a name="managing-palettes"></a>管理调色板


## <span id="ddk_managing_palettes_gg"></span><span id="DDK_MANAGING_PALETTES_GG"></span>


如 GDI 对图形驱动程序管理的支持工作中所述。 当 GDI 调用函数[**DrvEnablePDEV**](/windows/win32/api/winddi/nf-winddi-drvenablepdev)时，驱动程序必须将其默认调色板提供给[**lnk-devinfo**](/windows/win32/api/winddi/ns-winddi-tagdevinfo)结构中的 gdi。 此时，驱动程序应使用对 GDI 服务函数 [**EngCreatePalette**](/windows/win32/api/winddi/nf-winddi-engcreatepalette)的调用来创建默认调色板。

支持可设置调色板的驱动程序也必须支持 [**DrvSetPalette**](/windows/win32/api/winddi/nf-winddi-drvsetpalette) 函数。 此函数由显示驱动程序以独占方式使用。

 

