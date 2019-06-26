---
title: Direct3D 图面句柄
description: Direct3D 图面句柄
ms.assetid: cefede2e-3e82-4de3-ae49-4982578fd2fe
keywords:
- 上下文 WDK Direct3D 图面上的句柄
- 图面处理 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6de7eb01e57cbe98153f9c4708df9b32ab3cf2e5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384864"
---
# <a name="direct3d-surface-handles"></a>Direct3D 图面句柄


## <span id="ddk_direct3d_surface_handles_gg"></span><span id="DDK_DIRECT3D_SURFACE_HANDLES_GG"></span>


Microsoft DirectX 7.0 设备驱动程序接口 (DDI) 旨在提升，由此 Direct3D 运行时组件分析尽可能少的命令流尽可能之前将命令传递给驱动程序模型。 此外，以便它可供将来的硬件，则应格式化命令流。

定向到这些目标的一项重要更改是从中间结构拥有的 Direct3D/DirectDraw 运行时为所拥有、 更新和驱动程序进行格式设置的结构中所有面相关数据的移动。

通过命令数据流中嵌入的句柄进行引用图面。 在这些高频率操作中，该驱动程序可以查找的图面表示从该句柄，而不必求助于如锁定通过帮助程序函数面[ **EngLockDirectDrawSurface** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-englockdirectdrawsurface).

分配这些句柄的机制是一个名为的驱动程序入口点[ **D3dCreateSurfaceEx**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)。 对现有的调用后面直接调用此入口点[ *DdCanCreateSurface* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549213(v=vs.85))并[ *DdCreateSurface* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))入口点和后的视频内存地址和句柄已分配给一个面。 在**D3dCreateSurfaceEx**时，驱动程序将复制所有相关的信息 DirectDraw 运行时的复制的图面上的结构，包括其自己图面上的结构。 驱动程序端副本所需的大小，如图面上的数据格式，并**fpVidMem** (的成员[ **DD\_图面\_全局**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_surface_global)结构）。

由运行时句柄被保证对于每个设备和每个进程是唯一的。 不保证是唯一的每个上下文句柄和其中的驱动程序中更详细地讨论了一些含义[创建驱动程序端面结构](creating-driver-side-surface-structures.md)。

没有对应的**DestroySurfaceEx**调用，以便在销毁端驱动程序的图面上结构[ *DdDestroySurface* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_destroysurface)时间。

 

 





