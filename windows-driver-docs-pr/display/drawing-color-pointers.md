---
title: 绘制彩色指针
description: 绘制彩色指针
keywords:
- 绘图指针 WDK Windows 2000 显示
- 显示驱动程序 WDK Windows 2000，指针
- 指针 WDK Windows 2000 显示
- 颜色指针 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23d102d92a7e88fc23d461fb34a7eec2bac67a04
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809191"
---
# <a name="drawing-color-pointers"></a>绘制彩色指针


## <span id="ddk_drawing_color_pointers_gg"></span><span id="DDK_DRAWING_COLOR_POINTERS_GG"></span>


以与单色指针相同的方式定义颜色指针 (即，作为包含 AND 部分和 XOR 部分的位图--请参阅 [指针绘图](pointer-drawing.md) 和 [绘制单色指针](drawing-monochrome-pointers.md)) 还支持透明和反转。

-   如果颜色位图为黑色 (索引 0) 并且和掩码值为1，则结果为 "透明"。

-   如果颜色位图为白色并且和掩码值为1，则结果为反转。

-   如果设备无法显示颜色，则可以将指针绘制为黑色和白色。

这些约定允许应用程序使用单色和单色显示的单个指针定义。

 

 





