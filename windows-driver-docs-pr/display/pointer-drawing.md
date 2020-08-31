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
ms.openlocfilehash: 33d50d395bc9b98b02f3434c1f2f28a2c9277f69
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064030"
---
# <a name="pointer-drawing"></a>指针绘制


## <span id="ddk_pointer_drawing_gg"></span><span id="DDK_POINTER_DRAWING_GG"></span>


GDI 支持颜色指针和单色指针。 单色指针的形状由单个位图定义。 位图的宽度与显示器上指针的宽度相同，但位图的垂直区与显示时的宽度两倍，允许它包含两个掩码。

对指针函数的调用由 GDI 序列化。 这意味着驱动程序中的两个不同线程无法同时执行指针函数。 有两个可能的指针函数： [**DrvSetPointerShape**](/windows/desktop/api/winddi/nf-winddi-drvsetpointershape) 和 [**DrvMovePointer**](/windows/desktop/api/winddi/nf-winddi-drvmovepointer)。

 

