---
title: DirectDraw 体系结构
description: DirectDraw 体系结构
keywords:
- GDI WDK DirectDraw
- 绘制 WDK DirectDraw，体系结构
- DirectDraw WDK Windows 2000 显示器、体系结构
- 用户模式 DirectDraw WDK Windows 2000 显示
- 内核模式 DirectDraw WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9321a510d705d1afab722f4748c1cbf5a668df58
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809395"
---
# <a name="directdraw-architecture"></a>DirectDraw 体系结构


## <span id="ddk_directdraw_architecture_gg"></span><span id="DDK_DIRECTDRAW_ARCHITECTURE_GG"></span>


Microsoft DirectDraw 包含以下组件：

-   用户模式 DirectDraw (*ddraw.dll*) ，它是由 DirectDraw 应用程序加载并调用的系统提供的动态链接库 (DLL) 。 此组件提供硬件仿真，管理各种 DirectDraw 对象，并提供显示内存和显示硬件管理服务。

-   内核模式 DirectDraw，它是由内核模式显示驱动程序加载的系统提供的图形引擎 *win32k.sys* 的组成部分。 DirectDraw 的此部分对驱动程序执行参数验证，从而更容易实现更可靠的驱动程序。 这是一个重要的设计目标，因为显示驱动程序是 Microsoft Windows 2000 和更高版本操作系统的受信任组件。 内核模式 DirectDraw 还处理与 GDI 和所有跨进程状态的同步。

-   显示驱动程序的 DirectDraw 部分（以及显示驱动程序的其余部分）是由图形硬件供应商实现的。 在本文档中，此组件称为 DirectDraw 驱动程序。 显示驱动程序的其他部分处理 GDI 和其他与 DirectDraw 相关的调用。

本文档一般指的是系统提供的两个组件。

下图显示了 DirectDraw 驱动程序体系结构的关系图。

![说明 directdraw 驱动程序体系结构的关系图](images/ddfig1.png)

如上图所示，应用程序通过 GDI (用户和内核模式部分) 和显示驱动程序访问显示卡。 显示驱动程序始终支持 GDI 调用，通常支持 DirectDraw 和 Direct3D 调用。 当显示驱动程序不支持 GDI 模拟功能时，与设备无关的位图 (DIB) 引擎部分。

在调用 DirectDraw 时，它通过 DirectDraw 驱动程序直接访问图形卡。 DirectDraw 为受支持的硬件功能调用 DirectDraw 驱动程序，或为必须在软件中模拟的函数 (HEL) 的硬件仿真层。 另一方面，GDI 调用将发送给驱动程序，如果调用不受支持，则必须回调到 DIB 引擎。

**注意**   如果 DirectDraw 驱动程序无法操作，则 DirectDraw 不会将操作传递到 DirectDraw HEL，而是将 DirectDraw 驱动程序的错误代码传递回应用程序。

 

在初始化时和模式更改期间，显示驱动程序会将功能从 (cap 返回到 DirectDraw) 位。 这使得 DirectDraw 可以访问有关可用驱动程序函数及其地址的信息，以及有关显示卡和驱动程序的功能的信息 (例如拉伸、透明 blits、显示跨度和其他高级特性) 。 DirectDraw 提供此信息后，可以使用 DirectDraw 驱动程序直接访问显示卡，而无需进行 GDI 调用或使用显示驱动程序的 GDI 特定部分。

 

 





