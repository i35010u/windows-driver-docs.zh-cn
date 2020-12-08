---
title: 使用 ks
description: 使用 ks
keywords:
- 内核流调试，显示图形
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a0d6894c3557b3d71649527837fead6d5dbf0d7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803205"
---
# <a name="using-ksgraph"></a>使用 !ks.graph


[**！ Ks**](-ks-graph.md)命令是内核流式处理扩展模块中功能最强大的扩展命令之一。 此命令以内核模式从任何给定的起点显示整个关系图。

在运行 [**！ ks**](-ks-graph.md)之前，您可能需要启用所有能够激活的库扩展。 为此，请发出 [**libexts enableall**](-ks-libexts.md) 命令。 **！ Ks** 的输出将是以界定闭合排序顺序排列的内核模式图的文本说明。 以下是示例：

```dbgcmd
kd> !graph ffa0c6d4 7
Attempting a graph build on ffa0c6d4...  Please be patient...
Graph With Starting Point ffa0c6d4:
"usbaudio" Filter ffaaa768, Child Factories 2
    Output Factory 0:
        Pin ffb1caf0 (File 811deeb8, -> "splitter" ffa8b008) Irps(q/p) = 7, 1
```

此示例将显示一个捕获图形，其中两个 Sndrec32.exe 正在从电传 u 麦克风捕获。 每个单独的记录都以 (usbaudio 的名称开头，在上面的部分中) 并在筛选器上显示筛选器地址 (0xFFAAA768) 和子 pin 工厂的数量 (2) 。

在每个条目下，会枚举每个工厂实例的地址，并列出每个 (0xFFB1CAF0) 的每个 pin 实例的地址、对应于每个实例的文件对象 (0x811DEEB8) 、连接方向、该连接的目标和目标 pin 的地址 (0xFFA8B008) 。 同时还会显示每个 pin 的排队 (7) 和挂起的 Irp (1) 。

 ( 的前向方向符号的连接（ &gt;) ）指示 pin 是输出插针并且连接到输入插针。 另一方面，具有反向方向符号 (&lt; ) 的连接是输入插针，并显示连接的源。 输出如下所示：

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

为了跟随图形，请使用以下过程：

**若要遵循此图：**

1.  查找感兴趣的 pin。 请考虑0xFFB1CAF0，usbaudio 的输出插针 (出厂 0) 。

2.  找到连接的 pin。 在此示例中，这是拆分器 pin 0xFFA8B008。

3.  查看连接方向，并以可视方式移动以查找筛选器名称。  (记住，列表界定闭合排序。 ) 在此示例中，向右箭头指示我们需要在列表中的此条目下面查找相应的 pin。 下面是拆分筛选器的0xFFA0C660。

4.  在筛选器 pin 实例列表中查找目标 pin 地址。 在这种情况下，此地址为0xFFA8B008。

要按照此图执行的操作：还可以使用命令来分析任何给定起始点的已停止关系图。 为此，请在 *Flags* 参数中指定4：

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

对于此类输出，请查看 "可疑" 列表。 这些可疑筛选器是指图形中正在进行的关键路径。 根据分析器为延迟生成的原因，从该点开始调试。

**注意**   此功能只能用于已停止的图形！ 分析器无法知道图形处于此状态的时间。 进入调试器并分析正在运行的图形作为停止关系图仍会显示可疑筛选器。

 

 

 





