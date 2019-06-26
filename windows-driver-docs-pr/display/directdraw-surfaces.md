---
title: DirectDraw 图面
description: DirectDraw 图面
ms.assetid: be99b124-5193-4826-be28-ed6a132b84af
keywords:
- 绘图图面相 WDK DirectDraw 表面有关
- DirectDraw 图面 WDK Windows 2000 显示有关图面
- 关于曲面的图面 WDK DirectDraw
- 功能的位将 WDK DirectDraw
- 限制 bits WDK DirectDraw
- 绘图图面 WDK DirectDraw
- DirectDraw 图面 WDK Windows 2000 显示
- WDK DirectDraw 图面
- 显示 WDK DirectDraw，功能位
- 主图面 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 440d2c7f6162356df3419e578c4dce819e3f7e5f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379374"
---
# <a name="directdraw-surfaces"></a>DirectDraw 图面


## <span id="ddk_directdraw_surfaces_gg"></span><span id="DDK_DIRECTDRAW_SURFACES_GG"></span>


Microsoft DirectDraw Surface 是 Microsoft DirectX 图形中的基本映像单元。 它是任一矩形的像素为单位的特定宽度、 高度和像素格式; 集合或为 Microsoft Direct3D 中包含的命令或顶点的缓冲区。 图面有与之关联的位表示它们的行为和使用情况。 调用这些位*呈现功能 bits* (或*指针顶端才位*简称)。 Caps 位表示其关联的图面，如保存呈现的纹素的预期的用途 (DDSCAPS\_纹理 caps 位)，三维呈现为目标 (DDSCAPS\_3DDEVICE)，以及许多其他。 有关 surface caps 位的详细信息，请参阅[ **DDSCAPS** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550286(v=vs.85))结构。

*主*面是当前正在扫描出在显示卡到监视器的面。 有关主表面的详细信息，请参阅[Flipping](flipping.md)并[内存配置](memory-configurations.md)部分。

 

 





