---
title: 分析捕获停滞问题
description: 分析捕获停滞问题
ms.assetid: 9a88deba-374c-4ccc-8bb8-18e3b4124158
keywords:
- 流式处理调试被废弃的内核
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: fdeeacbaeba1a30770c714d9df0bef41f445ad58
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354965"
---
# <a name="analyzing-a-capture-stall"></a>分析捕获停滞问题


下面是模拟捕获停滞的人为地创建的方案。 这是非常有价值的方案，因为类似的情况经常出现在压力测试。 方案是，如下所示：

Sndrec32 记录从主捕获设备的 Windows 录制组件，Creative SBLive 这种情况下 wave 设备。 为一段时间，它记录通常;但是，在关系图停留 8.50 秒，因为我们已显式导致 portcls 不适用于全面捕获 Irp 用于此测试的目的。

应用程序显示运行的但不是前移流的位置。 位置将在 8.50 秒处停止。

由于此计算机上的主捕获设备是 PCI 声卡的步骤，首先使用[ **！ ks.pciaudio** ](-ks-pciaudio.md)命令尝试并确定的起点。 使用标志值为 1 以显示所有正在运行流的请求：

```dbgcmd
kd> !pciaudio 1

1 Audio FDOs found:
 Functional Device 8121c030 [\Driver\emu10k]
        Wave Cyclic Streams:
            Pin 812567c0 RUN [emu10k1m!CMiniportWaveCyclicStreamSBLive ff9ec7f8] 
```

在这种情况下，只有一个 PCI 音频设备和 Intel emu10k 驱动程序提供服务 (\\驱动程序\\emu10k)。 此驱动程序当前存在一个正在运行流 (0x812567C0)。 现在，可以使用[ **！ ks.graph** ](-ks-graph.md)以查看内核关系图。 设置*级别*并*标志*同时为 7 可获取隔栏上的最大详细信息：

```dbgcmd
kd> !graph 812567c0 7 7
Attempting a graph build on 812567c0...  Please be patient...
Graph With Starting Point 812567c0:
"emu10k" Filter ff9ebb98, Child Factories 5
    Output Factory 0:
        Pin 812567c0 (File 811c6630, -> "splitter" 811df960) Irps(q/p) = 8, 0
 Queued: 81255418 811df008 81252008 81255280 81250b30 ffa1fe70 81252e70 ffa01d98 
```

上图显示工厂 0 的详细信息。 Emu10k 输出插针 0x812567C0 连接到拆分器输入插针 0x811DF960。 有八个 Irp 排队到 emu10k 的输出插针。 从输出[ **！ ks.graph** ](-ks-graph.md)继续，如下所示：

```dbgcmd
"splitter" Filter ffb18890, Child Factories 2
    Output Factory 0:
        Pin 811df430 (File ffa55f90) Irps(q/p) = 10, 0
 Queued: ffadd008 ffa73b00 ffa1e998 811de310 ffa54370 ffaaf008 811dee70 81250e70 811de580 811de8c0 
```

有十个 Irp 排队到拆分器的输出插针。

```dbgcmd
    Input Factory 1:
        Pin 811df960 (File 81187820, <- "emu10k" 812567c0) Irps(q/p) = 0, 8
            Pending: 81255418 811df008 81252008 81255280 81250b30 ffa1fe70 81252e70 ffa01d98 
```

拆分器的输入插针已没有排队的 Irp;但是，它正在等待从输入队列的 emu10k 八个。

```dbgcmd
Analyzing a Hung Graph From 812567c0:

Suspect Filters (For a Hung Graph):
 "emu10k" Filter ff9ebb98 or class "PortCls Wave Cyclic" is suspect.
        Reasons For This Analysis:
            - No critical pin has less than 8 queued Irps
            - Downstream "splitter" pin 811df960 is starved
        Irps to check:
 81255418 811df008 81252008 81255280 81250b30 ffa1fe70 81252e70 ffa01d98
```

中的信息，分析器会建议 emu10k 或 WaveCyclic 可能是错误。 它还提供了一系列可疑 Irp;这些是要排队发送至 emu10k 的输入插针 Irp。 如果任何这些 Irp 完成，拆分器会将数据复制并完成 IRP 和关系图的进展。 由于某种原因，emu10k 尚未完成这些捕获 Irp。

 

 





