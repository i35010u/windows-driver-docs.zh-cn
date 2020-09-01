---
title: 在 DirectDraw 中执行浮点运算
description: 在 DirectDraw 中执行浮点运算
ms.assetid: 2ce638e8-2d32-4692-8093-adb413bfbe52
keywords:
- 浮点运算 WDK DirectDraw
- 绘制 WDK DirectDraw，浮点运算
- DirectDraw WDK Windows 2000 显示，浮点操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f2f42490bda31d314b2c8ff5c2ca316f5506759
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067286"
---
# <a name="performing-floating-point-operations-in-directdraw"></a>在 DirectDraw 中执行浮点运算


## <span id="ddk_performing_floating_point_operations_in_directdraw_gg"></span><span id="DDK_PERFORMING_FLOATING_POINT_OPERATIONS_IN_DIRECTDRAW_GG"></span>


DirectDraw 驱动程序回调函数必须执行对 GDI 提供的 [**EngSaveFloatingPointState**](/windows/desktop/api/winddi/nf-winddi-engsavefloatingpointstate) 和 [**EngRestoreFloatingPointState**](/windows/desktop/api/winddi/nf-winddi-engrestorefloatingpointstate) 函数的调用之间的所有浮点运算。 也就是说，驱动程序的回调函数必须先保存浮点状态，然后才能执行浮点运算，并且在完成浮点运算时必须还原浮点状态。 有关浮点运算的详细信息，请参阅 [图形驱动程序函数中的浮点运算](floating-point-operations-in-graphics-driver-functions.md)。

 

