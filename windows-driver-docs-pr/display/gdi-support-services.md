---
title: GDI 支持服务
description: GDI 支持服务
ms.assetid: a5521f9f-ddf6-4892-bf6d-aebb7936df11
keywords:
- GDI WDK Windows 2000 显示中，服务例程
- 图形驱动程序 WDK Windows 2000 显示中，服务例程
- 绘制 WDK GDI，服务例程
- 服务例程 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca220ac893d235b99633179f7c4618a3ca9712bf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543141"
---
# <a name="gdi-support-services"></a>GDI 支持服务


## <span id="ddk_gdi_support_services_gg"></span><span id="DDK_GDI_SUPPORT_SERVICES_GG"></span>


*GDI*导出可以简化驱动程序设计的许多服务例程。 该驱动程序可以直接调用这些例程。 名称的例程的是常规的图形引擎的服务的名称开头**Eng**。 始终与特定对象相关的服务例程开头的对象; 的名称例如， [ **CLIPOBJ\_cEnumStart** ](https://msdn.microsoft.com/library/windows/hardware/ff539421)是[ **CLIPOBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff539417)服务。

**请注意**  服务例程中的第一个参数是指向用户对象的指针是用户对象上的方法，使用常用的 c + + 约定调用。 因此，在 c + + 编写的驱动程序可以作为方法访问服务例程。

 

这些服务例程划分为以下类别：

[设计面管理](gdi-support-for-surfaces.md)

[调色板服务](gdi-support-for-palettes.md)

[路径服务](gdi-services-for-paths.md)

[窗口服务](gdi-support-for-window-objects.md)

[呈现服务](gdi-drawing-and-related-services.md)

[字体和文本服务](gdi-font-and-text-services.md)

[内存服务](gdi-memory-services.md)

[事件服务](gdi-event-services.md)

[文件、 模块和处理服务](gdi-file--module--and-process-services.md)

[信号量服务](gdi-semaphore-services.md)

[打印机服务](gdi-printer-services.md)

[与驱动程序相关的服务](gdi-driver-related-services.md)

[信息服务](gdi-information-services.md)

[公用服务](gdi-utility-services.md)

[浮点服务](gdi-floating-point-services.md)

[半色调服务](gdi-halftone-services.md)

[使用图形 DDI](using-the-graphics-ddi.md)描述图形 DDI 入口点，还介绍了其中许多服务例程可用于帮助驱动程序实现的入口点。 每个服务函数的详细说明，请参阅[由打印机和显示器驱动程序的 GDI 函数调用](https://msdn.microsoft.com/library/windows/hardware/ff566544)。

 

 





