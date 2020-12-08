---
title: AGP 支持
description: AGP 支持
keywords:
- AGP WDK DirectDraw，关于 AGP 支持
- 绘制 AGP 支持 WDK DirectDraw，关于 AGP 支持
- DirectDraw AGP 支持 WDK Windows 2000 显示，关于 AGP 支持
- 内存 WDK DirectDraw AGP，关于 AGP 支持
- 加速图形端口 WDK DirectDraw
- 显示内存 WDK DirectDraw
- 非本地显示内存 WDK DirectDraw
- 显示内存 WDK DirectDraw，关于 AGP 支持
- 非本地显示内存 WDK DirectDraw，关于非本地显示内存
- AGP WDK DirectDraw
- 绘制 AGP 支持 WDK DirectDraw
- DirectDraw AGP 支持 WDK Windows 2000 显示
- 内存 WDK DirectDraw AGP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40daee9b8d9115c210f1515baba53a4795120ebe
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810529"
---
# <a name="agp-support"></a>AGP 支持


## <span id="ddk_agp_support_gg"></span><span id="DDK_AGP_SUPPORT_GG"></span>


Microsoft DirectDraw 将 *加速图形端口 (AGP) 内存* 作为显示内存的子类。 此内存类型称为非 *本地显示内存*。 术语 "AGP 内存" 和 "非本地显示内存" 是从 DirectDraw 和 DirectDraw 驱动程序的角度来看的。

AGP 内存被视为显示内存的纯子类。 也就是说，如果驱动程序指示它支持 AGP 内存，则在大多数情况下，它必须具有相同的本地和非本地显示内存功能，尽管允许性能差异。 例外情况是设置了 DDCAPS2 \_ NONLOCALVIDMEMCAPS 标志，在这种情况下，非本地显示内存的 blt 功能可能与本地显示内存不同。

例如，如果驱动程序声明它可以通过显示内存进行纹理显示，则必须能够从本地和非本地显示内存中进行纹理。 Blitting 的处理方式类似。 导出源颜色键 blt 功能的驱动程序必须能够在非本地显示内存中对源颜色进行键控键控。 此规则有一个例外，就是可以阻止在非本地显示内存中分配某些表面类型。 例如，可以使用堆来防止覆盖面在 AGP 内存中被分配。

因为 AGP 内存被视为显示内存的子类，所以 DirectDraw 对于 AGP 内存没有单独的显示驱动程序入口点集。 现有的显示驱动程序调用用于 AGP 面和局部显示内存图面。 AGP 兼容的驱动程序必须检查传入的图面，以确定它们是在非本地还是本地显示内存中，并采取适当的措施。 Blts 从系统到 AGP (，反之亦然) 按照常规方式浏览 DirectDraw 仿真层，除非驱动程序支持系统到显示内存 Blts (，在这种情况下，它还必须支持系统到 AGP 传输) 。

驱动程序应尽可能多地设置 DDCAPS2 \_ TEXMANINNONLOCALVIDMEM 标志，因为在这种情况下，Direct3D 纹理管理器会在 AGP 内存 (而不是在系统内存) 中的表面的视频内存副本的备份映像。

本部分的其余部分讨论了使用 DirectDraw 非本地显示内存功能修改现有驱动程序以支持 AGP 内存所需的步骤。

 

 





