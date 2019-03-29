---
title: 移动指针 DrvMovePointer
description: 移动指针 DrvMovePointer
ms.assetid: cd82cea8-a37e-4e00-9342-9d6491e8c83c
keywords:
- 显示绘图指针 WDK Windows 2000
- 显示驱动程序 WDK Windows 2000 中，指针
- 显示指针 WDK Windows 2000
- DrvMovePointer
- 移动指针位置
- 重新定位指针
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f573774db34ab9e43efdd83b20da36563ed870b4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575886"
---
# <a name="moving-the-pointer-drvmovepointer"></a>移动指针：DrvMovePointer


## <span id="ddk_moving_the_pointer_drvmovepointer_gg"></span><span id="DDK_MOVING_THE_POINTER_DRVMOVEPOINTER_GG"></span>


如果[ **DrvSetPointerShape** ](https://msdn.microsoft.com/library/windows/hardware/ff556289)纳入该驱动程序，然后[ **DrvMovePointer** ](https://msdn.microsoft.com/library/windows/hardware/ff556248)还必须支持。 此函数将驱动程序管理指针移动到新位置。 因为 GDI 将对指针函数的调用序列化*DrvMovePointer*不会调用任何线程中显示器驱动程序，在绘制时除非 GCAPS\_设置了 ASYNCMOVE 标志[ **DEVINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff552835)结构。

该驱动程序应调用[ **EngMovePointer** ](https://msdn.microsoft.com/library/windows/hardware/ff564977)要具有 GDI 移动设备上的引擎托管指针。 该驱动程序请求 GDI 通过调用管理光标[ **EngSetPointerShape**](https://msdn.microsoft.com/library/windows/hardware/ff565017)。

 

 





