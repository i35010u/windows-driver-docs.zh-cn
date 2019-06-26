---
title: 启用和禁用图面
description: 启用和禁用图面
ms.assetid: 34a1d1a5-b139-4d59-8754-b77d71bc75ad
keywords:
- 绘制 WDK GDI，初始化、 启用和禁用图面
- 正在初始化图形驱动程序 WDK Windows 2000 显示，请启用和禁用图面
- GDI WDK Windows 2000 显示、 初始化、 启用和禁用图面
- 显示图形驱动程序 WDK Windows 2000，初始化、 启用和禁用图面
- 图面上初始化 WDK GDI
- 禁用 WDK GDI 的图面
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9bd90d1375f2579ead8676d487861daeec5f1321
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355577"
---
# <a name="enabling-and-disabling-the-surface"></a>启用和禁用图面


## <span id="ddk_enabling_and_disabling_the_surface_gg"></span><span id="DDK_ENABLING_AND_DISABLING_THE_SURFACE_GG"></span>


作为最终初始化阶段中，调用 GDI **DrvEnableSurface**。 *DrvEnableSurface*必须通过调用适当的 GDI 服务，以创建该指定的图面类型。 如中所述[GDI 支持对于图面](gdi-support-for-surfaces.md)，并根据设备和情况下，驱动程序可以调用适当的 GDI 服务内*DrvEnableSurface*创建设计面的：

-   有关*设备管理面*，该驱动程序应调用[ **EngCreateDeviceSurface** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatedevicesurface)函数来获取面的的句柄。

-   若要创建标准格式 (*DIB*) 位图，GDI 可以管理完全，包括所有绘制操作的性能，该驱动程序应调用**EngCreateBitmap**驱动程序。

*DrvEnableSurface*返回有效的图面上句柄作为返回值。

以下一项外围应用的创建、 驱动程序必须与相关联的图面 PDEV 通过调用 GDI 服务[ **EngAssociateSurface**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engassociatesurface)。 此调用还指出的 GDI 哪一个绘图函数驱动程序已挂钩的该图面。

GDI 调用[ **DrvDisableSurface** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablesurface)函数来通知当前面为 PDEV 由创建的驱动程序*DrvEnableSurface*不再需要。 该驱动程序必须解除分配任何内存和资源分配的执行期间*DrvEnableSurface*。 *DrvDisableSurface*之前，始终调用[ **DrvDisablePDEV**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisablepdev)，如果 PDEV 具有一个已启用的图面。

创建后，不再使用时，必须删除图面。 未能正确匹配图面上的创建与删除操作可能导致孤立对象地累积并降低系统性能。

 

 





