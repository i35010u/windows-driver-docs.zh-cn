---
title: 显示驱动程序 （Windows 2000 模式）
description: 显示驱动程序 （Windows 2000 模式）
ms.assetid: 9d49f4e7-5153-417e-8f15-42b3dcdf3fa6
keywords:
- 显示驱动程序模型 WDK Windows 2000 中，显示器驱动程序
- Windows 2000 显示驱动程序模型 WDK、 显示驱动程序
- 显示驱动程序 WDK Windows 2000
- 显示驱动程序 WDK Windows 2000 中，有关显示器驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aee86541ef21033780ec0a0dfb483ec0ba48ba50
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544818"
---
# <a name="display-drivers-windows-2000-model"></a>显示驱动程序 （Windows 2000 模式）


## <span id="ddk_display_drivers_windows_2000_model__gg"></span><span id="DDK_DISPLAY_DRIVERS_WINDOWS_2000_MODEL__GG"></span>


基于 Microsoft NT 的操作系统显示驱动程序编写人员所关注两个核心软件接口：

-   图形 DDI 接口-的显示器驱动程序实现的函数集。 GDI 可以调用图形 DDI 接口来处理图形命令。

-   GDI 接口调用的系统提供的帮助器例程显示驱动程序来简化驱动程序实现。

本部分介绍与基于 NT 的操作系统显示器驱动程序，以及某些实现信息相关联的关键概念。 请参阅[图形驱动程序支持 GDI](gdi-support-for-graphics-drivers.md)并[使用图形 DDI](using-the-graphics-ddi.md)图形驱动程序设计的详细信息，共有两个打印机驱动程序并显示驱动程序，如驱动程序初始化和终止和图形输出。

显示驱动程序编写人员还可以实现以下 DDIs:

-   DirectDraw DDI-图形界面，使供应商提供的 DirectDraw 硬件加速功能。 请参阅[DirectDraw](directdraw.md)有关详细信息。

-   Direct3D DDI-允许供应商提供的 Direct3D 硬件加速的 3D 图形界面。 请参阅[Direct3D DDI](direct3d.md)有关详细信息。

有关图形 DDI 入口点和结构，以及服务的 GDI 函数和对象，请参阅的完整说明[GDI 函数](https://msdn.microsoft.com/library/windows/hardware/ff566543)。

 

 





