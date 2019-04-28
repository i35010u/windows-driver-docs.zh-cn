---
title: DirectDraw 体系结构
description: DirectDraw 体系结构
ms.assetid: 3bdde4f0-7502-4ca0-80bd-c4d3d93b85fd
keywords:
- GDI WDK DirectDraw
- 绘制 WDK DirectDraw，体系结构
- DirectDraw WDK Windows 2000 显示，体系结构
- 用户模式下 DirectDraw WDK Windows 2000 显示
- 内核模式 DirectDraw WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe32349048421cd29066bac2b299719e3c4a49a5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352903"
---
# <a name="directdraw-architecture"></a>DirectDraw 体系结构


## <span id="ddk_directdraw_architecture_gg"></span><span id="DDK_DIRECTDRAW_ARCHITECTURE_GG"></span>


Microsoft DirectDraw 包括以下组件：

-   用户模式下 DirectDraw (*ddraw.dll*)，这是系统提供动态链接库 (DLL 来加载和 DirectDraw 应用程序调用的)。 此组件提供硬件仿真、 管理各种 DirectDraw 对象，并提供显示内存和显示硬件管理服务。

-   内核模式 DirectDraw，这是一个整型的一部分*win32k.sys*，由内核模式显示驱动程序加载的系统提供的图形引擎。 DirectDraw 的这一部分的驱动程序，使其更轻松地实现更可靠的驱动程序执行参数验证。 这是因为显示器驱动程序是 Microsoft Windows 2000 和更高版本操作系统的受信任的组件的关键设计目标。 内核模式 DirectDraw 还处理与 GDI 和所有跨进程状态的同步。

-   显示驱动程序，它在其余部分的显示驱动程序，将实现由图形硬件供应商 DirectDraw 部分。 此组件称为本文档中的 DirectDraw 驱动程序。 显示驱动程序句柄 GDI 的其他部分和其他非 DirectDraw 相关的调用。

本文档以一般方式将两个系统提供的组件称为 DirectDraw。

下图显示了 DirectDraw 驱动程序体系结构的关系图。

![说明 directdraw 驱动程序体系结构的关系图](images/ddfig1.png)

在上图中所示，应用程序访问通过 GDI （用户和内核模式部分） 显示卡和显示驱动程序。 显示驱动程序始终支持 GDI 调用和 DirectDraw，通常情况下，和 Direct3D 调用。 不受显示器驱动程序时，设备无关位图 (DIB) 引擎部分的 GDI 来模拟功能。

DirectDraw 调用时，它的 DirectDraw 驱动程序通过直接访问图形卡。 DirectDraw 调用的函数必须在软件中模拟的受支持的硬件功能的 DirectDraw 驱动程序或硬件仿真层 (HEL)。 GDI 调用，但是，将发送到驱动程序，然后，必须调用返回到 DIB 引擎如果调用不受支持。

**请注意**   DirectDraw DirectDraw 驱动程序失败操作，如果不将操作传递到 DirectDraw HEL，而是将 DirectDraw 驱动程序的错误代码传递回应用程序。

 

在初始化时和在模式更改期间，显示器驱动程序返回功能 (cap) 位到 DirectDraw。 这使 DirectDraw 来访问有关可用的驱动程序函数，其地址和显示卡和驱动程序的功能信息 （如延伸，透明 blits，可以显示音调、 和其他高级的特征）。 一旦 DirectDraw 后，此信息，它可以使用 DirectDraw 驱动程序显示卡直接访问，而无需进行 GDI 调用或使用 GDI 特定部分的显示驱动程序。

 

 





