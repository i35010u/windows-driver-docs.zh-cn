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
ms.openlocfilehash: 3ff61aae629e2c2cb395d300b1c61b7847834023
ms.sourcegitcommit: abe7fe9f3fbee8d12641433eeab623a4148ffed3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2020
ms.locfileid: "92185211"
---
# <a name="moving-the-pointer-drvmovepointer"></a>移动指针：DrvMovePointer

如果驱动程序中包含 [**DrvSetPointerShape**](/windows/win32/api/winddi/nf-winddi-drvsetpointershape) ，则还必须支持 [**DrvMovePointer**](/windows/win32/api/winddi/nf-winddi-drvmovepointer) 。 此函数将驱动程序托管指针移动到新位置。 由于 GDI 会序列化对指针函数的调用，因此在显示驱动程序中绘制任何线程时，不会调用 *DrvMovePointer* ，除非已在 [**lnk-devinfo**](/windows/win32/api/winddi/ns-winddi-devinfo) 结构中设置了 GCAPS_ASYNCMOVE 标志。

驱动程序应调用 [**EngMovePointer**](/windows/win32/api/winddi/nf-winddi-engmovepointer) ，使 GDI 可以在设备上移动引擎托管指针。 驱动程序请求 GDI 通过调用 [**EngSetPointerShape**](/windows/win32/api/winddi/nf-winddi-engsetpointershape)来管理游标。
