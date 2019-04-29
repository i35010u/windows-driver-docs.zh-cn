---
title: 内存配置
description: 内存配置
ms.assetid: e3341854-13ce-4028-ad75-49e8189ac0f7
keywords:
- stride WDK DirectDraw
- 宣传 WDK DirectDraw
- WDK DirectDraw 的偏移量
- 绘制内存 WDK DirectDraw，堆
- DirectDraw 内存 WDK Windows 2000 显示堆
- WDK DirectDraw，堆内存
- 显示内存 WDK DirectDraw 堆
- 堆 WDK DirectDraw
- 堆分配内存
- VIDEOMEMORY
- WDK DirectDraw，内存堆分配的图面
- 绘制内存 WDK DirectDraw，配置选项
- DirectDraw 内存 WDK Windows 2000 显示中，配置选项
- 内存 WDK DirectDraw，配置选项
- 显示内存 WDK DirectDraw，配置选项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4d4392c1003927e679d97225da16c1c92a8d250
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370718"
---
# <a name="memory-configurations"></a>内存配置


## <span id="ddk_memory_configurations_gg"></span><span id="DDK_MEMORY_CONFIGURATIONS_GG"></span>


以下各节包含三种不同类型的内存配置：[线性](linear-memory-allocation.md)，[矩形](rectangular-memory-allocation.md)，并[混合](mixed-memory-allocation.md)显示内存分配。 每个部分包括示例代码可以进行修改以适应卡片的物理特征和，可以将其添加到分配的 HAL 显示内存堆。

对齐需求中所述[内存堆分配](memory-heap-allocation.md)主题可以应用于所有三种类型的内存配置。 线性通常使用更高效的内存比矩形内存应用程序因为按顺序存储行。 任何位置可以是访问轻松地通过不断前进或后退沿此线性范围。

 

 





