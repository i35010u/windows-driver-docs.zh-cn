---
title: 使用 ks.graph
description: 使用 ks.graph
ms.assetid: 05dcd5d3-fac6-4af5-8149-955435fb016f
keywords:
- 内核调试，显示一个图形流式处理
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea6be6966026bc039c0ffbf3706da9c247b305f0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367975"
---
# <a name="using-ksgraph"></a>使用 !ks.graph


[ **！ Ks.graph** ](-ks-graph.md)命令是一个流式处理扩展插件模块的内核中功能最强大的扩展命令。 此命令显示整个关系图的图片在内核模式下从任何给定的起始点。

在运行前[ **！ ks.graph**](-ks-graph.md)，可能想要启用能够处于活动状态的所有库扩展。 若要执行此操作，请发出[ **！ ks.libexts enableall** ](-ks-libexts.md)命令。 输出 **！ ks.graph**按拓扑结构上排序顺序将内核模式关系图的文本说明。 下面是一个示例：

```dbgcmd
kd> !graph ffa0c6d4 7
Attempting a graph build on ffa0c6d4...  Please be patient...
Graph With Starting Point ffa0c6d4:
"usbaudio" Filter ffaaa768, Child Factories 2
    Output Factory 0:
        Pin ffb1caf0 (File 811deeb8, -> "splitter" ffa8b008) Irps(q/p) = 7, 1
```

此示例显示在其中两个 Sndrec32.exe 捕获来自电报 USB 麦克风捕获图形。 每个单独的记录开始 (在上面的部分 usbaudio) 的名称和筛选器上显示的筛选器地址 (0xFFAAA768) 和子 pin 工厂 (2) 的数量。

下面每个条目，每个工厂枚举并列出的每个 pin 实例 (0xFFB1CAF0)、 文件对象 (0x811DEEB8) 相对应的每个实例、 连接的方向，该连接的目标的地址和地址目标 pin (0xFFA8B008)。 此外会显示每个固定数量的排队 (7) 和挂起的 Irp (1)。

建立连接，具有正向符号 (-&gt;) 指示 pin 是输出插针，连接到输入插针。 具有反方向符号的连接 (&lt;-)，但是，输入插针，并且显示连接的来源。 输出将继续，如下所示：

```dbgcmd
"splitter" Filter ffa0c660, Child Factories 2
    Output Factory 0:
        Pin 81250008 (File ffb10028, -> "kmixer" 8123c000) Irps(q/p) = 3, 0
        Pin 811df9c0 (File ffaaf2f0, -> "kmixer" 81236000) Irps(q/p) = 3, 0
    Input Factory 1:
        Pin ffa8b008 (File ffb26d68, <- "usbaudio" ffb1caf0) Irps(q/p) = 1, 7
"kmixer" Filter ffa65b70, Child Factories 4
    Input Factory 2:
        Pin 81236000 (File ffaaf7d0, <- "splitter" 811df9c0) Irps(q/p) = 0, 0
    Output Factory 3:
        Pin 81252d00 (File 811df1d8) Irps(q/p) = 10, 0
"kmixer" Filter ffb03808, Child Factories 4
    Input Factory 2:
        Pin 8123c000 (File ffb10130, <- "splitter" 81250008) Irps(q/p) = 0, 0
    Output Factory 3:
        Pin ffa1e9c0 (File 81253468) Irps(q/p) = 10, 0
```

若要理解关系图，请按下列步骤：

**若要按照此关系图中：**

1.  找到感兴趣的 pin。 请考虑 0xFFB1CAF0，usbaudio 的输出插针 （工厂 0）。

2.  找到已连接的 pin。 在此示例中，这是拆分器 pin 0xFFA8B008。

3.  查看连接方向，并以可视方式移动这样一来查找筛选器名称。 （请记住，对列表排序时拓扑结构上。）在此示例中，向右箭头指示我们需要先看下面要查找的相应图钉的列表中的此条目。 下面的拆分器筛选器 0xFFA0C660 是立即。

4.  在筛选器 pin 实例列表中查找目标 pin 地址。 在这种情况下，此地址是 0xFFA8B008。

收件人遵循此关系图： 命令还可用于分析来自任何给定的起始点已停止的图形。 若要执行此操作，指定 4 英寸*标志*参数：

```dbgcmd
kd> !graph 812567c0 7 4

Attempting a graph build on 812567c0...  Please be patient...

Graph With Starting Point 812567c0:

"emu10k" Filter ff9ebb98, Child Factories 5
    Output Factory 0:
        Pin 812567c0 (File 811c6630, -> "splitter" 811df960) Irps(q/p) = 8, 0
"splitter" Filter ffb18890, Child Factories 2
    Output Factory 0:
        Pin 811df430 (File ffa55f90) Irps(q/p) = 10, 0
    Input Factory 1:
        Pin 811df960 (File 81187820, <- "emu10k" 812567c0) Irps(q/p) = 0, 8

Analyzing a Hung Graph From 812567c0:

Suspect Filters (For a Hung Graph):
    "emu10k" Filter ff9ebb98 or class "PortCls Wave Cyclic" is suspect.
        Reasons For This Analysis:
            - No critical pin has less than 8 queued Irps
            - Downstream "splitter" pin 811df960 is starved
        Irps to check:
            81255418 811df008 81252008 81255280 81250b30 ffa1fe70 81252e70 ffa01d98

NOTE: The above is based on heuristic analysis.  It is not designed to be a
      replacement for an actual developer looking at this particular hang!  The
      filters listed as suspects may or may not be the actual cause of the
      stall!
```

对于此类输出，查看"怀疑"列表。 这些可疑的筛选器是指那些处于向前运行的关系图中的关键路径中。 开始调试从该点基于在分析器生成的停止的原因。

**请注意**  应仅使用此功能已停止的关系图上 ！ 分析器还具有无法知道如何在关系图已处于此状态。 中断到调试器和分析正在运行的图形为已停止的关系图仍然显示可疑的筛选器。

 

 

 





