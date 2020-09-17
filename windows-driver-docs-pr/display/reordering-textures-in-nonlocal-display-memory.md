---
title: 将非本地显示内存中的纹理重新排序
description: 将非本地显示内存中的纹理重新排序
ms.assetid: b4b4c478-7034-4ff9-8cb2-f86baffd89f7
keywords:
- 显示内存 WDK DirectDraw，重新排序纹理
- 非本地显示内存 WDK DirectDraw，重新排序纹理
- AGP WDK DirectDraw，重新排序纹理
- 绘制 AGP 支持 WDK DirectDraw，重新排序纹理
- DirectDraw AGP 支持 WDK Windows 2000 显示，重新排序纹理
- 内存 WDK DirectDraw AGP，重新排序纹理
- 重新排序纹理 WDK DirectDraw
- DDCAPS2_SYSTONONLOCAL_AS_SYSTOLOCAL
- 纹理 WDK DirectDraw，重新排序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe6b961e59a0132a691067bb4e91cdd6890bea7f
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716018"
---
# <a name="reordering-textures-in-nonlocal-display-memory"></a>将非本地显示内存中的纹理重新排序


## <span id="ddk_reordering_textures_in_nonlocal_display_memory_gg"></span><span id="DDK_REORDERING_TEXTURES_IN_NONLOCAL_DISPLAY_MEMORY_GG"></span>


在某些特殊情况下，驱动程序编写器可能需要在 AGP 内存中重新排序纹理，以允许更有效的纹理管理。 DDCAPS2 \_ SYSTONONLOCAL \_ AS \_ SYSTOLOCAL 标志发出的信号表明驱动程序可支持 blts 从 (系统内存副本的表面) 到非本地视频内存（使用为本地视频内存 blts 指定的所有相同 cap）。

\_ \_ \_ 仅当设置 DDCAPS2 NONLOCALVIDMEMCAPS 标志时，DDCAPS2 SYSTONONLOCAL AS SYSTOLOCAL 标志才有效 \_ 。 如果 \_ \_ 设置了 DDCAPS2 SYSTONONLOCAL AS \_ SYSTOLOCAL，则 \_ 驱动程序必须设置 DDCAPS CANBLTSYSMEM 标志，并且所有关联的后备 surface blt cap 必须正确。 DDCAPS2 \_ SYSTONONLOCAL \_ AS \_ SYSTOLOCAL 表示 surface TO 视频 memory DDCAPS blt cap 还适用于后备面到非本地视频内存 blts。 例如，假定[**DDCORECAPS**](/windows/win32/api/ddrawi/ns-ddrawi-_ddcorecaps)结构的**dwSVBCaps**、 **dwSVBCKeyCaps**、 **dwSVBFXCaps**和**dwSVBRops**成员正确填充。 从后备 surface 到非本地内存的任何 blt 都将传递给驱动程序。

**注意**   此功能旨在使驱动程序本身能够有效地对纹理进行排序。 这并 *不* 意味着可以将硬件写入 AGP 内存。 当前不支持将硬件直接写入 AGP 内存。

 

 

