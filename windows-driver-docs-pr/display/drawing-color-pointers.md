---
title: 绘制颜色指针
description: 绘制颜色指针
ms.assetid: f2791ccc-3d9e-46f0-bc70-051ac298c1ee
keywords:
- 显示绘图指针 WDK Windows 2000
- 显示驱动程序 WDK Windows 2000 中，指针
- 显示指针 WDK Windows 2000
- 显示颜色指针 WDK Windows 2000
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49424ca9fd9b40b375da98debfb79bdb3bfb98a3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520198"
---
# <a name="drawing-color-pointers"></a>绘制颜色指针


## <span id="ddk_drawing_color_pointers_gg"></span><span id="DDK_DRAWING_COLOR_POINTERS_GG"></span>


单色指针相同的方式定义的颜色指针 (也就是说，作为包括 AND 部分和 XOR 部分-一个位图，请参阅[指针绘制](pointer-drawing.md)并[绘图单色指针](drawing-monochrome-pointers.md)) 还支持透明度和反转。

-   如果颜色位图为黑色 （索引 0） 和 AND 掩码值为 1，则结果为透明度。

-   如果颜色位图为白色，AND 掩码值为 1，则结果将是反转。

-   如果设备不能显示颜色，然后一个指针，可以绘制为黑色和白色。

这些约定允许应用程序使用单个指针定义的颜色和单色显示。

 

 





