---
title: 指针绘制
description: 指针绘制
ms.assetid: 5eaedf04-cbd9-4591-8cff-0087508aa7a9
keywords:
- 绘图指针 WDK Windows 2000 显示
- 显示驱动程序 WDK Windows 2000，指针
- 指针 WDK Windows 2000 显示
- 单色指针 WDK Windows 2000 显示
- 颜色指针 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b09ac9cf281ff76b50b17fa763adbb0a270f78e3
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715638"
---
# <a name="pointer-drawing"></a>指针绘制


## <span id="ddk_pointer_drawing_gg"></span><span id="DDK_POINTER_DRAWING_GG"></span>


GDI 支持颜色指针和单色指针。 单色指针的形状由单个位图定义。 位图的宽度与显示器上指针的宽度相同，但位图的垂直区与显示时的宽度两倍，允许它包含两个掩码。

对指针函数的调用由 GDI 序列化。 这意味着驱动程序中的两个不同线程无法同时执行指针函数。 有两个可能的指针函数： [**DrvSetPointerShape**](/windows/win32/api/winddi/nf-winddi-drvsetpointershape) 和 [**DrvMovePointer**](/windows/win32/api/winddi/nf-winddi-drvmovepointer)。

 

