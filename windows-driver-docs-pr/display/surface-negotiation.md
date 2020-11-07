---
title: 图面协商
description: 图面协商
ms.assetid: af368be6-ea32-49ea-b49e-7e3c9a30facb
keywords:
- surface 协商 WDK GDI
- GDI WDK Windows 2000 显示，表面
- 图形驱动程序 WDK Windows 2000 显示，表面协商
- 绘制 WDK GDI，surface 协商
- 协商 WDK GDI
- surface 协商 WDK GDI，关于曲面协商
- GDI WDK Windows 2000 显示，位图
- 图形驱动程序 WDK Windows 2000 显示，位图
- 绘制 WDK GDI，位图
- 位图 WDK GDI
- 辅助面
- 离屏表面 WDK GDI
- 主要表面 WDK GDI
- 屏幕面上的 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6b45d8150c3a2709197ba3a6f724770cc4e18e4
ms.sourcegitcommit: a44ade167cdfb541cf1818e9f9e3726f23f90b66
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2020
ms.locfileid: "94361537"
---
# <a name="surface-negotiation"></a>图面协商


## <span id="ddk_surface_negotiation_gg"></span><span id="DDK_SURFACE_NEGOTIATION_GG"></span>


绘图和文本输出都需要一个要在其上绘制的图面。 此图面由 [**DrvEnableSurface**](/windows/win32/api/winddi/nf-winddi-drvenablesurface) 函数创建，被称为 *主表面* 。 此表面也称为 *屏幕图面* ，因为它显示在视频显示中。 尽管驱动程序可以支持多个 PDEVs，但每个 *PDEV* 仅启用了一个主表面。 支持 [**DrvCreateDeviceBitmap**](/windows/win32/api/winddi/nf-winddi-drvcreatedevicebitmap) 函数的驱动程序可以创建和使用其他表面。 这些位图图面称为 " *辅助* " 或 " *屏外" 表面* 。 对于这两种类型的图面，驱动程序负责确定它支持的绘图操作的类型。

