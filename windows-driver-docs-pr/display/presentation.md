---
title: 呈现
description: 呈现
ms.assetid: 23a01b5b-0654-4c43-ac96-a75810fa20df
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示、 演示文稿
- 演示文稿 WDK DirectX 8.0
- 呈现结果可见 WDK DirectX 8.0
- 可见结果 WDK DirectX 8.0
- DDLT_PRESENTATION
- DDBLT_LAST_PRESENTATION
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 563fabb561e7ee9f1048f7c6044542446f32a53d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369281"
---
# <a name="presentation"></a>呈现


## <span id="ddk_presentation_gg"></span><span id="DDK_PRESENTATION_GG"></span>


DirectX 8.0 规范"演示文稿"（或进行呈现对用户可见的结果） 的概念在 API 中。 以前，这被完成在全屏幕模式下翻页，或在窗口模式下的平面闪。 应用程序使用的新**存在**API 来执行 full 屏幕翻转或开窗模式平面闪。 但是，此机制是尚未公开 DDI 级别。 运行时只需将映射**存在**API 为[ *DdFlip* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_flip)或者[ *DdBlt* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_blt) DDI 条目具体取决于应用程序模式的点。

DirectX 8.0 已添加的作为传递给驱动程序的通知时 blt 操作实际上是两个新 DirectDraw blt 标志的一部分**存在**，并因此将标记框架边界。 这些新标志才有 DDBLT\_演示文稿和 DDBLT\_最后一个\_演示文稿。 需要两个标志是因为剪辑可能会导致单个**存在**调用调用驱动程序中的多个 blt 操作。 在此情况下，所有调用为 blts**存在**操作具有 DDBLT\_演示文稿标志设置。 但是，用于执行仅序列的最后一个 blt**存在**具有 DDBLT\_最后一个\_演示文稿位集。 因此，如果 blt 用于实现**存在**调用时，该驱动程序会看到与 DDBLT 的零个或多个 blts\_演示文稿设置与这两个 DDLT 恰好一个 blt 后跟位\_演示文稿和 DDBLT\_最后一个\_演示文稿的位组。 应用程序永远不会设置这些标志。 只有运行时被允许传递到 blt 的这些标志。 此外，这些标志仅传递给驱动程序支持 DirectX 8.0 DDI 中。

该驱动程序只允许队列最多三个框架。 如果驱动程序发现与 DDBLT blt 调用\_演示文稿集和它已有三个 DDBLT\_上次\_演示文稿 blts 排队它时不能与 DDERR 调用\_WASSTILLDRAWING。 运行时重试直到具有足够清空队列。

如果该驱动程序不能有效地确定何时 DDBLT\_最后一个\_队列中的演示文稿 blt 已停用，则该驱动程序必须不队列帧根本。 DDBLT\_上次\_演示文稿是否会导致此类驱动程序，以返回 DDERR\_WASSTILLDRAWING 快捷键直到全部完成，就像应用程序已调用完全**锁**上源之前调用的图面**Blt**。

最后，对于多个窗口的应用程序同时运行，驱动程序应计算基于源的每个 blt，而不是主要的演示文稿 blts，即允许驱动程序进行排队三个帧 / 窗口/呈现器目标。 这会导致更好的性能。

 

 





