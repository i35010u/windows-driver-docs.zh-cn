---
title: DirectDraw 图面
description: DirectDraw 图面
ms.assetid: be99b124-5193-4826-be28-ed6a132b84af
keywords:
- 绘图图面 WDK DirectDraw，关于曲面
- DirectDraw 图面上的 WDK Windows 2000 显示，关于图面
- 平面 DirectDraw，关于图面
- 功能位 WDK DirectDraw
- cap bits WDK DirectDraw
- 绘图图面 WDK DirectDraw
- DirectDraw 图面 WDK Windows 2000 显示
- 表面 WDK DirectDraw
- 表面 WDK DirectDraw，功能位
- 主要面
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be6408bb5be076d78025ac87d0361123326832c7
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065888"
---
# <a name="directdraw-surfaces"></a>DirectDraw 图面


## <span id="ddk_directdraw_surfaces_gg"></span><span id="DDK_DIRECTDRAW_SURFACES_GG"></span>


Microsoft DirectDraw 表面是 Microsoft DirectX graphics 中的基本图像单位。 它是特定宽度、高度和像素格式的像素的矩形集合;或包含 Microsoft Direct3D 的命令或顶点的缓冲区。 表面具有与之关联的、表示其行为和使用情况的位。 对于 short) ， *这些位称为 (* 或 *cap 位* 。 Cap 位表示其关联表面的预期用法，如保存纹素以用于呈现 (DDSCAPS \_ 纹理帽位) ，为三维呈现的目标 (DDSCAPS \_ 3DDEVICE) ，等等。 有关 surface cap 位的详细信息，请参阅 [**DDSCAPS**](/previous-versions/windows/hardware/drivers/ff550286(v=vs.85)) 结构。

*主要*表面是显示卡当前正在扫描到监视器上的表面。 有关主要表面的详细信息，请参阅 " [翻转](flipping.md) 和 [内存配置](memory-configurations.md) " 部分。

 

