---
title: 扩展图面功能标志
description: 扩展图面功能标志
ms.assetid: 197d899e-57ab-40f8-9c09-440c2dc6197c
keywords:
- 绘图图面上的扩展的功能 WDK DirectDraw，标志
- DirectDraw 扩展表面功能 WDK Windows 2000 显示，标志
- 扩展表面功能 WDK DirectDraw 标志
- 标记扩展面 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 744577721cbcd94a1249daf10b0b6077a083cc9f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381862"
---
# <a name="extended-surface-capability-flags"></a>扩展图面功能标志


## <span id="ddk_extended_surface_capability_flags_gg"></span><span id="DDK_EXTENDED_SURFACE_CAPABILITY_FLAGS_GG"></span>


应用程序设置相应的标记扩展的图面功能添加到最新版本的 DirectDraw 都对驱动程序可见**dwCaps2**的成员[ **DDSCAPS2**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550292(v=vs.85))结构。

应用程序可以仅设置 DDSCAPS2\_HARDWAREDEINTERLACE 标志结合 DDSCAPS\_覆盖标志。 如果驱动程序会看到此标志设置为**用于 CreateSurface**时间，这意味着 DirectDraw 需要驱动程序将执行会尽一切努力匹配硬件的视频端口帧速率设备帧速率。

DDSCAPS2\_HINTDYNAMIC、 DDSCAPS2\_HINTSTATIC 和 DDSCAPS2\_不透明的标志是在应用程序设置的提示**用于 CreateSurface**告知驱动程序应用程序的计划的时间执行与图面。 DDSCAPS2\_HINTDYNAMIC 标志意味着应用程序将频繁地更新图面。 DDSCAPS2\_HINTSTATIC 标志意味着应用程序将很少更新图面，但仍需要访问权限。 这意味着该驱动程序必须能够允许锁表面上看，这可能涉及一些隐藏的解压缩和压缩的步骤。 DDSCAPS2\_不透明标志意味着应用程序将永远不会锁定 blt，或更新该图面生命周期的其余部分的图面。 该驱动程序可以自由地压缩或重新排序在图面，而无需不断将其解压缩。

**请注意**  驱动程序不需要设置这些标志以启用它们。 DirectDraw 只是将这些位传递到驱动程序时[ *DdCreateSurface* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))调用。

 

驱动程序编写人员可能想要使用的扩展的堆限制功能 (中所述[扩展堆限制](extended-heap-restrictions.md)) 的 DirectDraw 来自动放置 DDSCAPS2\_中的不透明纹理优化堆。 这是完全取决于驱动程序开发人员。

DDSCAPS2\_HINTDYNAMIC、 DDSCAPS2\_HINTSTATIC 和 DDSCAPS2\_Microsoft DirectX 驱动程序开发工具包 (DDK) 文档中的更详细地介绍了不透明的标志。

DDSCAPS2\_TEXTUREMANAGE 标志不是与驱动程序相关。 此标志告知 DirectX 运行时，它负责从后备面以显示为相应的内存，迁移在图面，若要启用加速 3D 纹理。

 

 





