---
title: 分析捕获停滞问题
description: 分析捕获停滞问题
keywords:
- 内核流调试，等等
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec553fdf56101b0b38a60afaad25e1de88bba12a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783551"
---
# <a name="analyzing-a-capture-stall"></a>分析捕获停滞问题


以下是一个模拟捕获延迟的人为创建方案。 这是一个特别有价值的方案，因为类似的情况常常发生在压力测试中。 场景如下：

Windows 记录组件 Sndrec32 正在从主捕获设备进行记录，在本例中为创造性 SBLive wave 设备。 在一段时间内，它会正常记录;但是，图形会停留在8.50 秒，因为我们已明确导致 portcls 不能完成捕获 Irp 来完成此测试。

应用程序显示正在运行，但不向前移动流位置。 位置在8.50 秒内停止。

由于此计算机上的主捕获设备是 PCI 声卡，因此请首先使用 [**！ ks**](-ks-pciaudio.md) 命令尝试并确定起点。 使用标志值1请求显示所有正在运行的流：

```dbgcmd
kd> !pciaudio 1

1 Audio FDOs found:
 Functional Device 8121c030 [\Driver\emu10k]
        Wave Cyclic Streams:
            Pin 812567c0 RUN [emu10k1m!CMiniportWaveCyclicStreamSBLive ff9ec7f8] 
```

在这种情况下，只有一个 PCI 音频设备，它由 Intel emu10k 驱动程序 (\\ driver \\ emu10k) 提供服务。 此驱动程序当前有一个正在运行的流 (0x812567C0) 。 现在可以使用 [**！ ks**](-ks-graph.md) 来查看内核关系图。 将 *级别* 和 *标志* 设置为7可获取有关延迟的最大详细信息：

```dbgcmd
kd> !graph 812567c0 7 7
Attempting a graph build on 812567c0...  Please be patient...
Graph With Starting Point 812567c0:
"emu10k" Filter ff9ebb98, Child Factories 5
    Output Factory 0:
        Pin 812567c0 (File 811c6630, -> "splitter" 811df960) Irps(q/p) = 8, 0
 Queued: 81255418 811df008 81252008 81255280 81250b30 ffa1fe70 81252e70 ffa01d98 
```

上面显示了工厂0的详细信息。 Emu10k output 引脚0x812567C0 连接到拆分器输入插针0x811DF960。 有8个 emu10k's 的输出插针。 从 [**！ ks**](-ks-graph.md) 开始的输出如下所示：

```dbgcmd
"splitter" Filter ffb18890, Child Factories 2
    Output Factory 0:
        Pin 811df430 (File ffa55f90) Irps(q/p) = 10, 0
 Queued: ffadd008 ffa73b00 ffa1e998 811de310 ffa54370 ffaaf008 811dee70 81250e70 811de580 811de8c0 
```

有10个为拆分器的输出插针排队的 Irp。

```dbgcmd
    Input Factory 1:
        Pin 811df960 (File 81187820, <- "emu10k" 812567c0) Irps(q/p) = 0, 8
            Pending: 81255418 811df008 81252008 81255280 81250b30 ffa1fe70 81252e70 ffa01d98 
```

拆分器的输入插针没有排队的 Irp;但是，它正在等待八个 from emu10k 进入队列。

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

通过此信息，analyzer 会建议 emu10k 或 WaveCyclic 可能出现故障。 它还提供可疑 Irp 的列表;这些是已排队到 emu10k's 输入插针的 Irp。 如果这些 Irp 中有任何一个完成，拆分器会复制数据并完成 IRP，并使该图形取得进展。 出于某种原因，emu10k 未完成这些捕获 Irp。

 

 





