---
title: 控制指针 DrvSetPointerShape
description: 控制指针 DrvSetPointerShape
ms.assetid: 14d782de-5da8-40e9-a3e3-91d2588146e0
keywords:
- 绘图指针 WDK Windows 2000 显示
- 显示驱动程序 WDK Windows 2000，指针
- 指针 WDK Windows 2000 显示
- DrvSetPointerShape
- 指针 WDK Windows 2000 显示的形状
- 改变指针 WDK Windows 2000 显示的形状
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a547bcd2df13cf2f293f38af58793dd0775f79e
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715364"
---
# <a name="controlling-the-pointer-drvsetpointershape"></a>控制指针：DrvSetPointerShape


## <span id="ddk_controlling_the_pointer_drvsetpointershape_gg"></span><span id="DDK_CONTROLLING_THE_POINTER_DRVSETPOINTERSHAPE_GG"></span>


如果显示驱动程序控制指针，则驱动程序必须支持 [**DrvSetPointerShape**](/windows/win32/api/winddi/nf-winddi-drvsetpointershape) 以允许更改指针形状。 对 DrvSetPointerShape 的调用会产生以下结果：

1.  函数删除驱动程序已在显示器上绘制的任何现有指针。

2.  函数设置新请求的形状，除非它无法处理形状。

3.  新指针显示在调用的参数所指示的位置。

驱动程序可以调用 [**EngSetPointerShape**](/windows/win32/api/winddi/nf-winddi-engsetpointershape) ，使 GDI 管理软件游标。

 

