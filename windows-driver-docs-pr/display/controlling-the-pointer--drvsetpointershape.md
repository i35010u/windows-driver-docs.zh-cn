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
ms.openlocfilehash: e30d375aaeaa6df6b56609eae1517fc2ec6d72c1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370291"
---
# <a name="controlling-the-pointer-drvsetpointershape"></a>控制指针：DrvSetPointerShape


## <span id="ddk_controlling_the_pointer_drvsetpointershape_gg"></span><span id="DDK_CONTROLLING_THE_POINTER_DRVSETPOINTERSHAPE_GG"></span>


如果显示驱动程序控制鼠标指针，则该驱动程序必须支持[ **DrvSetPointerShape** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsetpointershape)以允许要进行更改的指针形状。 DrvSetPointerShape 调用生成以下结果：

1.  该函数中删除该驱动程序已在显示屏书写的任何现有指针。

2.  该函数将设置新的请求的形状，除非它是无法处理该形状。

3.  在调用的参数所指示的位置显示新的指针。

该驱动程序可以调用[ **EngSetPointerShape** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engsetpointershape)要具有 GDI 管理软件游标。

 

 





