---
title: 扩展图面功能标志
description: 扩展图面功能标志
keywords:
- 绘制扩展 surface 功能 WDK DirectDraw，标志
- DirectDraw 扩展 surface 功能 WDK Windows 2000 显示，标志
- 扩展 surface 功能 WDK DirectDraw，标志
- 标志 WDK DirectDraw 扩展图面
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f234f3e3daff937c786ca01588e8635f0adb33f6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817407"
---
# <a name="extended-surface-capability-flags"></a>扩展图面功能标志


## <span id="ddk_extended_surface_capability_flags_gg"></span><span id="DDK_EXTENDED_SURFACE_CAPABILITY_FLAGS_GG"></span>


当应用程序在 [**DDSCAPS2**](/previous-versions/windows/hardware/drivers/ff550292(v=vs.85))结构的 **dwCaps2** 成员中设置相应的标志时，添加到最新版本 DirectDraw 的扩展 surface 功能将对驱动程序可见。

应用程序只能 \_ 与 DDSCAPS 叠加标志一起设置 DDSCAPS2 HARDWAREDEINTERLACE 标志 \_ 。 如果驱动程序在 **CreateSurface** 时发现此标志已设置，则表示 DirectDraw 需要驱动程序将执行任何必要的操作，以便将硬件视频端口帧速率与设备帧速率相匹配。

DDSCAPS2 \_ HINTDYNAMIC、DDSCAPS2 \_ HINTSTATIC 和 DDSCAPS2 \_ 不透明标志是应用程序在 **CreateSurface** 时间设置的提示，该提示告知驱动程序应用程序计划如何处理该图面。 DDSCAPS2 \_ HINTDYNAMIC 标志表示应用程序将经常更新图面。 DDSCAPS2 \_ HINTSTATIC 标志表示应用程序很少更新图面，但仍需要访问权限。 这意味着驱动程序必须能够在表面上允许锁定，这可能涉及到一些隐藏的解压缩和压缩步骤。 DDSCAPS2 \_ 不透明标志表示应用程序永远不会锁定、blt 或更新该图面的生存期的其余部分。 该驱动程序可自由压缩或重新排序，无需对其进行解压缩。

**注意**   驱动程序无需设置这些标志即可启用它们。 DirectDraw 仅在调用 [*DdCreateSurface*](/previous-versions/windows/hardware/drivers/ff549263(v=vs.85)) 时将这些位传递给驱动程序。

 

驱动程序编写器可能想要使用扩展堆 [限制](extended-heap-restrictions.md))  (中所述的扩展堆限制功能，以自动将 DDSCAPS2 不 \_ 透明纹理置于优化堆中。 这完全取决于驱动程序开发人员。

\_ \_ \_ (DDK) 文档中更详细地介绍了 DDSCAPS2 HINTDYNAMIC、DDSCAPS2 HINTSTATIC 和 DDSCAPS2 不透明标志。

DDSCAPS2 \_ TEXTUREMANAGE 标志与驱动程序无关。 此标志通知 DirectX 运行时它负责从后备面移动图面，以显示内存（根据需要）以启用加速的3D 纹理。

 

