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
ms.openlocfilehash: 0194b0d84ba3cc3f097c3ed40f7cabcb7369be41
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358455"
---
# <a name="pointer-drawing"></a>指针绘制


## <span id="ddk_pointer_drawing_gg"></span><span id="DDK_POINTER_DRAWING_GG"></span>


GDI 支持颜色指针和单色指针。 由单个位图定义单色指针的形状。 位图的宽度是相同的将指针悬停在显示中，但位图的宽度具有范围作为两次垂直上将显示的显示，从而使其可以包含两个掩码。

对指针函数的调用是通过 GDI 进行序列化。 这意味着在驱动程序中的两个不同的线程不能同时执行指针函数。 有两个可能的指针函数：[**DrvSetPointerShape** ](https://msdn.microsoft.com/library/windows/hardware/ff556289)并[ **DrvMovePointer**](https://msdn.microsoft.com/library/windows/hardware/ff556248)。

 

 





