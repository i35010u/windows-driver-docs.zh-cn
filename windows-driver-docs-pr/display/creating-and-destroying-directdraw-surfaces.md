---
title: 创建和销毁 DirectDraw 图面
description: 创建和销毁 DirectDraw 图面
ms.assetid: d5557897-1810-448e-a2a8-aba96643b19c
keywords:
- 绘图图面相 WDK DirectDraw、 创建
- DirectDraw 图面 WDK Windows 2000 显示，请创建
- 显示 WDK DirectDraw 创建
- 绘图图面相 WDK DirectDraw、 销毁
- DirectDraw 图面 WDK Windows 2000 显示，请销毁
- 显示 WDK DirectDraw 销毁
- 销毁 WDK DirectDraw 图面
- DdCanCreateSurface
- DdCreateSurface
- D3dCreateSurfaceEx
- DdDestroySurface
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d26ee923972cf76b2de93340d4cc88b6a51fdc46
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564821"
---
# <a name="creating-and-destroying-directdraw-surfaces"></a>创建和销毁 DirectDraw 图面


## <span id="ddk_creating_and_destroying_directdraw_surfaces_gg"></span><span id="DDK_CREATING_AND_DESTROYING_DIRECTDRAW_SURFACES_GG"></span>


四个阶段过程中创建直接绘图图面。 这些阶段包括：

1.  [*DdCanCreateSurface*](https://msdn.microsoft.com/library/windows/hardware/ff549213)。 运行时调用的驱动程序*DdCanCreateSurface*若要查看驱动程序是否允许创建此类型、 大小和格式的面。 该驱动程序可以返回到应用程序传播了失败代码。

2.  [*DdCreateSurface*](https://msdn.microsoft.com/library/windows/hardware/ff549263)。 驱动程序创建面上，可能会分配的内存图面的内容。 可以使用一次调用，创建复杂的图面*DdCreateSurface*。 因此，该驱动程序可能需要一次调用创建许多曲面。

3.  内存分配。 DirectDraw 运行时为内存分配到响应中的驱动程序都没有分配任何面的[ *DdCreateSurface* ](https://msdn.microsoft.com/library/windows/hardware/ff549263)调用。 以下各节中更详细地介绍了此过程。

4.  [**D3dCreateSurfaceEx**](https://msdn.microsoft.com/library/windows/hardware/ff542840)。 此函数将一个句柄以供将来使用 DirectX 中有问题的图面与相关联[**D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704)标记流。 该驱动程序还会创建其自己的这一次维护 DirectDraw 图面上结构副本。 有关详细信息**D3dCreateSurfaceEx**，请参阅 DirectX 驱动程序开发工具包 (DDK) 文档。

**请注意**   DirectDraw 驱动程序必须永远不会直接分配用户模式内存图面 (例如，通过调用[ **EngAllocUserMem** ](https://msdn.microsoft.com/library/windows/hardware/ff564178)函数)。 相反，驱动程序可以为用户模式内存中的图面分配 DirectDraw 运行时。
如果该驱动程序直接分配的内存，后续请求以更改视频模式的进程，而不是创建的图面上，可能会导致操作系统崩溃或内存泄漏。 若要让 DirectDraw 运行时分配的用户模式内存，则驱动程序应返回 DDHAL\_PLEASEALLOC\_USERMEM 值从其[ *DdCreateSurface* ](https://msdn.microsoft.com/library/windows/hardware/ff549263)函数。 详细信息，请参阅备注部分上*DdCreateSurface*参考页。

 

通过驱动程序的单一调用销毁图面[ *DdDestroySurface* ](https://msdn.microsoft.com/library/windows/hardware/ff549281)入口点仅当该驱动程序分配，或参与面的图面上创建期间分配的内存。 如果 DirectDraw 运行时分配内存并不涉及该驱动程序，运行时不会调用*DdDestroySurface*。

仅当在其中创建的模式仍然存在，将保留图面。 模式更改时，驱动程序的控制下的所有表面被都破坏，就而言，驱动程序。 也有可能会导致这种方式要销毁的所有表面其他事件。 不需要的驱动程序，以确定原因[ *DdDestroySurface* ](https://msdn.microsoft.com/library/windows/hardware/ff549281)调用。

 

 





