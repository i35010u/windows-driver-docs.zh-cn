---
title: 丢失和还原 DirectDraw 图面
description: 丢失和还原 DirectDraw 图面
keywords:
- 绘图图面 WDK DirectDraw，丢失
- DirectDraw 表面，WDK Windows 2000 显示，丢失
- 平面 DirectDraw，丢失
- 绘图图面 WDK DirectDraw，还原
- DirectDraw 图面，WDK Windows 2000 显示，还原
- surface DirectDraw，还原
- 还原图面 WDK DirectDraw
- 丢失的图面 WDK DirectDraw
- 暂停面 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56a3f7231928b88e33750c99d95f6c84b2c1cc30
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832399"
---
# <a name="losing-and-restoring-directdraw-surfaces"></a>丢失和还原 DirectDraw 图面


## <span id="ddk_losing_and_restoring_directdraw_surfaces_gg"></span><span id="DDK_LOSING_AND_RESTORING_DIRECTDRAW_SURFACES_GG"></span>


对于与驱动程序的 surface 对象不同，其运行时的表面对象的表面对象生存期更长。 在少数情况下，最值得注意的是，表面会 *丢失*。 这意味着，在调用 [*DdDestroySurface*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_destroysurface) 时，将销毁驱动程序的 surface 对象，但会将运行时的 surface 对象置于挂起状态。 稍后，可以 *还原* 运行时对象，该对象对应于驱动程序级别的 [*DdCreateSurface*](/previous-versions/windows/hardware/drivers/ff549263(v=vs.85)) 调用。

通常，驱动程序无需知道这种中间丢失状态。 但是，在某些情况下，了解此过程将有助于驱动程序编写器。

驱动程序编写器可以选择在一个原子调用中处理复杂的 surface 还原。 在表面还原时，DirectDraw 运行时检查驱动程序的 [**D3dCreateSurfaceEx**](/windows/win32/api/ddrawint/nc-ddrawint-pdd_createsurfaceex) 入口点。 如果定义了此入口点，则 DirectDraw 运行时在一次调用 [*DdCreateSurface*](/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))时还原所有复杂的图面。 驱动程序可能不能区分原始创建以及通过还原图面引起的创建。

 

