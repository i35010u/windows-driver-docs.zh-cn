---
title: 指针绘制
description: 指针绘制
ms.assetid: 5eaedf04-cbd9-4591-8cff-0087508aa7a9
keywords:
- 显示绘图指针 WDK Windows 2000
- 显示驱动程序 WDK Windows 2000 中，指针
- 显示指针 WDK Windows 2000
- 单色指针 WDK Windows 2000 显示
- 显示颜色指针 WDK Windows 2000
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7eb6a48f2f26749da0d7cb7fa9c3b7aad403f4d2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365701"
---
# <a name="pointer-drawing"></a>指针绘制


## <span id="ddk_pointer_drawing_gg"></span><span id="DDK_POINTER_DRAWING_GG"></span>


GDI 支持颜色指针和单色指针。 由单个位图定义单色指针的形状。 位图的宽度是相同的将指针悬停在显示中，但位图的宽度具有范围作为两次垂直上将显示的显示，从而使其可以包含两个掩码。

对指针函数的调用是通过 GDI 进行序列化。 这意味着在驱动程序中的两个不同的线程不能同时执行指针函数。 有两个可能的指针函数：[**DrvSetPointerShape** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsetpointershape)并[ **DrvMovePointer**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvmovepointer)。

 

 





