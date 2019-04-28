---
title: 指针控件
description: 指针控件
ms.assetid: 70e80be0-28f8-40a7-9018-fab71d80c8f6
keywords:
- 显示绘图指针 WDK Windows 2000
- 显示驱动程序 WDK Windows 2000 中，指针
- 显示指针 WDK Windows 2000
- 传递指针信息 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c31e49fb0ffeea2cacc4a860971af4feee692d91
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352204"
---
# <a name="pointer-control"></a>指针控件


## <span id="ddk_pointer_control_gg"></span><span id="DDK_POINTER_CONTROL_GG"></span>


每个应用程序必须能够控制移动以响应指针设备，如鼠标有窗口显示的指针。 显示驱动程序、 GDI 或微型端口驱动程序可以[绘制在指针](pointer-drawing.md)。 请参考[控制指针](controlling-the-pointer--drvsetpointershape.md)并[移动指针](moving-the-pointer--drvmovepointer.md)。

GDI 可直接处理所有绘制显示器的使用以线性方式可寻址缓冲区的指针。 设备不是*线性帧缓冲区*，使用 GDI [ **DrvCopyBits** ](https://msdn.microsoft.com/library/windows/hardware/ff556182)绘制的指针。 但是，支持的硬件和显示驱动程序中实现的指针代码是要快得多。

显示器驱动程序有时可以选择将绘制哪些类型的指针和哪种类型，它们将允许 GDI 来处理。 例如，设备可能会在硬件支持单色指针，但失败颜色的指针调用，允许 GDI 来改为处理它们。

显示驱动程序可以控制在情况下为其处理器不需要以独占方式拥有指针和指针不需要关闭中断，如垂直同步中断绘制。 在这些特殊的情况下，微型端口驱动程序必须绘制并控制鼠标指针，因为某些内核模式回调 （它们是仅微型端口驱动程序） 所需。 这会产生负面影响性能，因为它需要 Ioctl 与每个指针操作的微型端口驱动程序进行通信。

若要编写显示驱动程序和微型端口驱动程序对，必须传递指针信息之间的两个的驱动程序，并允许微型端口驱动程序假定任何或所有指针的绘制，如有必要包括 Ioctl。

 

 





