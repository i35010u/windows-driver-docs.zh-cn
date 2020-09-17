---
title: 指针控件
description: 指针控件
ms.assetid: 70e80be0-28f8-40a7-9018-fab71d80c8f6
keywords:
- 绘图指针 WDK Windows 2000 显示
- 显示驱动程序 WDK Windows 2000，指针
- 指针 WDK Windows 2000 显示
- 传递指针信息 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 967e762a7aef426a95a50b1beadf39d842ea849f
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715642"
---
# <a name="pointer-control"></a>指针控件


## <span id="ddk_pointer_control_gg"></span><span id="DDK_POINTER_CONTROL_GG"></span>


每个应用程序都必须能够控制一个指针，该指针在窗口内显示，以响应指针设备，如鼠标。 显示驱动程序、GDI 或视频微型端口驱动程序可以 [绘制指针](pointer-drawing.md)。 另请参阅 [控制指针](controlling-the-pointer--drvsetpointershape.md) 并 [移动指针](moving-the-pointer--drvmovepointer.md)。

GDI 可以直接处理使用以线性方式寻址的缓冲区显示的所有指针。 对于非 *线性帧缓冲区*的设备，GDI 使用 [**DrvCopyBits**](/windows/win32/api/winddi/nf-winddi-drvcopybits) 来绘制指针。 但是，硬件支持的指针代码和在显示器驱动程序中实现的速度要快得多。

显示驱动程序有时可以选择它们将绘制的指针类型以及将允许 GDI 处理的类型。 例如，设备可能支持硬件中的单色指针，但不能调用颜色指针，而是允许 GDI 改为处理它们。

显示驱动程序可以控制指针，因为在这种情况下，处理器不一定是独占的，因此不需要在中断（例如垂直同步中断）的情况下绘制指针。 在这些特殊情况下，微型端口驱动程序必须绘制并控制指针，因为某些内核模式回调 (仅在视频微型端口驱动程序) 中可用。 这会对性能产生负面影响，因为它要求 IOCTLs 与每个指针操作的微型端口驱动程序通信。

若要编写显示驱动程序和微型端口驱动程序对，必须包含 IOCTLs，用于在两个驱动程序之间传递指针信息，并允许微型端口驱动程序假设绘制任何或所有指针（如有必要）。

 

