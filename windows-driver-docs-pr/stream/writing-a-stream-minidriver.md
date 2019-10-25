---
title: 编写流微型驱动程序
description: 编写流微型驱动程序
ms.assetid: 83540dff-3774-4197-8ba1-d28e12b4e366
keywords:
- Stream .sys 类驱动程序 WDK Windows 2000 内核，写入
- 流式处理微型驱动程序 WDK Windows 2000 内核，写入
- 微型驱动程序 WDK Windows 2000 内核流式处理，写入
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e0f8efce05454aa20a2de3822345bd227ef9981
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845141"
---
# <a name="writing-a-stream-minidriver"></a>编写流微型驱动程序





流类驱动程序的主要设计目标是处理处理操作系统的工作，其中包括支持多处理器计算机的复杂性，以及支持内核流式处理语义。 它要求微型驱动程序仅处理其必须执行的任何操作的设备特定部分。 类驱动程序为微型驱动程序分配内存，为微型驱动程序可能需要的任何 NT 内核资源执行簿记，并（可选）处理所有同步问题。

类驱动程序通过一组由微型驱动程序提供的回调与微型驱动程序通信。 编写流式处理微型驱动程序的大部分工作都是在编写这些回调时进行的。

在本文档中，我们将微型驱动程序提供的每种类型的例程称为**StrMiniXxx**。 微型驱动程序可能必须提供每个例程的一个或多个版本，具体取决于基础硬件可以执行的不同函数的数量。

流式处理驱动程序通常可以支持多个不同的数据流。 例如，DVD 播放机同时生成音频和视频流。 在内核流的上下文中，每个数据流都由一个[pin](ks-pins.md)表示。

Stream 类驱动程序跟踪微型驱动程序上的每个 pin。 在类驱动程序的术语中，每个 pin 类型都是一个*流*。 像固定类型这样的流可能有多个实例。 由于流可以接收 i/o 请求，因此驱动程序必须为每个流提供回调。

微型驱动程序可能必须提供以下例程。 它们在下面以及参考指南中进行了详细介绍。

**每个微型驱动程序提供的例程**

[*StrMiniCancelPacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_cancel_srb)

[*StrMiniReceiveDevicePacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_receive_device_srb)

[*StrMiniRequestTimeout*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_request_timeout_handler)

[*StrMiniEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_event_routine)

[*StrMiniInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_interrupt)

**微型驱动程序为每个单独的流提供的例程**

[*StrMiniReceiveStreamDataPacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_receive_device_srb)

[**StrMiniReceiveStreamControlPacket**](https://docs.microsoft.com/previous-versions/ff568467(v=vs.85))

[*StrMiniEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_event_routine)

[*StrMiniClock*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_query_clock_routine)

微型驱动程序可以对多个不同的流使用相同的回调。 回调可以确定其所代表的流是从其参数中调用的。

与所有 WDM 驱动程序一样，微型驱动程序也必须提供**DriverEntry**例程。 微型驱动程序的**DriverEntry**例程的主要任务是向类驱动程序注册微型驱动程序。

类驱动程序代表微型驱动程序接收所有 i/o 请求。 为了获得完成请求所需的信息，类驱动程序会生成一个流请求块（SRB），并将其传递给**StrMini*XXX*数据包**例程之一。 类驱动程序会将对设备的 i/o 请求作为一个整体发送到[*StrMiniReceiveDevicePacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_receive_device_srb)例程。 它将请求传递到[*StrMiniReceiveStreamDataPacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_receive_device_srb) （用于内核流式处理读取和写入请求）或[**StrMiniReceiveStreamControlPacket**](https://docs.microsoft.com/previous-versions/ff568467(v=vs.85)) （适用于其他请求）。

通常情况下，类驱动程序将其请求排队，并一次将一个传递给微型驱动程序。 微型驱动程序可以选择性地执行自己的同步;然后，微型驱动程序负责将它无法立即处理的请求排队。 有关详细信息，请参阅[微型驱动程序同步](minidriver-synchronization.md)。

微型驱动程序必须提供两个附加例程用于操作流请求块。 类驱动程序在收到 cancel IRP 时调用[*StrMiniCancelPacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_cancel_srb) ，并需通知微型驱动程序取消特定数据包。 类驱动程序还跟踪微型驱动程序完成其流请求块处理所花费的时间。 如果微型驱动程序的时间太长，则类驱动程序会超时请求，并调用微型驱动程序的[*StrMiniRequestTimeout*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_request_timeout_handler)例程。

发生硬件中断时，操作系统会向类驱动程序发出信号，然后调用微型驱动程序的[*StrMiniInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_interrupt)例程来处理中断。

 

 




