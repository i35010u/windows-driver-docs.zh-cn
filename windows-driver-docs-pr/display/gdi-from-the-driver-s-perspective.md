---
title: 从驱动程序角度理解 GDI
description: 从驱动程序角度理解 GDI
keywords:
- GDI WDK Windows 2000 显示器，驱动程序通信
- 图形驱动程序 WDK Windows 2000 显示器、驱动程序通信
- 绘制 WDK GDI，驱动程序通信
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 454de18e0f90b25c9df2ff311156ea86dca9f5d8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798335"
---
# <a name="gdi-from-the-drivers-perspective"></a>从驱动程序角度理解 GDI


## <span id="ddk_gdi_from_the_driver_92_s_perspective_gg"></span><span id="DDK_GDI_FROM_THE_DRIVER_92_S_PERSPECTIVE_GG"></span>


GDI 是基于 Microsoft Windows NT 的图形驱动程序和应用程序之间的中介支持。 应用程序调用 Microsoft Win32 GDI 函数来发出图形输出请求。 这些请求将路由到内核模式 GDI。 然后，内核模式 GDI 将这些请求发送到相应的图形驱动程序，如显示驱动程序或打印机驱动程序。 内核模式 GDI 是系统提供的不能替换的模块。

GDI 通过一组图形设备驱动程序接口（ (图形 DDI) 函数）与图形驱动程序通信。 这些函数由其 *winspool.drv* 前缀标识。 通过这些入口点的输入/输出参数，在 GDI 和驱动程序之间传递信息。 驱动程序 *必须* 支持某些用于 GDI 的 *DrvXxx* 函数来调用。 该驱动程序通过在其关联的硬件上执行相应的操作来支持 GDI 的请求，然后再返回到 GDI。

GDI 本身包含许多图形输出功能，无需驱动程序来支持这些功能，从而减少了驱动程序的大小。 GDI 还会导出驱动程序可调用的服务功能，从而进一步减少驱动程序必须提供的支持数量。 GDI 服务函数由其 **Eng** 前缀标识，提供对 GDI 维护结构的访问的函数的名称格式为 *Xxx*<strong>OBJ *\_</strong> * * xxx*。

下图显示了这种通信流。

![阐释图形驱动程序和图形设备接口 (gdi) 交互的关系图](images/gditoddi.png)

 

 





