---
title: 图面协商
description: 图面协商
ms.assetid: af368be6-ea32-49ea-b49e-7e3c9a30facb
keywords:
- 图面协商 WDK GDI
- GDI WDK Windows 2000 显示，图面
- 图形驱动程序 WDK Windows 2000 显示，图面上协商
- 绘制 WDK GDI，图面上协商
- 协商 WDK GDI
- 有关图面上协商的图面上协商 WDK GDI，
- GDI WDK Windows 2000 显示位图
- 图形驱动程序 WDK Windows 2000 显示位图
- 绘制 WDK GDI，位图
- WDK GDI 位图
- 辅助图面 WDK GDI
- 屏外表面 WDK GDI
- 主图面 WDK GDI
- 屏幕上显示 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c22a73ee8b98e8dd06513499e10c36f9142f864
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564274"
---
# <a name="surface-negotiation"></a>图面协商


## <span id="ddk_surface_negotiation_gg"></span><span id="DDK_SURFACE_NEGOTIATION_GG"></span>


绘制和文本输出需要在其上绘制图面。 创建此面**DrvEnableSurface**尽管驱动程序可以支持多个 PDEVs。 支持的驱动程序[ **DrvCreateDeviceBitmap** ](https://msdn.microsoft.com/library/windows/hardware/ff556185)函数可以创建和使用其他的面。 这些位图图面嘿 *辅助图面*或*屏外表面*。 对于任一类型的图面，该驱动程序负责确定类型的绘制操作它支持。

 

 





