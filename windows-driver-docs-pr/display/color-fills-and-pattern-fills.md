---
title: 颜色填充和模式填充
description: 颜色填充和模式填充
keywords:
- 绘制 blt WDK DirectDraw，颜色填充
- DirectDraw blitting WDK Windows 2000 显示，颜色填充
- blitting WDK DirectDraw，颜色填充
- blt WDK DirectDraw，颜色填充
- surface DirectDraw，blitting
- 绘制 blt WDK DirectDraw，模式填充
- DirectDraw blitting WDK Windows 2000 显示，模式填充
- blitting WDK DirectDraw，模式填充
- blt WDK DirectDraw，模式填充
- 填充 WDK DirectDraw 的颜色
- 模式填充 WDK DirectDraw
- 填充颜色 WDK DirectDraw
- 填充模式 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88a22282ceb3bd26a390580f8a34e665f4815931
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810287"
---
# <a name="color-fills-and-pattern-fills"></a>颜色填充和模式填充


## <span id="ddk_color_fills_and_pattern_fills_gg"></span><span id="DDK_COLOR_FILLS_AND_PATTERN_FILLS_GG"></span>


颜色填充（如矩形所述）使用特定颜色填充屏幕区域。 在大多数卡上，只需显示内存的地址、矩形的尺寸和颜色。 某些卡需要开始和结束 X 和 Y 坐标。 请注意，Windows 会自动删除这些坐标中的最后一行。 例如，当从0到640的编号时，Windows 会删除第640行。

某些卡使用图案填充，这可以实现与颜色填充相同的效果。 8 x 8 像素区域 (模式) 构成所需的颜色，该模式用于填充指定的区域。 模式设置为等于所需的颜色，并与颜色填充完全相同。 模式填充使用四种不同的颜色，可以混合使用这些颜色，从而减少必要说明的数量。

 

 





