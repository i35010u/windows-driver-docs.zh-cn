---
title: 调试处理停滞
description: 调试处理停滞
ms.assetid: 9dff37ed-4843-4e85-8ab3-6a0a37a58c23
keywords:
- 内核调试，视频流停止，处理停止流式处理
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0051d7ae2a9f4aa5eddc1a7efe3b47bfdcef71d0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523017"
---
# <a name="debugging-a-processing-stall"></a>调试处理停滞


首先找到相关的 pin。 在假设的情况下，相关的视频捕获 pin 具有地址**8160DDE0**，因此，我们使用[ **！ ks.dump** ](-ks-dump.md)此地址的扩展命令，以获取更多详细信息：

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

首先，确定 pin 是适当的状态和另一个线程是否正在挂起处理互斥体。 在这种情况下，锁定状态是**KSSTATE\_运行**，和处理互斥体不被保留后，接下来，我们使用如[ **！ ks.dumpqueue** ](-ks-dumpqueue.md)扩展若要确定是否有帧可用：

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

中的上述部分显示 **！ ks.dumpqueue**输出，我们看到，有五个帧等待或可用。 这些帧超前或落后于前导边缘？ 在中 **！ ks.dumpqueue**显示，帧始终可以从最早列出到最新。 框架标头的前边缘与匹配的第一个帧列出，最早的帧。 因此所有可用的帧都是领先的前沿。

如果这不是这种情况，并改为的所有帧已背后前导边缘，并且拥有计数应克隆指针的引用，这些问题很可能源自的硬件或硬件的驱动程序的编程。 请确保硬件信号缓冲区完成 （检查中断和 dpc 进行标记），并确定，该驱动程序是进行适当的响应这些通知 （通过如删除缓冲区完成后，克隆）。

如果如下所示示例中，所有帧都是领先的前沿，问题几乎可以肯定是一个软件问题。 进一步的信息可以通过查看插针的获取和入口。

### <a name="span-idinterpretingtheandgatespanspan-idinterpretingtheandgatespaninterpreting-the-and-gate"></a><span id="interpreting_the_and_gate"></span><span id="INTERPRETING_THE_AND_GATE"></span>解释和入口

Pin 和入口控件处理。 如果其中一个入口计数，可以进行处理。 使用获取的当前状态和入口 **！ ks.dump**扩展：

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

由于入口计数是一个，And 门处于打开状态。 在这种情况下，调查处理停止以下可能的原因：

-   进程调度错误地返回的状态为\_PENDING。

-   数据可用性用例缺少[KsPinAttemptProcessing](https://go.microsoft.com/fwlink/p/?linkid=56545)调用。

 

 





