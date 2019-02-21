---
title: 从驱动程序的角度来看的 GDI
description: 从驱动程序的角度来看的 GDI
ms.assetid: 2a6769ea-c6ae-4397-a5e4-f38964d2d8d1
keywords:
- GDI WDK Windows 2000 显示，驱动程序通信
- 图形驱动程序 WDK Windows 2000 显示，驱动程序通信
- 绘制 WDK GDI，驱动程序通信
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a8cde56bd38f37d2b3c1d91307d59adfe8bf267
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519664"
---
# <a name="gdi-from-the-drivers-perspective"></a>从驱动程序的角度来看的 GDI


## <span id="ddk_gdi_from_the_driver_92_s_perspective_gg"></span><span id="DDK_GDI_FROM_THE_DRIVER_92_S_PERSPECTIVE_GG"></span>


GDI 是基于 Microsoft Windows NT 的图形驱动程序和应用程序之间的中间支持。 应用程序调用 Microsoft Win32 GDI 函数，使图形输出请求。 这些请求路由到内核模式 GDI。 内核模式 GDI 然后将这些请求发送到相应的图形驱动程序，如显示驱动程序或打印机驱动程序。 内核模式 GDI 是一个系统提供的模块，不能替换。

GDI 与图形驱动程序通过一系列图形设备驱动程序接口 （DDI 图形） 功能进行通信。 这些函数由标识其*Drv*前缀。 GDI 和驱动程序之间的信息通过这些入口点的输入/输出参数传递。 该驱动程序*必须*支持某些*DrvXxx* GDI 要调用的函数。 该驱动程序支持 GDI 的请求通过返回到 GDI 之前执行其相关联的硬件上的适当操作。

GDI 中本身、 消除对驱动程序以支持这些功能需要和从而使可减少驱动程序的大小包括许多图形输出功能。 GDI 还将导出该驱动程序可以调用，服务功能进一步减少了驱动程序必须提供的支持。 GDI 服务功能由标识其**Eng**前缀，并提供对 GDI 维护结构的访问的函数具有名称形式*Xxx*<strong>OBJ *\_</strong>* * Xxx*。

下图显示了该通信流程。

![说明的图形驱动程序和图形设备接口 (gdi) 交互的关系图](images/gditoddi.png)

 

 





