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
ms.openlocfilehash: ff45614ba2c715cb754b9491f8b918da57011758
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564752"
---
# <a name="managing-palettes"></a>管理调色板


## <span id="ddk_managing_palettes_gg"></span><span id="DDK_MANAGING_PALETTES_GG"></span>


中所述 GDI 支持的图形驱动程序管理工作。 该驱动程序必须提供到 GDI 中其默认调色板[ **DEVINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff552835)结构，当调用函数时 GDI [ **DrvEnablePDEV**](https://msdn.microsoft.com/library/windows/hardware/ff556211)。 在此期间，驱动程序应创建默认调色板对 GDI 服务函数的调用使用[ **EngCreatePalette**](https://msdn.microsoft.com/library/windows/hardware/ff564212)。

支持可设置调色板的驱动程序还必须支持[ **DrvSetPalette** ](https://msdn.microsoft.com/library/windows/hardware/ff556282)函数。 显示器驱动程序被以独占方式使用此函数。

 

 





