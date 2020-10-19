---
title: 支持图形输出
description: 支持图形输出
ms.assetid: 2ac9b01d-9dca-44b4-9645-9c5eefb2ef1b
keywords:
- GDI WDK Windows 2000 显示，图形输出
- 图形驱动程序 WDK Windows 2000 显示，输出
- 绘制 WDK GDI，图形输出
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: acb52081d1fc9e84e293b4460c0ca0a14f1c3b0b
ms.sourcegitcommit: abe7fe9f3fbee8d12641433eeab623a4148ffed3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2020
ms.locfileid: "92185213"
---
# <a name="supporting-graphics-output"></a>支持图形输出

驱动程序处理的特定图形操作取决于绘图表面和硬件功能。 如果图面为标准格式的 *DIB*，则 GDI 将处理驱动程序不支持的所有呈现操作。 驱动程序可以挂接任意 [绘图函数](optional-display-driver-functions.md) 并实现它们以利用硬件支持。

对于设备管理的图面，驱动程序至少必须支持图形输出函数 [**DrvCopyBits**](/windows/win32/api/winddi/nf-winddi-drvcopybits)、 [**DrvTextOut**](/windows/win32/api/winddi/nf-winddi-drvtextout)和 [**DrvStrokePath**](/windows/win32/api/winddi/nf-winddi-drvstrokepath)。 它可根据需要支持任何其他图形输出功能。 例如，支持 [**DrvBitBlt**](/windows/win32/api/winddi/nf-winddi-drvbitblt)可以提高性能。 某些函数需要特定级别的功能，而其他功能则允许设备通过设置 [**lnk-devinfo**](/windows/win32/api/winddi/ns-winddi-devinfo) 结构中的相应 GCAPS 标志来指示其功能。

对驱动程序的所有绘图调用始终都是单线程的，而不考虑 surface 类型。

以下主题介绍了驱动程序如何实现以下操作：

[绘制线条和曲线](drawing-lines-and-curves.md)

[绘制和填充路径](drawing-and-filling-paths.md)

[复制位图](copying-bitmaps.md)

[半色调](halftoning.md)

[图像颜色管理](image-color-management.md)
