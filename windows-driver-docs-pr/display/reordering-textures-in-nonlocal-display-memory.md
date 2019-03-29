---
title: 将非本地显示内存中的纹理重新排序
description: 将非本地显示内存中的纹理重新排序
ms.assetid: b4b4c478-7034-4ff9-8cb2-f86baffd89f7
keywords:
- 显示内存 WDK DirectDraw，纹理的重新排序
- 非本地显示内存 WDK DirectDraw，纹理的重新排序
- AGP WDK DirectDraw，纹理的重新排序
- 绘制 AGP 支持 WDK DirectDraw，纹理的重新排序
- DirectDraw AGP 支持 WDK Windows 2000 显示，纹理的重新排序
- 内存 WDK DirectDraw AGP，纹理的重新排序
- 纹理 WDK DirectDraw 的重新排序
- DDCAPS2_SYSTONONLOCAL_AS_SYSTOLOCAL
- 纹理 WDK DirectDraw 重新排序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f31af9f68d724f171f2b69aa8bb914a6ed9c5955
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566692"
---
# <a name="reordering-textures-in-nonlocal-display-memory"></a>将非本地显示内存中的纹理重新排序


## <span id="ddk_reordering_textures_in_nonlocal_display_memory_gg"></span><span id="DDK_REORDERING_TEXTURES_IN_NONLOCAL_DISPLAY_MEMORY_GG"></span>


有特殊的情况下，驱动程序编写器可能需要重新排序 AGP 内存，以允许更有效的纹理管理中的纹理。 DDCAPS2\_SYSTONONLOCAL\_AS\_SYSTOLOCAL 标志指示该驱动程序可以从备份到非本地使用的完全为指定的上限的视频内存的图面 （系统内存复制的图面） 支持 blts备份到本地的视频内存 blts 图面上的内存。

DDCAPS2\_SYSTONONLOCAL\_AS\_SYSTOLOCAL 标志是有效的仅当 DDCAPS2\_NONLOCALVIDMEMCAPS 标志设置。 如果 DDCAPS2\_SYSTONONLOCAL\_AS\_SYSTOLOCAL 是设置，那么 DDCAPS\_CANBLTSYSMEM 标志必须设置驱动程序和所有相关的后备图面上 blt caps 必须正确。 DDCAPS2\_SYSTONONLOCAL\_AS\_SYSTOLOCAL 表示 DDCAPS blt 上限也适用于备份到非本地的视频内存 blts 面上的视频内存的后备面。 例如， **dwSVBCaps**， **dwSVBCKeyCaps**， **dwSVBFXCaps**，以及**dwSVBRops**成员[ **DDCORECAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff549248)假定结构正确填充。 从后备面任何 blt 匹配这些 caps 位的非本地内存传递给驱动程序。

**请注意**  此功能旨在使驱动程序本身为纹理的有效重新排序。 这是*不*意味着两者硬件可以写入 AGP 内存。 目前不支持直接写入 AGP 内存的硬件。

 

 

 





