---
title: 丢失和还原 DirectDraw 图面
description: 丢失和还原 DirectDraw 图面
ms.assetid: 74203932-8a30-44ea-8d0d-45265dd2e74a
keywords:
- 绘制的图面 WDK DirectDraw 丢失
- 显示 DirectDraw 表面 WDK Windows 2000，会丢失
- 显示 WDK DirectDraw 丢失
- 绘图图面相 WDK DirectDraw、 还原
- DirectDraw 图面 WDK Windows 2000 显示，请还原
- 显示 WDK DirectDraw 还原
- 还原 WDK DirectDraw 图面
- 丢失图面 WDK DirectDraw
- 挂起的图面 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5292518166bdc186ed258f7b646a41c8f805864
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384842"
---
# <a name="losing-and-restoring-directdraw-surfaces"></a>丢失和还原 DirectDraw 图面


## <span id="ddk_losing_and_restoring_directdraw_surfaces_gg"></span><span id="DDK_LOSING_AND_RESTORING_DIRECTDRAW_SURFACES_GG"></span>


图面上的对象生存期较长的运行时的图面上对象不是它们是用于驱动程序的图面上对象。 在少数情况下，最值得注意的是模式发生更改，图面会变得*丢失*。 这意味着，驱动程序的图面上对象被销毁时[ *DdDestroySurface* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_destroysurface)调用，但运行时的图面上对象放入挂起状态。 运行时对象可以是更高版本，*还原*，它对应于[ *DdCreateSurface* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))驱动程序级别的调用。

通常情况下，驱动程序不需要注意此中间丢失状态。 但是，有某些情况下了解此过程有助于驱动程序编写器。

驱动程序编写人员可以选择处理复杂的图面上还原，在一个原子调用中。 在图面上的还原时间，则 DirectDraw 运行时检查驱动程序的[ **D3dCreateSurfaceEx** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)入口点。 如果定义此入口点，则 DirectDraw 运行时将还原到一次调用中的所有复杂表面[ *DdCreateSurface*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))。 该驱动程序可能将不能在初始创建和创建导致还原图面之间进行区分。

 

 





