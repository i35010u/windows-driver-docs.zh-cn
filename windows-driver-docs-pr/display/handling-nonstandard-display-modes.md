---
title: 处理非标准显示模式
description: 处理非标准显示模式
keywords:
- 非标准显示模式 WDK DirectX 9.0，处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c07b9f76245d71cbf945ea751dbace0f6534cefc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796273"
---
# <a name="handling-nonstandard-display-modes"></a>处理非标准显示模式


## <span id="ddk_handling_nonstandard_display_modes_gg"></span><span id="DDK_HANDLING_NONSTANDARD_DISPLAY_MODES_GG"></span>


支持非标准显示模式的设备的 DirectX 9.0 驱动程序还必须处理以下使用该非标准模式的操作：

-   与标准显示模式的行为相同的翻转、array.blit、锁定和解锁操作。

-   在 DirectX 主表面处于活动状态时，对驱动程序的图形设备接口 (GDI) 函数的调用。

    在 DirectX 主处于活动状态时，驱动程序不应收到任何 GDI DDI 绘图调用。 但是，驱动程序应处理此类绘图，而不会导致操作系统崩溃。 驱动程序可以提供此情况的实现，通过立即返回 success 来忽略它，或使其失败。 请注意，来自 GDI 的数据基于 GDI 主表面格式。 因此，如果驱动程序提供了此情况的实现，则在将其绘制到 DirectX 主图面之前，它必须从 GDI 格式转换。

-   由于 GDI 无法访问非标准的显示格式，因此不能对 DirectX 主表面调用 GDI DDI *DrvDeriveSurface* 函数。

-   在 DirectX 主图面处于活动状态时键入 "Ctl + Alt + Del"。

    在发生任何 GDI 绘图之前，内核将标准主副本指定为对驱动程序的 [*DdFlip*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_flip) 函数的调用中的目标。 因此，在任何 GDI 绘图之前，驱动程序必须将显示设备编程为标准显示模式。 还将调用主图面的驱动程序的 [*DdDestroySurface*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_destroysurface) 函数。 请注意，驱动程序可能会放弃 DirectX 主图面的内容。

-   窗口模式和非标准格式

    使用 "表面格式" 的 " [针对2D 操作的报表支持](reporting-support-for-2d-operations-using-surface-formats.md) " 主题介绍了驱动程序如何指定它可以执行呈现并呈现与当前桌面不同的格式的图像。 此方案自然扩展以支持非标准格式;驱动程序必须只在 [**DDPIXELFORMAT**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat)结构的 **dwOperations** 成员中添加启用标志，才能获得格式。

专用格式和旧代码不能用于公开非标准桌面格式。

 

