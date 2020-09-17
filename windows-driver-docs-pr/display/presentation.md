---
title: 呈现
description: 呈现
ms.assetid: 23a01b5b-0654-4c43-ac96-a75810fa20df
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，演示
- 演示文稿 WDK DirectX 8。0
- 呈现结果可见 WDK DirectX 8。0
- 可见结果 WDK DirectX 8。0
- DDLT_PRESENTATION
- DDBLT_LAST_PRESENTATION
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2bff4b19ca157fb9a75958a4c35e755f313d0d73
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716014"
---
# <a name="presentation"></a>呈现


## <span id="ddk_presentation_gg"></span><span id="DDK_PRESENTATION_GG"></span>


DirectX 8.0 将 "演示" (的概念正规化，或使用户在 API 中) 可见。 以前，此操作是通过在全屏幕模式下进行页面翻转或按窗口模式 blitting 来完成的。 应用程序使用新的 **现有** API 来执行全屏翻转或窗口模式 blitting。 但是，此机制尚未在 DDI 级别公开。 运行时只需将 **当前** API 映射到 [*DdFlip*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_flip) 或 [*DdBlt*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_blt) DDI 入口点，具体取决于应用程序模式。

DirectX 8.0 添加了两个新的 DirectDraw blt 标志，这些标志将作为通知出现在 blt 操作实际上是 **存在** 的一部分，因此会标记帧边界。 这些新标志是 DDBLT \_ 演示文稿和 DDBLT \_ 上一次 \_ 演示。 需要两个标志，因为剪辑可能会导致在驱动程序中调用多个 blt 操作的单个 **现有** 调用。 在这种情况下，由于 **当前** 操作而调用的所有 blts 都 \_ 将设置 DDBLT 表示标志。 但是，只有用于执行 **现有** 序列的最终 blt 才会 \_ 设置 DDBLT 上一次 \_ 显示位。 因此，如果使用 blt 实现了一个 **当前** 调用，则驱动程序会看到零个或多个 blts，并在其中 \_ 刚好有一个 blt 同时设置了 DDLT \_ 表示和 DDBLT \_ 最后一个 \_ 表示位。 应用程序永远不会设置这些标志。 仅允许运行时将这些标志传递到 blt。 此外，这些标志仅传递到支持 DirectX 8.0 DDI 的驱动程序。

该驱动程序只允许排队最多三个帧。 如果驱动程序发现 blt 调用带有 DDBLT \_ 演示集，并且它已经有三个 DDBLT， \_ 最后一个 \_ 表示 blts 排队，则必须通过 DDERR WASSTILLDRAWING 使调用失败 \_ 。 运行时将重试，直到队列充分耗尽。

如果驱动程序无法有效地确定 \_ 队列中 DDBLT 最后一次 blt 的时间 \_ 已停用，则驱动程序必须根本不会对帧进行排队。 DDBLT \_ 最后一次 \_ 演示应该导致此类驱动程序返回 DDERR \_ WASSTILLDRAWING，直到快捷键完全完成，就像在调用**Blt**之前，应用程序已在源图面上调用**锁**。

最后，对于同时运行的多个开窗应用程序，驱动程序应基于每个 blt 的源（而不是主应用程序）对 blts 进行计数，也就是说，允许驱动程序将每个窗口/呈现器目标的三个帧排队。 这将提高性能。

 

