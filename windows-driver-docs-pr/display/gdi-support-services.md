---
title: GDI 支持服务
description: GDI 支持服务
ms.assetid: a5521f9f-ddf6-4892-bf6d-aebb7936df11
keywords:
- GDI WDK Windows 2000 显示，服务例程
- 图形驱动程序 WDK Windows 2000 显示，服务例程
- 绘制 WDK GDI，服务例程
- 服务例程 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a78c6bccb13496fde5af186a9772d977246ff90
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839677"
---
# <a name="gdi-support-services"></a>GDI 支持服务


## <span id="ddk_gdi_support_services_gg"></span><span id="DDK_GDI_SUPPORT_SERVICES_GG"></span>


*GDI*将导出许多可简化驱动程序设计的服务例程。 驱动程序可以直接调用这些例程。 例程的名称，这些例程的名称以**Eng**开头。 与特定对象相关的服务例程始终以对象的名称开头;例如， [**CLIPOBJ\_cEnumStart**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-clipobj_cenumstart)是一种[**CLIPOBJ**](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_clipobj)服务。

**请注意**，   第一个参数是指向用户对象的指针是该用户对象上的方法，并且是使用常用C++约定调用的服务例程。 因此，使用编写的C++驱动程序可以将服务例程作为方法来访问。

 

这些服务例程分为以下几类：

[Surface management](gdi-support-for-surfaces.md)

[调色板服务](gdi-support-for-palettes.md)

[路径服务](gdi-services-for-paths.md)

[窗口服务](gdi-support-for-window-objects.md)

[呈现服务](gdi-drawing-and-related-services.md)

[字体和文本服务](gdi-font-and-text-services.md)

[内存服务](gdi-memory-services.md)

[事件服务](gdi-event-services.md)

[文件、模块和进程服务](gdi-file--module--and-process-services.md)

[信号服务](gdi-semaphore-services.md)

[打印机服务](gdi-printer-services.md)

[与驱动程序相关的服务](gdi-driver-related-services.md)

[信息服务](gdi-information-services.md)

[实用工具服务](gdi-utility-services.md)

[浮点服务](gdi-floating-point-services.md)

[半色调服务](gdi-halftone-services.md)

[使用图形 ddi](using-the-graphics-ddi.md)介绍图形 ddi 入口点，并说明其中许多服务例程可用于帮助驱动程序实现入口点。 有关每个服务函数的详细说明，请参阅[由打印机调用的 GDI 函数和显示驱动程序](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。

 

 





