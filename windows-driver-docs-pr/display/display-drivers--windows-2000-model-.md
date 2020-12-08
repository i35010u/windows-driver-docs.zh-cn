---
title: 显示驱动程序（Windows 2000 模型）
description: 显示驱动程序（Windows 2000 模型）
keywords:
- 显示驱动程序模型 WDK Windows 2000，显示驱动程序
- Windows 2000 显示器驱动程序模型 WDK，显示驱动程序
- 显示驱动程序 WDK Windows 2000
- 显示驱动程序 WDK Windows 2000，关于显示器驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c9b07b363c3a69053d13d4714ddeea5799f8c06
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809255"
---
# <a name="display-drivers-windows-2000-model"></a>显示驱动程序（Windows 2000 模型）


## <span id="ddk_display_drivers_windows_2000_model__gg"></span><span id="DDK_DISPLAY_DRIVERS_WINDOWS_2000_MODEL__GG"></span>


基于 Microsoft NT 的操作系统显示驱动程序编写器涉及两个核心软件接口：

-   图形 DDI 接口-显示驱动程序实现的函数集。 GDI 可以调用图形 DDI 接口来处理图形命令。

-   GDI 接口-系统提供的、由显示驱动程序调用的帮助器例程，以简化驱动程序实现。

本部分介绍与基于 NT 的操作系统显示驱动程序相关的关键概念，以及一些实现信息。 有关打印机驱动程序和显示驱动程序（如驱动程序初始化和终止）和图形输出等常见的图形驱动程序设计细节，请参阅 [对图形驱动程序的 GDI 支持](gdi-support-for-graphics-drivers.md) 和 [使用图形 DDI](using-the-graphics-ddi.md) 。

显示驱动程序编写器还可以实现以下 DDIs：

-   DirectDraw DDI-图形接口，允许供应商提供适用于 DirectDraw 的硬件加速。 有关详细信息，请参阅 [DirectDraw](directdraw.md) 。

-   Direct3D DDI-三维图形界面，允许供应商提供 Direct3D 的硬件加速。 有关详细信息，请参阅 [DIRECT3D DDI](direct3d.md) 。

有关图形 DDI 入口点和结构以及 GDI 服务函数和对象的完整说明，请参阅 [Gdi 函数](/windows-hardware/drivers/ddi/index)。

 

