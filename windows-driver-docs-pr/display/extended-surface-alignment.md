---
title: 扩展图面对齐
description: 扩展图面对齐
keywords:
- 绘制扩展图面对齐 WDK DirectDraw
- DirectDraw 扩展图面对齐 WDK Windows 2000 显示器
- surface DirectDraw，扩展对齐
- 扩展的图面对齐 WDK DirectDraw
- 堆 WDK DirectDraw
- 校准 WDK DirectDraw 扩展图面
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 425f9a2b9d92094e2473306593065e56d7814155
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838291"
---
# <a name="extended-surface-alignment"></a>扩展图面对齐


## <span id="ddk_extended_surface_alignment_gg"></span><span id="DDK_EXTENDED_SURFACE_ALIGNMENT_GG"></span>


Microsoft DirectDraw 支持每个堆的图面对齐要求。 此支持是在 Microsoft DirectX 5.0 中引入的。 驱动程序可以为矩形堆指定 X 和 Y 对齐，并为线性堆指定间距和开始偏移对齐方式。 这些对齐方式对于不同的表面类型可能有所不同。

某些显示硬件无法在原子操作中设置其开始显示偏移。 显示期间开始时，当驱动程序只是通过设置值的一半时，此类硬件就可以锁住新的显示起始偏移量。 DirectDraw 现在允许驱动程序指定可见后台缓冲区的对齐要求。 某些硬件可能能够表示可能可见的后台缓冲区的对齐要求，这些缓冲区强制开始显示偏移是只需要一个寄存器写入的值。 此方法可帮助避免偶尔出现的闪烁，如果主图面以较高的频率进行翻转，则会看到此闪烁。

 

 





