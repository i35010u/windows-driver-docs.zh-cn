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
ms.openlocfilehash: 4544bff4ad6a3c8763090253a399b956ea7be92a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372867"
---
# <a name="moving-the-pointer-drvmovepointer"></a>移动指针：DrvMovePointer


## <span id="ddk_moving_the_pointer_drvmovepointer_gg"></span><span id="DDK_MOVING_THE_POINTER_DRVMOVEPOINTER_GG"></span>


如果[ **DrvSetPointerShape** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsetpointershape)纳入该驱动程序，然后[ **DrvMovePointer** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvmovepointer)还必须支持。 此函数将驱动程序管理指针移动到新位置。 因为 GDI 将对指针函数的调用序列化*DrvMovePointer*不会调用任何线程中显示器驱动程序，在绘制时除非 GCAPS\_设置了 ASYNCMOVE 标志[ **DEVINFO** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-tagdevinfo)结构。

该驱动程序应调用[ **EngMovePointer** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engmovepointer)要具有 GDI 移动设备上的引擎托管指针。 该驱动程序请求 GDI 通过调用管理光标[ **EngSetPointerShape**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engsetpointershape)。

 

 





