---
title: 在 DirectDraw 中执行浮点运算
description: 在 DirectDraw 中执行浮点运算
ms.assetid: 2ce638e8-2d32-4692-8093-adb413bfbe52
keywords:
- 浮点运算 WDK DirectDraw
- 绘制 WDK DirectDraw，浮点运算
- DirectDraw WDK Windows 2000 显示，浮点运算
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94fe18ca429ab07640306399adeab4ad35107466
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366402"
---
# <a name="performing-floating-point-operations-in-directdraw"></a>在 DirectDraw 中执行浮点运算


## <span id="ddk_performing_floating_point_operations_in_directdraw_gg"></span><span id="DDK_PERFORMING_FLOATING_POINT_OPERATIONS_IN_DIRECTDRAW_GG"></span>


DirectDraw 驱动程序回调函数必须执行的 GDI 提供调用之间的所有浮点运算[ **EngSaveFloatingPointState** ](https://msdn.microsoft.com/library/windows/hardware/ff565010)并[ **EngRestoreFloatingPointState** ](https://msdn.microsoft.com/library/windows/hardware/ff565006)函数。 也就是说，驱动程序的回调函数必须将保存在执行浮点运算之前的浮点状态和浮点操作完成时，必须还原的浮点状态。 有关浮点运算的详细信息，请参阅[图形驱动程序函数中的浮点操作](floating-point-operations-in-graphics-driver-functions.md)。

 

 





