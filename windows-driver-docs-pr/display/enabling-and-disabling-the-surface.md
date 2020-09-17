---
title: 启用和禁用图面
description: 启用和禁用图面
ms.assetid: 34a1d1a5-b139-4d59-8754-b77d71bc75ad
keywords:
- 绘制 WDK GDI，初始化，启用和禁用图面
- 初始化图形驱动程序 WDK Windows 2000 显示、启用和禁用图面
- GDI WDK Windows 2000 显示、初始化、启用和禁用图面
- 图形驱动程序 WDK Windows 2000 显示、初始化、启用和禁用图面
- surface 初始化 WDK GDI
- surface 禁用 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca53f72bf1297daded8ccbc0737d9a2e5b20e5d6
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715194"
---
# <a name="enabling-and-disabling-the-surface"></a>启用和禁用图面


## <span id="ddk_enabling_and_disabling_the_surface_gg"></span><span id="DDK_ENABLING_AND_DISABLING_THE_SURFACE_GG"></span>


作为最后的初始化阶段，GDI 将调用 **DrvEnableSurface**。 *DrvEnableSurface* 必须通过调用相应的 GDI 服务来指定 surface 类型来创建它。 如 [GDI 支持](gdi-support-for-surfaces.md)中所述，根据设备和环境，驱动程序可以从 *DrvEnableSurface* 中调用相应的 GDI 服务来创建图面：

-   对于 *设备管理的图面*，驱动程序应调用 [**EngCreateDeviceSurface**](/windows/win32/api/winddi/nf-winddi-engcreatedevicesurface) 函数以获取图面的句柄。

-   若要创建 GDI 可以完全管理的标准格式 (*DIB*) 位图（包括所有绘图操作的性能），驱动程序应调用 **EngCreateBitmap** 驱动程序。

*DrvEnableSurface* 返回有效的 surface 控点作为返回值。

创建图面后，驱动程序必须通过调用 GDI 服务 [**EngAssociateSurface**](/windows/win32/api/winddi/nf-winddi-engassociatesurface)将该表面与 PDEV 相关联。 此调用还会告诉 GDI 驱动程序已为该表面挂钩哪些绘图函数。

GDI 将调用 [**DrvDisableSurface**](/windows/win32/api/winddi/nf-winddi-drvdisablesurface) 函数，以通知驱动程序已不再需要为 PDEV by *DrvEnableSurface* 创建的当前表面。 驱动程序必须分配在执行 *DrvEnableSurface*的过程中分配的任何内存和资源。 如果 PDEV 具有已启用的图面，则始终在[**DrvDisablePDEV**](/windows/win32/api/winddi/nf-winddi-drvdisablepdev)之前调用*DrvDisableSurface* 。

创建之后，必须在其不再使用时将其删除。 未能正确地将曲面创建与删除相匹配可能会导致对象被淘汰并降低系统性能。

 

