---
title: 处理非标准显示模式
description: 处理非标准显示模式
ms.assetid: 4a3b0064-46d4-40bb-b49b-ac172012a7b7
keywords:
- 使用了非标准的显示模式 WDK DirectX 9.0 中，处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54bb8c5a64a372260bc8ebd24e5f04ef44ab75df
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323801"
---
# <a name="handling-nonstandard-display-modes"></a>处理非标准显示模式


## <span id="ddk_handling_nonstandard_display_modes_gg"></span><span id="DDK_HANDLING_NONSTANDARD_DISPLAY_MODES_GG"></span>


支持非标准的显示模式的设备的 DirectX 9.0 驱动程序还必须处理使用，使用了非标准模式下的以下操作：

-   翻转位块，锁定和解锁的行为与使用标准显示模式相同的操作。

-   对驱动程序的图形设备接口 (GDI) 函数的 DirectX 主面处于活动状态时调用。

    该驱动程序不应在收到任何 GDI DDI 主 DirectX 处于活动状态时绘制调用。 但是，该驱动程序应处理此类绘制而不会导致操作系统崩溃。 驱动程序可以提供一个实现，这种情况下的，忽略该立即返回成功的消息，或将其故障。 请注意，GDI 中的数据基于 GDI 的主图面格式。 因此，如果该驱动程序提供了一个实现，这种情况下的，它必须从 GDI 格式转换之前绘制到 DirectX 主图面。

-   调用 GDI DDI *DrvDeriveSurface*针对 DirectX 主面函数不会发生，因为 GDI 无法访问的非标准的显示格式。

-   DirectX 主面处于活动状态时，请键入"Ctl + Alt + Del"。

    内核驱动程序的调用中的目标为指定标准主[ *DdFlip* ](https://msdn.microsoft.com/library/windows/hardware/ff549306)函数任何 GDI 绘图发生之前。 因此，该驱动程序必须进行编程标准显示模式之前任何 GDI 绘制到显示设备。 在驱动程序[ *DdDestroySurface* ](https://msdn.microsoft.com/library/windows/hardware/ff549281)函数也称为主图面。 请注意，驱动程序可以放弃 DirectX 主图面的内容。

-   窗口模式和非标准格式

    [2D 操作面格式使用报告支持](reporting-support-for-2d-operations-using-surface-formats.md)主题介绍如何驱动程序指定它可以从不同于当前桌面的格式执行到呈现和存在的映像。 此方案很自然地扩展以支持非标准格式; 数据格式该驱动程序只将添加中的启用标志**dwOperations**的成员[ **DDPIXELFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff550274)格式的结构。

专用格式和旧代码不能用于公开使用了非标准的桌面格式。

 

 





