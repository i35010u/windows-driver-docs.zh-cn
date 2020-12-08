---
title: 显示内存
description: 显示内存
keywords:
- 显示内存 WDK DirectDraw，关于显示内存
- 绘制内存 WDK DirectDraw，关于显示内存
- DirectDraw 内存 WDK Windows 2000 显示，关于内存
- 内存 WDK DirectDraw，关于内存
- 绘制内存 WDK DirectDraw
- DirectDraw 内存 WDK Windows 2000 显示
- 内存 WDK DirectDraw
- 显示内存 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63a805f597d6f8fa5cc0dac96b810f93f7df84cf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809247"
---
# <a name="display-memory"></a>显示内存


## <span id="ddk_display_memory_gg"></span><span id="DDK_DISPLAY_MEMORY_GG"></span>


通常，将尽可能多的显示内存分配到 DirectDraw 会提高显示性能，并使游戏和其他 DirectDraw 应用程序更快地运行，并获得更好的视觉对象质量。

通常情况下，显示卡的间距设置为显示的宽度，以便不会将任何内存浪费给右 (在概念上) 前台缓冲区。 这会在可用于其他表面的概念底部留下一个空闲区。 在这种情况下，内存访问非常简单，因为一个指针可以引用可访问的显示内存的整个区域。

如果螺距大于主图面的宽度，则会浪费前台缓冲区的概念右侧的内存。 这必须作为单独的矩形堆回收，而不考虑卡上的内存是线性还是矩形。  (即使内存是线性的，某些显示驱动程序也会修复这种 blitter 的速度。 仅可将内存作为单独的堆回收，而不是重写驱动程序。 ) 

 

 





