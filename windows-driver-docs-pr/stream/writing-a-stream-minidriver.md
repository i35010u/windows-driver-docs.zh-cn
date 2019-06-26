---
title: 编写流微型驱动程序
description: 编写流微型驱动程序
ms.assetid: 83540dff-3774-4197-8ba1-d28e12b4e366
keywords:
- Stream.sys 类驱动程序 WDK Windows 2000 内核、 编写
- 流式处理微型驱动程序 WDK Windows 2000 内核、 编写
- 微型驱动程序 WDK Windows 2000 内核流式处理、 编写
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1df004fb437789d471844324aa2688b4c69dfa0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385352"
---
# <a name="writing-a-stream-minidriver"></a>编写流微型驱动程序





Stream 类驱动程序的主要设计目标是处理这两个处理操作系统，包括支持多处理器计算机，并支持流式处理语义的内核的复杂性的工作。 它需要微型驱动程序来处理必须执行任何操作的特定于设备的部分。 类驱动程序为微型驱动程序分配内存，执行任何 NT 内核资源微型驱动程序可能需要和 （可选） 处理所有同步问题的簿记。

与通过一系列提供微型驱动程序回调微型驱动程序进行通信的类驱动程序。 编写流式处理的微型驱动程序的工作的大部分出现在编写这些回调。

在本文档中，我们指每种类型的作为微型驱动程序提供的例程**StrMiniXxx**。 微型驱动程序可能需要提供一个或多个版本的每个例程，具体取决于底层硬件是能够执行不同功能。

流式处理的驱动程序通常可以支持多个不同的数据的流。 例如，DVD 播放机将生成一个音频和视频流。 在内核流式处理的上下文中，由表示数据的每个流[pin](ks-pins.md)。

Stream 类驱动程序跟踪的微型驱动程序上的每个 pin。 在类驱动程序的术语中，每个 pin 类型是*流*。 那些，类似于固定类型，可能拥有多个实例。 由于流可以接收的 I/O 请求，该驱动程序必须将每个流提供的回调。

以下是微型驱动程序可能需要提供的例程。 它们全面阐述了更下方，并在参考指南。

**每个微型驱动程序提供的例程**

[*StrMiniCancelPacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nc-strmini-phw_cancel_srb)

[*StrMiniReceiveDevicePacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nc-strmini-phw_receive_device_srb)

[*StrMiniRequestTimeout*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nc-strmini-phw_request_timeout_handler)

[*StrMiniEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nc-strmini-phw_event_routine)

[*StrMiniInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nc-strmini-phw_interrupt)

**例程微型驱动程序提供了为每个单独的流**

[*StrMiniReceiveStreamDataPacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nc-strmini-phw_receive_device_srb)

[**StrMiniReceiveStreamControlPacket**](https://docs.microsoft.com/previous-versions/ff568467(v=vs.85))

[*StrMiniEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nc-strmini-phw_event_routine)

[*StrMiniClock*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nc-strmini-phw_query_clock_routine)

很可能微型驱动程序为多个不同的流使用相同的回调。 回调可以确定的名义利用其形参调用的流。

微型驱动程序，如所有 WDM 驱动程序，还必须提供**DriverEntry**例程。 主要任务**DriverEntry**例程的微型驱动程序是将注册的类驱动程序微型驱动程序。

在类驱动程序接收代表微型驱动程序的所有 I/O 请求。 若要获取其要完成该请求所需的信息，在类驱动程序生成的流请求块 (SRB)，并将其传递到其中一个**StrMini*XXX*数据包**例程。 在类驱动程序将对设备的 I/O 请求调度到整个[ *StrMiniReceiveDevicePacket* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nc-strmini-phw_receive_device_srb)例程。 它将请求传递到的各个流[ *StrMiniReceiveStreamDataPacket* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nc-strmini-phw_receive_device_srb) （对于内核流式处理读取和写入请求） 或[ **StrMiniReceiveStreamControlPacket** ](https://docs.microsoft.com/previous-versions/ff568467(v=vs.85)) （适用于其他请求）。

通常情况下，类驱动程序其请求排队，并将它们传递一次一个地给微型驱动程序。 微型驱动程序，可能可以选择执行其自己的同步;微型驱动程序应负责无法立即处理的排队请求。 请参阅[微型驱动程序同步](minidriver-synchronization.md)有关详细信息。

微型驱动程序必须提供用于操作流请求块的两个其他例程。 类驱动程序调用[ *StrMiniCancelPacket* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nc-strmini-phw_cancel_srb)当它收到取消 IRP，并且需要告诉微型驱动程序来取消特定的数据包。 在类驱动程序还会跟踪的微型驱动程序所需的时间完成其处理的流请求块。 如果微型驱动程序花费的时间太长，类驱动程序超时请求，并调用微型驱动程序的[ *StrMiniRequestTimeout* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nc-strmini-phw_request_timeout_handler)例程。

当硬件中断发生时，操作系统向发出信号类驱动程序，后者随后调用微型驱动程序的[ *StrMiniInterrupt* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nc-strmini-phw_interrupt)例程来处理中断。

 

 




