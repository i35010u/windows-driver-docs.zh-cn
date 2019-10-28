---
title: 图形驱动程序的 GDI 支持
description: 图形驱动程序的 GDI 支持
ms.assetid: ef42cda0-106f-4c1b-babc-29a1070e2a2f
keywords:
- GDI WDK Windows 2000 显示，参考
- 图形驱动程序 WDK Windows 2000 显示，参考
- 绘制 WDK GDI，引用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb40614162608e34f5249d20c63a8de776796f66
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839684"
---
# <a name="gdi-support-for-graphics-drivers"></a>图形驱动程序的 GDI 支持


## <span id="ddk_gdi_support_for_graphics_drivers_gg"></span><span id="DDK_GDI_SUPPORT_FOR_GRAPHICS_DRIVERS_GG"></span>


本部分介绍基于 Microsoft Windows NT 的操作系统图形设备接口（GDI）。 然后，它详细说明了 GDI 为图形驱动程序提供的支持。

本节中对 GDI 的引用是对内核模式 GDI 的隐式引用;将显式标识 Microsoft Win32 GDI。 内核模式 GDI 也称为图形引擎。

GDI 函数和结构引用记录在 "[显示设备参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)" 部分中。 大多数 GDI 函数声明和结构定义都可以在*Winddi*中找到。 对于显示驱动程序，Microsoft DirectDraw 堆管理器函数在*Dmemmgr*中声明。 这两个文件附带 Windows 驱动程序工具包（WDK）。

 

 





