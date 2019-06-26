---
title: 图形驱动程序的 GDI 支持
description: 图形驱动程序的 GDI 支持
ms.assetid: ef42cda0-106f-4c1b-babc-29a1070e2a2f
keywords:
- GDI WDK Windows 2000 显示中引用
- 图形驱动程序 WDK Windows 2000 显示引用
- 绘制 WDK GDI，引用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31dff39f68591e368813187119599a80791ee86a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376612"
---
# <a name="gdi-support-for-graphics-drivers"></a>图形驱动程序的 GDI 支持


## <span id="ddk_gdi_support_for_graphics_drivers_gg"></span><span id="DDK_GDI_SUPPORT_FOR_GRAPHICS_DRIVERS_GG"></span>


本部分介绍基于 Microsoft Windows NT 的操作系统的图形设备接口 (GDI)。 然后，它详细说明 GDI 提供图形驱动程序的支持。

对在本部分中的 GDI 的引用是对内核模式 GDI; 隐式引用Microsoft Win32 GDI 将显式标识。 内核模式 GDI 也称为是图形引擎。

中介绍了 GDI 函数和结构参考资料[显示设备参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)部分。 大部分 GDI 函数声明和结构定义可在*Winddi.h*。 显示器驱动程序的 Microsoft DirectDraw 堆管理器函数中声明*Dmemmgr.h*。 这两种文件传送使用 Windows Driver Kit (WDK)。

 

 





