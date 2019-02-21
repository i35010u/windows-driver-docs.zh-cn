---
title: AGP 支持
description: AGP 支持
ms.assetid: 05a2f942-4374-421e-8292-d122f9fe3571
keywords:
- AGP WDK DirectDraw，有关 AGP 支持
- 绘制 AGP 支持 WDK DirectDraw AGP 支持
- DirectDraw AGP 支持 WDK Windows 2000 显示，有关 AGP 支持
- WDK DirectDraw AGP 想起 AGP 支持
- 加速的图形端口 WDK DirectDraw
- 显示内存 WDK DirectDraw
- 非本地显示内存 WDK DirectDraw
- 显示内存 WDK DirectDraw AGP 支持
- 非本地显示内存 WDK DirectDraw 有关非本地显示内存
- AGP WDK DirectDraw
- 绘制 AGP 支持 WDK DirectDraw
- DirectDraw AGP 支持 WDK Windows 2000 显示
- 内存 WDK DirectDraw AGP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 83b375f6a54598368728ca7a2ce15a5b64c2115b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534589"
---
# <a name="agp-support"></a>AGP 支持


## <span id="ddk_agp_support_gg"></span><span id="DDK_AGP_SUPPORT_GG"></span>


将 Microsoft DirectDraw*加速图形端口 (AGP) 内存*作为显示内存的子类。 此内存类型被称为*非本地显示内存*。 条款 AGP 内存和非本地显示内存是从 DirectDraw 和 DirectDraw 的角度来看同义词驱动程序。

AGP 内存被视为纯显示内存的子类。 即如果驱动程序表明它支持 AGP 内存，在大多数情况下它必须具有相同的功能功能对于显示本地和非本地内存，但允许性能差异。 例外情况是如果 DDCAPS2\_NONLOCALVIDMEMCAPS 标志设置，则非本地的 blt 功能在这种情况下显示内存可能不同于本地显示内存。

例如，如果驱动程序表明它可以从显示内存纹理，它必须能够为纹理从这两个显示本地和非本地内存。 平面闪处理方式类似。 驱动程序，导出源颜色关键 blt 功能必须能够执行操作的源的颜色相匹配 blt 到和从非本地显示内存。 此规则的一个例外是，则可以阻止某些图面类型分配非本地显示内存中。 例如，就可以使用堆以防止覆盖面分配 AGP 内存中。

由于 AGP 内存视为显示内存的子类，DirectDraw 有没有单独的一组 AGP 内存的显示驱动程序入口点。 现有的显示驱动程序调用用于 AGP 图面和本地显示内存图面。 是的 AGP 兼容驱动程序必须检查传入的图面，以确定它们是否在非本地或本地的显示内存中，并采取相应措施。 从系统到 AGP （反之亦然） Blts 经历按正常方式 DirectDraw 仿真层，除非驱动程序支持系统显示内存 blts （在此情况下它必须还支持系统 AGP 传输）。

驱动程序应设置 DDCAPS2\_TEXMANINNONLOCALVIDMEM 标志尽最大可能因为 Direct3D 纹理管理器在 AGP 内存 （而不是系统内存） 中保存的视频内存副本的一个面其后备图像时出现这种情况。

本部分的其余部分讨论需要修改现有的驱动程序支持 AGP 内存使用 DirectDraw 非本地显示内存中功能的步骤。

 

 





