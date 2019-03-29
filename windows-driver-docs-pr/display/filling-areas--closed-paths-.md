---
title: 填充区域（封闭路径）
description: 填充区域（封闭路径）
ms.assetid: 9dda1f0f-90e7-480b-aaeb-cb7781a1fe6c
keywords:
- GDI WDK Windows 2000 显示路径关闭
- 显示的图形驱动程序 WDK Windows 2000，路径，关闭
- 绘制 WDK GDI，路径，关闭
- 填充路径 WDK GDI，关闭
- 路径 WDK GDI 关闭
- 闭合的路径 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eeda151274b9a402f70d2263f5d106ead8c52805
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565283"
---
# <a name="filling-areas-closed-paths"></a>填充区域（封闭路径）


## <span id="ddk_filling_areas__28_closed_paths_29_gg"></span><span id="DDK_FILLING_AREAS__28_CLOSED_PATHS_29_GG"></span>


如线条图形中所示填充的像素被视为处于整数坐标。 在左侧和右侧的路径段界定一个区域中的每个扫描行。 左和右边框之间的像素被视为内部的填充区域。 完全位于左边框的像素为单位还有内，但是右边框上完全排除。 如果完全水平上边框，完全上边框的任何像素都位于内时不完全上的下边框的像素。

下图显示了如何将包含在填充区域的像素确定相对于左侧和右侧的区域的边框。 从数学上所述，在区域被视为"关闭"的左侧和顶部，并使"打开"的右侧和底部。

![说明确定包含填充区域的像素的关系图](images/fillbdy.png)

上面所述的填充区域的 x 轴的约定也适用于 y 轴，只需替换与上边框和右边框与下边框的左边的框。

 

 





