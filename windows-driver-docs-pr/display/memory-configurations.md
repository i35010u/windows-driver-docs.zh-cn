---
title: 内存配置
description: 内存配置
keywords:
- 步幅 WDK DirectDraw
- 音调 WDK DirectDraw
- 偏移 WDK DirectDraw
- 绘制内存 WDK DirectDraw，堆
- DirectDraw 内存 WDK Windows 2000 显示，堆
- 内存 WDK DirectDraw，堆
- 显示内存 WDK DirectDraw，堆
- 堆 WDK DirectDraw
- 分配内存堆
- VIDEOMEMORY
- 表面 WDK DirectDraw，内存堆分配
- 绘制内存 WDK DirectDraw，配置选项
- DirectDraw 内存 WDK Windows 2000 显示，配置选项
- 内存 WDK DirectDraw，配置选项
- 显示内存 WDK DirectDraw，配置选项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2271cb4384a31b6380e60fbc51aec1f87bc35146
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813221"
---
# <a name="memory-configurations"></a>内存配置


## <span id="ddk_memory_configurations_gg"></span><span id="DDK_MEMORY_CONFIGURATIONS_GG"></span>


以下各节包含三种不同类型的内存配置： [线性](linear-memory-allocation.md)、 [矩形](rectangular-memory-allocation.md)和 [混合](mixed-memory-allocation.md) 显示内存分配。 每个部分都包含可根据卡的物理特征进行修改的示例代码，可以将其添加到 HAL 以分配显示内存堆。

[内存堆分配](memory-heap-allocation.md)主题中所述的对齐要求适用于三种类型的内存配置中的任何一种。 通常，应用程序比矩形内存更有效地使用线性内存，因为行按顺序存储。 可以通过在此线性范围内向前或向后移动来轻松访问任何位置。

 

 





