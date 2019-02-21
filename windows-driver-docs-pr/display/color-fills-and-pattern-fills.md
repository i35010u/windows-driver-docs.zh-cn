---
title: 颜色填充和模式填充
description: 颜色填充和模式填充
ms.assetid: 6e597405-e40f-4cb8-b177-896681745e00
keywords:
- 绘制 blt WDK DirectDraw，颜色填充
- DirectDraw 图阵 WDK Windows 2000 显示颜色填充
- 图 WDK DirectDraw 阵，颜色填充
- blt WDK DirectDraw，颜色填充
- WDK DirectDraw 图阵的图面
- 绘制 blt WDK DirectDraw 图案填充
- DirectDraw 图阵 WDK Windows 2000 显示模式填充
- 平面闪 WDK DirectDraw，图案填充
- blt WDK DirectDraw 图案填充
- 颜色填充 WDK DirectDraw
- 图案填充 WDK DirectDraw
- 填充颜色 WDK DirectDraw
- 填充模式 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd9893a8932f712f26b16960bdc1540949c25c39
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534857"
---
# <a name="color-fills-and-pattern-fills"></a>颜色填充和模式填充


## <span id="ddk_color_fills_and_pattern_fills_gg"></span><span id="DDK_COLOR_FILLS_AND_PATTERN_FILLS_GG"></span>


所描述的矩形，颜色填充，填充使用特定颜色屏幕区域。 大多数卡，只显示内存地址上所需的维度的矩形和的颜色。 某些卡需要开始和结束 X 和 Y 坐标。 请注意，Windows 将自动删除这些坐标的最后一行。 例如，当它们的编号介于 0 到 640，Windows 将删除行 640。

某些卡使用图案填充，这样可以实现与颜色填充相同的功能。 像素 （模式） 中的 8 x 8 区域构成所需的颜色，并且该模式用于填充指定的区域。 该模式设置为等于所需属性和填充颜色填充相同的颜色。 图案填充采用四个单独的颜色可以混合，减少必要说明的数量。

 

 





