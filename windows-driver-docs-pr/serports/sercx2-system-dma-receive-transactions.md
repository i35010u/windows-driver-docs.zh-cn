---
title: SerCx2 System-DMA-Receive 事务
description: 某些串行控制器驱动程序实现对支持接收使用系统 DMA 控制器的事务。
ms.assetid: 0374D1BE-96ED-43D6-8661-5E9676B82C0D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad5d3b4ac0b153294e36245431871a54c2ac4278
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387968"
---
# <a name="sercx2-system-dma-receive-transactions"></a>SerCx2 System-DMA-Receive 事务


某些串行控制器驱动程序实现对支持接收使用系统 DMA 控制器的事务。 这种支持是可选的但可以提高性能，因为它使主处理器需要的用于通过编程方式设置 I/O (PIO) 的长整型数据传输。 SerCx2 执行设置了系统 DMA 控制器并启动代表串行控制器驱动程序的必要 DMA 传输系统 DMA 接收事务。

串行控制器驱动程序创建系统 DMA 接收对象时，驱动程序提供 SerCx2 将用于设置系统 DMA 接收事务的系统 DMA 适配器的参数。

系统 DMA 接收事务的开始之前, 串行控制器驱动程序可以选择要执行的串行控制器硬件或 DMA 适配器可能需要事务的任何特殊设置。 在事务完成后，该驱动程序，如有必要，任何执行清理操作的串行控制器硬件状态可能需要的。

## <a name="creating-the-system-dma-receive-object"></a>创建系统 DMA 接收对象


SerCx2 可以调用任何串行控制器驱动程序之前*EvtSerCx2SystemDmaReceive*Xxx * * 函数，该驱动程序必须调用[ **SerCx2SystemDmaReceiveCreate** ](https://msdn.microsoft.com/library/windows/hardware/dn265279)方法以向 SerCx2 注册这些函数。 此方法接受，作为输入参数，一个指向[ **SERCX2\_系统\_DMA\_接收\_配置**](https://msdn.microsoft.com/library/windows/hardware/dn265339)结构，其中包含驱动程序的指针*EvtSerCx2SystemDmaReceive*Xxx * * 函数。

作为一个选项，该驱动程序可以实现任何或所有以下函数：

-   [*EvtSerCx2SystemDmaReceiveInitializeTransaction*](https://msdn.microsoft.com/library/windows/hardware/dn265232)
-   [*EvtSerCx2SystemDmaReceiveCleanupTransaction*](https://msdn.microsoft.com/library/windows/hardware/dn265229)
-   [*EvtSerCx2SystemDmaReceiveConfigureDmaChannel*](https://msdn.microsoft.com/library/windows/hardware/dn265230)

作为一个选项，该驱动程序可以实现以下两个函数：

-   [*EvtSerCx2SystemDmaReceiveEnableNewDataNotification*](https://msdn.microsoft.com/library/windows/hardware/dn265231)
-   [*EvtSerCx2SystemDmaReceiveCancelNewDataNotification*](https://msdn.microsoft.com/library/windows/hardware/dn265228)

在前面的列表中实现的两个函数之一的驱动程序必须同时实现。

**SerCx2SystemDmaReceiveCreate**方法创建系统 DMA 接收对象并提供与调用驱动程序[ **SERCX2SYSTEMDMARECEIVE** ](https://msdn.microsoft.com/library/windows/hardware/dn265284)这句柄对象。 在驱动程序*EvtSerCx2SystemDmaReceive*Xxx * * 函数所有采用该句柄作为其第一个参数。 以下 SerCx2 方法将此句柄作为其第一个参数：

-   [**SerCx2SystemDmaReceiveNewDataNotification**](https://msdn.microsoft.com/library/windows/hardware/dn265283)
-   [**SerCx2SystemDmaReceiveInitializeTransactionComplete**](https://msdn.microsoft.com/library/windows/hardware/dn265281)
-   [**SerCx2SystemDmaReceiveCleanupTransactionComplete**](https://msdn.microsoft.com/library/windows/hardware/dn265278)
-   [**SerCx2SystemDmaReceiveGetDmaEnabler**](https://msdn.microsoft.com/library/windows/hardware/dn265280)

## <a name="hardware-initialization-and-clean-up"></a>硬件初始化和清理


初始化系统 DMA 接收事务开始时的串行控制器硬件或清理该事务结束时的串行控制器的硬件状态，可能需要一些串行控制器驱动程序。

如果驱动程序实现[ *EvtSerCx2SystemDmaReceiveInitializeTransaction* ](https://msdn.microsoft.com/library/windows/hardware/dn265232)事件回调函数，SerCx2 调用此函数可在开始第一个 DMA 之前初始化串行控制器传输在事务中。 如果实现，则*EvtSerCx2SystemDmaReceiveInitializeTransaction*函数必须调用[ **SerCx2SystemDmaReceiveInitializeTransactionComplete** ](https://msdn.microsoft.com/library/windows/hardware/dn265281)要初始化的串行控制器驱动程序完成时通知 SerCx2 方法。

如果该驱动程序实现[ *EvtSerCx2SystemDmaReceiveCleanupTransaction* ](https://msdn.microsoft.com/library/windows/hardware/dn265229)事件回调函数，SerCx2 调用此函数以进行最终 DMA 传输结束后清除硬件状态在事务中。 如果实现，则*EvtSerCx2SystemDmaReceiveInitializeTransaction*函数必须调用[ **SerCx2SystemDmaReceiveCleanupTransactionComplete** ](https://msdn.microsoft.com/library/windows/hardware/dn265278)方法通知 SerCx2 清理串行控制器驱动程序完成。

需要执行任何特殊配置的系统 DMA 接收事务开始时的系统 DMA 控制器的串行控制器驱动程序应实现[ *EvtSerCx2SystemDmaReceiveConfigureDmaChannel*](https://msdn.microsoft.com/library/windows/hardware/dn265230)事件回调函数。 此函数可以调用[ **SerCx2SystemDmaReceiveGetDmaEnabler** ](https://msdn.microsoft.com/library/windows/hardware/dn265280)方法以获取有关使用事务的系统 DMA 适配器 DMA 促成因素。 SerCx2 开始在事务中的第一个 DMA 传输之前调用此函数。 DMA 实现方法的详细信息，请参阅[启用 DMA 事务](https://msdn.microsoft.com/library/windows/hardware/ff540818)。

## <a name="new-data-notifications"></a>新数据通知


作为一个选项，可以实现串行控制器驱动程序[ *EvtSerCx2SystemDmaReceiveEnableNewDataNotification* ](https://msdn.microsoft.com/library/windows/hardware/dn265231)事件回调函数。 如果实现，SerCx2 使用此函数有效地管理作为系统 DMA 接收事务处理读取请求的处理过程中的超时间隔。

如果串行控制器收到的两个连续字节之间的间隔超出了客户端指定的最长时间，会发生间隔超时。 外围设备驱动程序将读取的请求发送到 SerCx2 后，间隔超时不能发生之前，至少一个字节的数据是从串行连接的外围设备收到。 之间的到达时间的读取的请求和外围设备中的数据的第一个字节的接收可能比所需接收的数据的读取请求的其余部分后接收到的第一个字节的时间。 有关详细信息，请参阅[**串行\_超时**](https://msdn.microsoft.com/library/windows/hardware/hh439614)。

SerCx2 调用*EvtSerCx2SystemDmaReceiveEnableNewDataNotification*函数，如果实现它后，若要启用*的新数据通知*。 如果启用了此通知并且串行控制器接收的新数据的一个或多个字节从外围设备，或已存在数据其接收 FIFO，串行控制器驱动程序必须调用[ **SerCx2SystemDmaReceiveNewDataNotification** ](https://msdn.microsoft.com/library/windows/hardware/dn265283)方法以通知 SerCx2。

若要检测可能间隔超时，SerCx2 定期调用[ **ReadDmaCounter** ](https://msdn.microsoft.com/library/windows/hardware/ff560782)例程的系统 DMA 适配器以检查是否在前一个时间间隔期间收到的任何数据。 SerCx2 如何检测数据的第一个字节的回执取决于是否实现串行控制器驱动程序*EvtSerCx2SystemDmaReceiveEnableNewDataNotification*函数。 如果执行此函数，SerCx2 调用函数来启用新数据通知和接收数据的第一个字节时驱动程序收到通知。 否则，SerCx2 定期调用**ReadDmaCounter**检测接收方，第一个字节，以及可能需要定期唤醒处理器来进行这些调用。 因此，驱动程序实现*EvtSerCx2SystemDmaReceiveEnableNewDataNotification*函数可以通过不要求使用处理器而那样频繁地唤醒减少电源消耗。

**请注意**  SerCx2 依赖**ReadDmaCounter**系统 DMA 适配器在系统 DMA 接收事务和系统 DMA 传输事务期间监视超时值的例程。 硬件抽象层 (HAL) 必须实现一个功能齐备**ReadDmaCounter**例行系统 DMA 控制器用来从串行控制器来回传输数据。

 

支持的系统 DMA 接收事务的新数据通知的串行控制器驱动程序必须实现[ *EvtSerCx2SystemDmaReceiveCancelNewDataNotification* ](https://msdn.microsoft.com/library/windows/hardware/dn265228)事件回调函数，以便 SerCx2 可以取消已启用的新数据通知发生前。 如果取消挂起的读取的请求时，启用了新数据通知或总超时发生时，调用 SerCx2 *EvtSerCx2SystemDmaReceiveCancelNewDataNotification*函数构建以用于取消通知。 如果此函数已成功取消挂起通知，它将返回 **，则返回 TRUE**。 返回值 **，则返回 TRUE**串行控制器驱动程序将不会调用保证**SerCx2SystemDmaReceiveNewDataNotification**。 返回值**FALSE**指示驱动程序已调用，或将很快就会调用**SerCx2SystemDmaReceiveNewDataNotification**。 有关总超时的详细信息，请参阅[**串行\_超时**](https://msdn.microsoft.com/library/windows/hardware/hh439614)。

 

 




