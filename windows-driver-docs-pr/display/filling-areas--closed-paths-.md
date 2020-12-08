---
title: 填充区域（封闭路径）
description: 填充区域（封闭路径）
keywords:
- GDI WDK Windows 2000 显示、路径、闭合
- 图形驱动程序 WDK Windows 2000 显示、路径、闭合
- 绘制 WDK GDI，路径，闭合
- 填充路径 WDK GDI，已关闭
- 路径 WDK GDI，已关闭
- 闭合路径 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c21cf2c9ec4aa7c8e892f604595c308c0dcde15e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808887"
---
# <a name="filling-areas-closed-paths"></a>填充区域（封闭路径）


## <span id="ddk_filling_areas__28_closed_paths_29_gg"></span><span id="DDK_FILLING_AREAS__28_CLOSED_PATHS_29_GG"></span>


与在线条绘图中一样，用于填充的像素被视为位于整数坐标。 区域中的每个扫描行都在左侧和右侧用路径的段向右界定。 在 "填充" 区域中，将在左边框和右边框之间的像素被视为。 完全位于左边框上的像素也在内，但会排除完全在右边框上的像素。 如果上边框是水平的，则边框上完全相同的任何像素均在内，而与下边框完全相同的像素则被排除。

下图显示了如何根据区域的左右边框确定填充区域中包含的像素。 从数学上说，区域被认为是左侧和顶部的 "关闭"，右侧和底部的 "打开"。

![阐释如何确定填充区域中包含的像素的关系图](images/fillbdy.png)

上面所述的用于填充区域 x 轴的约定也适用于 y 轴，方法是将左边框替换为上边框，将右边框替换为下边框。

 

 





