---
title: 位图传送
description: 位图传送
ms.assetid: d9cbe939-957d-48e0-8427-d2c1ca0a9dd6
keywords:
- blt WDK DirectDraw
- 绘制 blt WDK DirectDraw，有关平面闪
- 有关平面闪 DirectDraw 图阵 WDK Windows 2000 显示
- 有关平面闪平面 WDK DirectDraw 闪
- WDK DirectDraw 图阵的图面
- 绘制 blt WDK DirectDraw
- DirectDraw 图阵 WDK Windows 2000 显示
- 平面闪 WDK DirectDraw
- blt WDK DirectDraw，有关平面闪
- DdBlt
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04ae0a0c05c630a09bea15e02b39b3005c69741f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566061"
---
# <a name="blitting"></a>位图传送


## <span id="ddk_blitting_gg"></span><span id="DDK_BLITTING_GG"></span>


如果 blt 一个面中发生的情况，源和目标区域重叠时，必须确定正确方向，以避免覆盖之前将其复制的源的一部分。 这可以使用两个潜在的起始点在对角面完成。 所有需要 blt 引擎是位置和维度的每个映像。

尽可能将一切应进行实际 blt 提高速度。 复制代码，以避免 IF 语句的部分可能会使速度更快，例如驱动程序。 或许这种技术的最佳实现是将代码放入一个宏并使用它在不同的位置，而无需进行函数调用。 有关详细信息，请参阅[ *DdBlt*](https://msdn.microsoft.com/library/windows/hardware/ff549205)。

 

 





