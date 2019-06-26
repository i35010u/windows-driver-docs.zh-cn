---
title: 管理调色板
description: 管理调色板
ms.assetid: 7917b01f-f57d-4262-80b6-9e11e797e3b5
keywords:
- GDI WDK Windows 2000 显示颜色
- 图形驱动程序 WDK Windows 2000 显示颜色
- 颜色管理 WDK GDI
- 显示调色板 WDK Windows 2000
- 绘制 WDK GDI，颜色
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4cdbd9a79ed9f292f798997d81c91441e323a21
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383432"
---
# <a name="managing-palettes"></a>管理调色板


## <span id="ddk_managing_palettes_gg"></span><span id="DDK_MANAGING_PALETTES_GG"></span>


中所述 GDI 支持的图形驱动程序管理工作。 该驱动程序必须提供到 GDI 中其默认调色板[ **DEVINFO** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-tagdevinfo)结构，当调用函数时 GDI [ **DrvEnablePDEV**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablepdev)。 在此期间，驱动程序应创建默认调色板对 GDI 服务函数的调用使用[ **EngCreatePalette**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatepalette)。

支持可设置调色板的驱动程序还必须支持[ **DrvSetPalette** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsetpalette)函数。 显示器驱动程序被以独占方式使用此函数。

 

 





