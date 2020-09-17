---
title: 创建和销毁 DirectDraw 图面
description: 创建和销毁 DirectDraw 图面
ms.assetid: d5557897-1810-448e-a2a8-aba96643b19c
keywords:
- 绘图图面 WDK DirectDraw，创建
- DirectDraw 图面，WDK Windows 2000 显示，创建
- 平面 DirectDraw，创建
- 绘图图面 WDK DirectDraw，销毁
- DirectDraw 图面，WDK Windows 2000 显示，销毁
- surface DirectDraw，销毁
- 销毁图面 WDK DirectDraw
- DdCanCreateSurface
- DdCreateSurface
- D3dCreateSurfaceEx
- DdDestroySurface
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3a248253d077983c83025430dc69fb69825086d
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715344"
---
# <a name="creating-and-destroying-directdraw-surfaces"></a>创建和销毁 DirectDraw 图面


## <span id="ddk_creating_and_destroying_directdraw_surfaces_gg"></span><span id="DDK_CREATING_AND_DESTROYING_DIRECTDRAW_SURFACES_GG"></span>


直接绘制图面在四阶段过程中创建。 这些阶段包括：

1.  [*DdCanCreateSurface*](/previous-versions/windows/hardware/drivers/ff549213(v=vs.85))。 运行时调用驱动程序的 *DdCanCreateSurface* ，以查看驱动程序是否允许创建此类型、大小和格式的图面。 驱动程序可返回传播到应用程序的失败代码。

2.  [*DdCreateSurface*](/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))。 驱动程序创建图面，可能会为图面的内容分配内存。 可以一次创建所有复杂的图面，同时调用 *DdCreateSurface*。 因此，可能需要驱动程序在一次调用中创建多个表面。

3.  内存分配。 DirectDraw 运行时为驱动程序为响应 [*DdCreateSurface*](/previous-versions/windows/hardware/drivers/ff549263(v=vs.85)) 调用而未分配的任何图面分配内存。 以下部分更详细地介绍了此过程。

4.  [**D3dCreateSurfaceEx**](/windows/win32/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)。 此函数将句柄与有问题的图面关联起来，以便以后在 DirectX[**D3dDrawPrimitives2**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb) 令牌流中使用。 该驱动程序还会创建自己的由 DirectDraw 维护的 surface 结构副本。 有关 **D3dCreateSurfaceEx**的详细信息，请参阅 (DDK) 文档中的 DirectX 驱动程序开发工具包。

**注意**   DirectDraw 驱动程序决不能直接为 surface 分配用户模式内存 (例如，通过调用[**EngAllocUserMem**](/windows/win32/api/winddi/nf-winddi-engallocusermem)函数) 。 相反，驱动程序可以使 DirectDraw 运行时为表面分配用户模式内存。
如果驱动程序直接分配内存，则通过创建该图面的进程以外的进程来更改视频模式的后续请求可能会导致操作系统崩溃或内存泄漏。 为了使 DirectDraw 运行时分配用户模式内存，驱动程序应 \_ \_ 从其 [*DDCREATESURFACE*](/previous-versions/windows/hardware/drivers/ff549263(v=vs.85)) 函数返回 DDHAL PLEASEALLOC USERMEM 值。 有关详细信息，请参阅 " *DdCreateSurface* 引用" 页上的 "备注" 部分。

 

仅当在创建图面期间分配或涉及到为图面分配内存时，才会通过对驱动程序的 [*DdDestroySurface*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_destroysurface) 入口点调用来销毁表面。 如果 DirectDraw 运行时分配了内存并且驱动程序未涉及，则运行时不会调用 *DdDestroySurface*。

仅在创建曲面的模式持续时，它们才会保持不变。 如果存在模式更改，则会销毁驱动程序控件下的所有表面，就像驱动程序所关心的一样。 还有其他事件可能会导致所有表面以这种方式销毁。 驱动程序不需要确定 [*DdDestroySurface*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_destroysurface) 调用的原因。

 

