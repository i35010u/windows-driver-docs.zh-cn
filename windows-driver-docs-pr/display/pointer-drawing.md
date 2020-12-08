---
title: 指针绘制
description: 指针绘制
keywords:
- 绘图指针 WDK Windows 2000 显示
- 显示驱动程序 WDK Windows 2000，指针
- 指针 WDK Windows 2000 显示
- 单色指针 WDK Windows 2000 显示
- 颜色指针 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 300c7f34168b512d73e93af535bcf6e07db69bce
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795581"
---
# <a name="pointer-drawing"></a>指针绘制


## <span id="ddk_pointer_drawing_gg"></span><span id="DDK_POINTER_DRAWING_GG"></span>


GDI 支持颜色指针和单色指针。 单色指针的形状由单个位图定义。 位图的宽度与显示器上指针的宽度相同，但位图的垂直区与显示时的宽度两倍，允许它包含两个掩码。

对指针函数的调用由 GDI 序列化。 这意味着驱动程序中的两个不同线程无法同时执行指针函数。 有两个可能的指针函数： [**DrvSetPointerShape**](/windows/win32/api/winddi/nf-winddi-drvsetpointershape) 和 [**DrvMovePointer**](/windows/win32/api/winddi/nf-winddi-drvmovepointer)。

 

