---
title: 控制指针 DrvSetPointerShape
description: 控制指针 DrvSetPointerShape
ms.assetid: 14d782de-5da8-40e9-a3e3-91d2588146e0
keywords:
- 显示绘图指针 WDK Windows 2000
- 显示驱动程序 WDK Windows 2000 中，指针
- 显示指针 WDK Windows 2000
- DrvSetPointerShape
- 指针 WDK Windows 2000 显示的形状
- 重新调整指针 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f2cf9b4c63d0f0be27413b3790b0f04237087f7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392658"
---
# <a name="controlling-the-pointer-drvsetpointershape"></a>控制指针：DrvSetPointerShape


## <span id="ddk_controlling_the_pointer_drvsetpointershape_gg"></span><span id="DDK_CONTROLLING_THE_POINTER_DRVSETPOINTERSHAPE_GG"></span>


如果显示驱动程序控制鼠标指针，则该驱动程序必须支持[ **DrvSetPointerShape** ](https://msdn.microsoft.com/library/windows/hardware/ff556289)以允许要进行更改的指针形状。 DrvSetPointerShape 调用生成以下结果：

1.  该函数中删除该驱动程序已在显示屏书写的任何现有指针。

2.  该函数将设置新的请求的形状，除非它是无法处理该形状。

3.  在调用的参数所指示的位置显示新的指针。

该驱动程序可以调用[ **EngSetPointerShape** ](https://msdn.microsoft.com/library/windows/hardware/ff565017)要具有 GDI 管理软件游标。

 

 





