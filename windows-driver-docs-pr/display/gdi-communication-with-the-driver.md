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
ms.openlocfilehash: 35905c02d622b0e31c1aaedf6d25190361cfa1a9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353863"
---
# <a name="gdi-communication-with-the-driver"></a>GDI 与驱动程序的通信


## <span id="ddk_gdi_communication_with_the_driver_gg"></span><span id="DDK_GDI_COMMUNICATION_WITH_THE_DRIVER_GG"></span>


该驱动程序将只有一个函数导出到 GDI:[**DrvEnableDriver**](https://msdn.microsoft.com/library/windows/hardware/ff556210)。 所有其他驱动程序支持功能，包括[ **DrvDisableDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff556196)函数中，公开给 GDI 通过的指针的数组。 GDI 调用**DrvEnableDriver**初始化该驱动程序和传递回的驱动程序支持图形列表 DDI 函数。 虽然有一个驱动程序必须支持某些函数，GDI 将处理接收到来自驱动程序的函数列表中不包括这些操作**DrvEnableDriver**例程。 GDI 调用*DrvDisableDriver*驱动程序时无法卸载。 图形 DDI 函数深入探讨[使用图形 DDI](using-the-graphics-ddi.md)。

GDI 使大量对象和服务可供该驱动程序。 这些更改分为两类： 用户对象和服务例程。

 

 





