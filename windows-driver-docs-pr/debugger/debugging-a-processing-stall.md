---
title: 调试处理停滞问题
description: 调试处理停滞问题
keywords:
- 内核流调试，视频流停止，处理延迟
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd4fc8198d2c4ec1c1f7e354d5fea7bea094678a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803643"
---
# <a name="debugging-a-processing-stall"></a>调试处理停滞问题


首先查找相关的 pin。 在假设的情况下，相关视频捕获 pin 具有地址 **8160DDE0**，因此，我们在此地址上使用 [**！ ks**](-ks-dump.md) extension 命令来获取更多详细信息：

```dbgcmd
kd> !ks.dump 8160DDE0 7
Pin object 8160DDE0 [CKsPin = 8160DD50]
    DeviceState    KSSTATE_RUN
    ClientState    KSSTATE_RUN
    CKsPin object 8160DD50 [KSPIN = 8160DDE0]
        State                    KSSTATE_RUN
        Processing Mutex         8160DFD0 is not held
        And Gate &               8160DF88
        And Gate Count           1
```

首先，确定 pin 是否处于适当的状态，以及处理 mutex 是否正在由另一个线程持有。 在这种情况下，pin 状态为 **KSSTATE \_ RUN**，因为它应该是，并且不会保留处理互斥体，因此我们接下来使用 [**！ dumpqueue**](-ks-dumpqueue.md) 扩展来确定是否有可用的帧：

```dbgcmd
kd> !ks.dumpqueue 8160DDE0 7
Queue 8172D5D8:
 Frames Received  : 763
    Frames Waiting   : 5
...<this part of display not shown>...
Queue 8172D5D8:
 Frame Header 81B77E60:
        Irp = 816EE008
        Refcount = 1
    Frame Header 81A568D0:
        Irp = 816DE008
        Refcount = 0
    Frame Header 81844ED8:
        Irp = FFA0F650
        Refcount = 0
    Frame Header 8174B0B0:
        Irp = FFABB460
        Refcount = 0
    Leading Edge:
        Stream Pointer 8183EA58 [Public 8183EA90]:
            Frame Header = 81B77E60
...<this part of display not shown>...
```

在上面的 **！ dumpqueue** 输出的部分显示中，我们看到有5个帧正在等待或可用。 这些帧是位于前导边缘之前还是之后？ 在 **dumpqueue** 显示中，框架始终按从最旧到最新的顺序列出。 前导边缘的框架标头与列出的第一个帧的帧标题匹配，即最早的帧。 因此，所有可用帧都在前导边缘之前。

如果不是这种情况，而是所有的帧都在前导边缘之后，并且由于克隆指针而产生了引用计数，则问题很可能是由硬件或驱动程序的硬件编程引起的。 请确保硬件正在向缓冲区发出信号， (检查中断和 Dpc) 并确定驱动程序是否已通过在缓冲区完成时删除克隆来 (相应的通知，例如) 。

例如，如我们的示例中所述，所有帧都在领先的边缘，问题几乎肯定是软件问题。 可以通过查看 pin 和门获取详细信息。

### <a name="span-idinterpreting_the_and_gatespanspan-idinterpreting_the_and_gatespaninterpreting-the-and-gate"></a><span id="interpreting_the_and_gate"></span><span id="INTERPRETING_THE_AND_GATE"></span>解释和门

Pin 的和门控件处理。 如果入口计数为1，则可能发生处理。 使用 **！ ks** 扩展名获取和入口的当前状态：

```dbgcmd
kd> !ks.dump 8160DDE0 7
Pin object 8160DDE0 [CKsPin = 8160DD50]
    DeviceState    KSSTATE_RUN
    ClientState    KSSTATE_RUN
    CKsPin object 8160DD50 [KSPIN = 8160DDE0]
        State                    KSSTATE_RUN
        Processing Mutex         8160DFD0 is not held
        And Gate &               8160DF88
        And Gate Count           1
```

因为入口计数为1，所以和入口为打开状态。 在这种情况下，请调查处理延迟的以下潜在原因：

-   进程调度错误地返回了 "挂起" 状态 \_ 。

-   数据可用性事例缺少 [KsPinAttemptProcessing](/windows-hardware/drivers/ddi/ks/nf-ks-kspinattemptprocessing) 调用。

 

