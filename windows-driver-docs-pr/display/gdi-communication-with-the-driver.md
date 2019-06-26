---
title: GDI 与驱动程序的通信
description: GDI 与驱动程序的通信
ms.assetid: 81d9e87f-883b-4019-86fc-bccde861de46
keywords:
- GDI WDK Windows 2000 显示，驱动程序通信
- 图形驱动程序 WDK Windows 2000 显示，驱动程序通信
- 绘制 WDK GDI，驱动程序通信
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd59ab322eb4d96aa3a8f18ceb30bb2d951ac729
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386110"
---
# <a name="gdi-communication-with-the-driver"></a>GDI 与驱动程序的通信


## <span id="ddk_gdi_communication_with_the_driver_gg"></span><span id="DDK_GDI_COMMUNICATION_WITH_THE_DRIVER_GG"></span>


该驱动程序将只有一个函数导出到 GDI:[**DrvEnableDriver**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenabledriver)。 所有其他驱动程序支持功能，包括[ **DrvDisableDriver** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdisabledriver)函数中，公开给 GDI 通过的指针的数组。 GDI 调用**DrvEnableDriver**初始化该驱动程序和传递回的驱动程序支持图形列表 DDI 函数。 虽然有一个驱动程序必须支持某些函数，GDI 将处理接收到来自驱动程序的函数列表中不包括这些操作**DrvEnableDriver**例程。 GDI 调用*DrvDisableDriver*驱动程序时无法卸载。 图形 DDI 函数深入探讨[使用图形 DDI](using-the-graphics-ddi.md)。

GDI 使大量对象和服务可供该驱动程序。 这些更改分为两类： 用户对象和服务例程。

 

 





