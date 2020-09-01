---
title: 移动指针 DrvMovePointer
description: 移动指针 DrvMovePointer
ms.assetid: cd82cea8-a37e-4e00-9342-9d6491e8c83c
keywords:
- 绘图指针 WDK Windows 2000 显示
- 显示驱动程序 WDK Windows 2000，指针
- 指针 WDK Windows 2000 显示
- DrvMovePointer
- 移动指针位置
- 重定位指针
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e0bc3bd4285fab65721f536245d8f35adc6f165
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066016"
---
# <a name="moving-the-pointer-drvmovepointer"></a>移动指针：DrvMovePointer


## <span id="ddk_moving_the_pointer_drvmovepointer_gg"></span><span id="DDK_MOVING_THE_POINTER_DRVMOVEPOINTER_GG"></span>


如果驱动程序中包含 [**DrvSetPointerShape**](/windows/desktop/api/winddi/nf-winddi-drvsetpointershape) ，则还必须支持 [**DrvMovePointer**](/windows/desktop/api/winddi/nf-winddi-drvmovepointer) 。 此函数将驱动程序托管指针移动到新位置。 由于 GDI 会序列化对指针函数的调用，因此，如果在显示驱动程序中绘制任何线程，则不会调用 *DrvMovePointer* ，除非已 \_ 在 [**lnk-devinfo**](/windows/desktop/api/winddi/ns-winddi-tagdevinfo) 结构中设置了 GCAPS ASYNCMOVE 标志。

驱动程序应调用 [**EngMovePointer**](/windows/desktop/api/winddi/nf-winddi-engmovepointer) ，使 GDI 可以在设备上移动引擎托管指针。 驱动程序请求 GDI 通过调用 [**EngSetPointerShape**](/windows/desktop/api/winddi/nf-winddi-engsetpointershape)来管理游标。

 

