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
ms.openlocfilehash: ef6e17798c9c84903993f7107ab1e1039497b497
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064360"
---
# <a name="controlling-the-pointer-drvsetpointershape"></a>控制指针：DrvSetPointerShape


## <span id="ddk_controlling_the_pointer_drvsetpointershape_gg"></span><span id="DDK_CONTROLLING_THE_POINTER_DRVSETPOINTERSHAPE_GG"></span>


如果显示驱动程序控制指针，则驱动程序必须支持 [**DrvSetPointerShape**](/windows/desktop/api/winddi/nf-winddi-drvsetpointershape) 以允许更改指针形状。 对 DrvSetPointerShape 的调用会产生以下结果：

1.  函数删除驱动程序已在显示器上绘制的任何现有指针。

2.  函数设置新请求的形状，除非它无法处理形状。

3.  新指针显示在调用的参数所指示的位置。

驱动程序可以调用 [**EngSetPointerShape**](/windows/desktop/api/winddi/nf-winddi-engsetpointershape) ，使 GDI 管理软件游标。

 

