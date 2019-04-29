---
title: 异步渲染
description: 异步渲染
ms.assetid: f291e416-aaee-4639-9410-6d01b3b02097
keywords:
- 显示器驱动程序 WDK Windows 2000，异步呈现
- 异步呈现 WDK Windows 2000 显示
- 以异步方式呈现 WDK Windows 2000 显示
- 同步 WDK Windows 2000 显示
- 批处理 DirectDraw WDK Windows 2000 的绘图调用显示
- DirectDraw WDK Windows 2000 显示，请调用批处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37e3e8ba92f957b90f6db108180c8889ae674439
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350327"
---
# <a name="asynchronous-rendering"></a>异步渲染


## <span id="ddk_asynchronous_rendering_gg"></span><span id="DDK_ASYNCHRONOUS_RENDERING_GG"></span>


显示驱动程序，用于以异步方式处理一个或多个图形 DDI 绘制操作并能够使用其位图使用 GDI **EngModifySurface**。 该驱动程序还必须提供同步例程，以避免绘制错误，如果批处理图形 DDI 绘制操作。

此类驱动程序可以选择实现之一[ **DrvSynchronizeSurface** ](https://msdn.microsoft.com/library/windows/hardware/ff557273)或[ **DrvSynchronize** ](https://msdn.microsoft.com/library/windows/hardware/ff556323)与同步例程。 GDI 仅当该驱动程序已挂钩中对其调用每个例程[ **EngAssociateSurface**](https://msdn.microsoft.com/library/windows/hardware/ff564183)。 将仅调用 GDI **DrvSynchronizeSurface**将这两个同步例程挂接的驱动程序中。

[**DrvSynchronizeSurface** ](https://msdn.microsoft.com/library/windows/hardware/ff557273)提供对有关同步事件和为什么会发生驱动程序的其他信息。 这使驱动程序以减少由于同步的性能延迟。 例如，驱动程序加速器的队列中的哪些设备位图为该跟踪可能无法立即返回从**DrvSynchronizeSurface**如果指定的图面当前未在队列中。

除了提供同步例程，驱动程序还可以激活*基于时间*或*编程 * * 刷新机制*中设置以下标志**flGraphicsCaps2**字段[ **DEVINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff552835)结构：

-   GCAPS2\_SYNCTIMER-设置此标志会导致将定期调用的驱动程序同步例程。 批处理图形 DDI 调用的驱动程序必须指定此标志。 通过此操作，这些驱动程序软件光标的移动或中绘制的延迟执行爆发性地诸如避免问题。

    GDI 传递 DSS\_计时器\_到的事件标志[ **DrvSynchronizeSurface** ](https://msdn.microsoft.com/library/windows/hardware/ff557273)因定期事件而调用此同步例程时。

-   GCAPS2\_SYNCFLUSH-设置此标志会使驱动程序的同步例程调用 Microsoft Win32 **GdiFlush**调用 API。 执行异步呈现的驱动程序必须指定此标志，并提供同步例程。

    GDI 传递 DSS\_刷新\_到的事件标志[ **DrvSynchronizeSurface** ](https://msdn.microsoft.com/library/windows/hardware/ff557273)此同步例程由于刷新基于事件的调用时。 请参阅的详细信息的 Microsoft Windows SDK 文档**GdiFlush**。

### <a name="span-idlimitationsonbatchingdirectdrawdrawingcallsspanspan-idlimitationsonbatchingdirectdrawdrawingcallsspanspan-idlimitationsonbatchingdirectdrawdrawingcallsspanlimitations-on-batching-directdraw-drawing-calls"></a><span id="Limitations_on_Batching_DirectDraw_Drawing_Calls"></span><span id="limitations_on_batching_directdraw_drawing_calls"></span><span id="LIMITATIONS_ON_BATCHING_DIRECTDRAW_DRAWING_CALLS"></span>批处理 DirectDraw 绘图调用的限制

驱动程序必须永远不会执行批处理 DirectDraw 绘图调用时目标面是可见的屏幕。 这种情况发生在有窗口 DirectX 应用程序中已完成的帧通过在屏幕上的更新位置[ *DdBlt* ](https://msdn.microsoft.com/library/windows/hardware/ff549205) ，因此应立即显示。 此限制也适用于 DirectDraw 视频端口图面，可能会以异步方式翻转。

 

 





