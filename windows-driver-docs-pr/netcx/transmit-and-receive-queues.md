---
title: 传输和接收队列
description: 传输和接收队列
ms.assetid: 4BF61CDF-4B62-47EB-936A-7DE81D62678A
keywords:
- NetAdapterCx 传输和接收队列，NetCx 传输和接收队列
ms.date: 01/24/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 1b3ea0d727923ba62a2ad21db4f52c8a9730fef9
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75208963"
---
# <a name="transmit-and-receive-queues"></a>传输和接收队列

## <a name="overview"></a>概述

*数据包队列*或*数据路径队列*是在 NetAdapterCx 中引入的对象，使客户端驱动程序能够在软件驱动程序中更明确地为硬件功能（例如硬件传输和接收队列）建模。 本主题说明如何使用 NetAdapterCx 中的传输和接收队列。 

当客户端驱动程序调用[**NET_ADAPTER_DATAPATH_CALLBACKS_INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-net_adapter_datapath_callbacks_init)（通常来自其[*EVT_WDF_DRIVER_DEVICE_ADD*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)事件回调函数）时，它将提供两个队列创建回调： [*EVT_NET_ADAPTER_CREATE_TXQUEUE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nc-netadapter-evt_net_adapter_create_txqueue)和[*EVT_NET_ADAPTER_CREATE_RXQUEUE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nc-netadapter-evt_net_adapter_create_rxqueue)。 客户端分别在这些回调中创建传输队列和接收队列。

框架在转换为低功率状态之前清空队列，并在删除适配器之前将其删除。

## <a name="creating-packet-queues"></a>创建数据包队列

创建数据包队列（传输队列或接收队列）时，客户端必须提供以下三个回调函数的指针：

- [*EVT_PACKET_QUEUE_ADVANCE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)
- [*EVT_PACKET_QUEUE_SET_NOTIFICATION_ENABLED*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacketqueue/nc-netpacketqueue-evt_packet_queue_set_notification_enabled)
- [*EVT_PACKET_QUEUE_CANCEL*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacketqueue/nc-netpacketqueue-evt_packet_queue_cancel)

此外，客户端还可以在初始化队列配置结构后提供这些可选的回调函数：

- [*EVT_PACKET_QUEUE_START*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacketqueue/nc-netpacketqueue-evt_packet_queue_start)
- [*EVT_PACKET_QUEUE_STOP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacketqueue/nc-netpacketqueue-evt_packet_queue_stop)

### <a name="creating-a-transmit-queue"></a>创建传输队列

NetAdapterCx 在[启动序列](power-up-sequence-for-a-netadaptercx-client-driver.md)的最末尾[*EVT_NET_ADAPTER_CREATE_TXQUEUE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nc-netadapter-evt_net_adapter_create_txqueue)调用。 在此回调过程中，客户端驱动程序通常会执行以下操作：

- 选择性地为队列注册开始和停止回调。
- 调用[**NetTxQueueInitGetQueueId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nettxqueue/nf-nettxqueue-nettxqueueinitgetqueueid)可检索要设置的传输队列的标识符。
- 调用[**NetTxQueueCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nettxqueue/nf-nettxqueue-nettxqueuecreate)分配队列。 
    - 如果[**NetTxQueueCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nettxqueue/nf-nettxqueue-nettxqueuecreate)失败， *EvtNetAdapterCreateTxQueue*回调函数应返回错误代码。
- 查询数据包扩展偏移量。

下面的示例演示如何在代码中查找这些步骤。 为清楚起见，此示例中已省略错误处理代码。

```C++
NTSTATUS
EvtAdapterCreateTxQueue(
    _In_    NETADAPTER          Adapter,
    _Inout_ NETTXQUEUE_INIT *   TxQueueInit
)
{
    NTSTATUS status = STATUS_SUCCESS;

    // Prepare the configuration structure
    NET_PACKET_QUEUE_CONFIG txConfig;
    NET_PACKET_QUEUE_CONFIG_INIT(
        &txConfig,
        EvtTxQueueAdvance,
        EvtTxQueueSetNotificationEnabled,
        EvtTxQueueCancel);

    // Optional: register the queue's start and stop callbacks
    txConfig.EvtStart = EvtTxQueueStart;
    txConfig.EvtStop = EvtTxQueueStop;

    // Get the queue ID
    const ULONG queueId = NetTxQueueInitGetQueueId(TxQueueInit);

    // Create the transmit queue
    NETPACKETQUEUE txQueue;
    status = NetTxQueueCreate(
        TxQueueInit,
        &txAttributes,
        &txConfig,
        &txQueue);

    // Get the queue context for storing the queue ID and packet extension offset info
    PMY_TX_QUEUE_CONTEXT queueContext = GetMyTxQueueContext(txQueue);

    // Store the queue ID in the context
    queueContext->QueueId = queueId;

    // Query checksum packet extension offset and store it in the context
    NET_EXTENSION_QUERY extension;
    NET_EXTENSION_QUERY_INIT(
        &extension,
        NET_PACKET_EXTENSION_CHECKSUM_NAME,
        NET_PACKET_EXTENSION_CHECKSUM_VERSION_1);

    NetTxQueueGetExtension(txQueue, &extension, &queueContext->ChecksumExtension);

    // Query Large Send Offload packet extension offset and store it in the context
    NET_EXTENSION_QUERY_INIT(
        &extension,
        NET_PACKET_EXTENSION_LSO_NAME,
        NET_PACKET_EXTENSION_LSO_VERSION_1);
    
    NetTxQueueGetExtension(txQueue, &extension, &queueContext->LsoExtension);

    return status;
}
```

### <a name="creating-a-receive-queue"></a>创建接收队列

若要从[*EVT_NET_ADAPTER_CREATE_RXQUEUE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nc-netadapter-evt_net_adapter_create_rxqueue)创建接收队列，请使用与传输队列相同的模式并调用[**NetRxQueueCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrxqueue/nf-netrxqueue-netrxqueuecreate)。 

下面的示例演示如何创建接收队列。 为清楚起见，此示例中已省略错误处理代码。

```c++
NTSTATUS
EvtAdapterCreateRxQueue(
    _In_ NETADAPTER NetAdapter,
    _Inout_ PNETRXQUEUE_INIT RxQueueInit
)
{
    NTSTATUS status = STATUS_SUCCESS;

    // Prepare the configuration structure
    NET_PACKET_QUEUE_CONFIG rxConfig;
    NET_PACKET_QUEUE_CONFIG_INIT(
        &rxConfig,
        EvtRxQueueAdvance,
        EvtRxQueueSetNotificationEnabled,
        EvtRxQueueCancel);

    // Optional: register the queue's start and stop callbacks
    rxConfig.EvtStart = EvtRxQueueStart;
    rxConfig.EvtStop = EvtRxQueueStop;

    // Get the queue ID
    const ULONG queueId = NetRxQueueInitGetQueueId(RxQueueInit);

    // Create the receive queue
    NETPACKETQUEUE rxQueue;
    status = NetRxQueueCreate(
        RxQueueInit,
        &rxAttributes,
        &rxConfig,
        &rxQueue);

    // Get the queue context for storing the queue ID and packet extension offset info
    PMY_RX_QUEUE_CONTEXT queueContext = GetMyRxQueueContext(rxQueue);

    // Store the queue ID in the context
    queueContext->QueueId = queueId;

    // Query the checksum packet extension offset and store it in the context
    NET_EXTENSION_QUERY extension;
    NET_EXTENSION_QUERY_INIT(
        &extension,
        NET_PACKET_EXTENSION_CHECKSUM_NAME,
        NET_PACKET_EXTENSION_CHECKSUM_VERSION_1); 
          
    NetRxQueueGetExtension(rxQueue, &extension, &queueContext->ChecksumExtension);

    return status;
}
```

## <a name="polling-model"></a>轮询模型

Get-netadapter 数据路径是轮询模型，一个数据包队列的轮询操作完全独立于其他队列。 通过调用客户端驱动程序的队列提前回调来实现轮询模型，如下图所示：

![轮询流](images/polling.png)

## <a name="advancing-packet-queues"></a>前进数据包队列

包队列中轮询操作的顺序如下所示：

1. 操作系统为传输或接收提供客户端驱动程序的缓冲区。
2. 客户端驱动程序会将数据包用于硬件。
3. 客户端驱动程序将已完成的数据包返回到操作系统。

轮询操作出现在客户端驱动程序的[*EvtPacketQueueAdvance*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)回调函数中。 客户端驱动程序中的每个数据包队列都由称为 "*净环*" 的基础数据结构（其中包含或链接到系统内存中的实际网络数据缓冲区）进行支持。 在*EvtPacketQueueAdvance*期间，客户端驱动程序通过控制环中的索引，在网络环上执行发送和接收操作，在传输或接收数据时，在硬件和操作系统之间传输缓冲区所有权。

有关网络环的详细信息，请参阅[净环简介](introduction-to-net-rings.md)。

有关为传输队列实现*EvtPacketQueueAdvance*的示例，请参阅[使用净环发送网络数据](sending-network-data-with-net-rings.md)。 有关为接收队列实现*EvtPacketQueueAdvance*的示例，请参阅[接收网络数据和净环](receiving-network-data-with-net-rings.md)。

## <a name="enabling-and-disabling-packet-queue-notification"></a>启用和禁用数据包队列通知

当客户端驱动程序在数据包队列的网络环中收到新数据包时，NetAdapterCx 将调用客户端驱动程序的[*EvtPacketQueueSetNotificationEnabled*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacketqueue/nc-netpacketqueue-evt_packet_queue_set_notification_enabled)回调函数。 此回调向客户端驱动程序指示在客户端驱动程序调用[**NetTxQueueNotifyMoreCompletedPacketsAvailable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nettxqueue/nf-nettxqueue-nettxqueuenotifymorecompletedpacketsavailable)或[**NetRxQueueNotifyMoreReceivedPacketsAvailable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrxqueue/nf-netrxqueue-netrxqueuenotifymorereceivedpacketsavailable)之前，轮询（ *EvtPacketQueueAdvance*或*EvtPacketQueueCancel*）将停止并且不会继续。 通常，PCI 设备使用此回调来启用 Tx 或 Rx 中断。 一旦接收到中断，就可以再次禁用中断，并且客户端驱动程序将调用**NetTxQueueNotifyMoreCompletedPacketsAvailable**或**NetRxQueueNotifyMoreReceivedPacketsAvailable**来触发框架，以再次开始轮询。

### <a name="enabling-and-disabling-notification-for-a-transmit-queue"></a>启用和禁用传输队列的通知

对于 PCI NIC，启用传输队列通知通常意味着启用传输队列的硬件中断。 当硬件中断触发时，客户端从其 DPC 调用[**NetTxQueueNotifyMoreCompletedPacketsAvailable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nettxqueue/nf-nettxqueue-nettxqueuenotifymorecompletedpacketsavailable) 。

同样，对于 PCI NIC，禁用队列通知意味着禁用与队列关联的中断。

对于具有异步 i/o 模型的设备，客户端通常使用内部标志来跟踪已启用状态。 异步操作完成后，完成处理程序会检查此标志，并在设置后调用[**NetTxQueueNotifyMoreCompletedPacketsAvailable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nettxqueue/nf-nettxqueue-nettxqueuenotifymorecompletedpacketsavailable) 。

如果 NetAdapterCx 调用*NotificationEnabled*设置为**FALSE**的*EvtPacketQueueSetNotificationEnabled* ，则客户端不能调用[**NetTxQueueNotifyMoreCompletedPacketsAvailable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nettxqueue/nf-nettxqueue-nettxqueuenotifymorecompletedpacketsavailable) ，直到 NetAdapterCx 下一次调用此回调函数， *NotificationEnabled*设置为**TRUE**。

例如：

```C++
VOID
MyEvtTxQueueSetNotificationEnabled(
    _In_ NETPACKETQUEUE TxQueue,
    _In_ BOOLEAN NotificationEnabled
)
{
    // Optional: retrieve queue's WDF context
    MY_TX_QUEUE_CONTEXT *txContext = GetTxQueueContext(TxQueue);

    // If NotificationEnabled is TRUE, enable transmit queue's hardware interrupt
    ...
}

VOID
MyEvtTxInterruptDpc(
    _In_ WDFINTERRUPT Interrupt,
    _In_ WDFOBJECT AssociatedObject
    )
{
    MY_INTERRUPT_CONTEXT *interruptContext = GetInterruptContext(Interrupt);

    NetTxQueueNotifyMoreCompletedPacketsAvailable(interruptContext->TxQueue);
}
```

### <a name="enabling-and-disabling-notification-for-a-receive-queue"></a>为接收队列启用和禁用通知

对于 PCI NIC，启用接收队列通知看起来非常类似于 Tx 队列。 这通常意味着启用接收队列的硬件中断。 当硬件中断触发时，客户端从其 DPC 调用[**NetRxQueueNotifyMoreReceivedPacketsAvailable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrxqueue/nf-netrxqueue-netrxqueuenotifymorereceivedpacketsavailable) 。

例如：

```C++
VOID
MyEvtRxQueueSetNotificationEnabled(
    _In_ NETPACKETQUEUE RxQueue,
    _In_ BOOLEAN NotificationEnabled
)
{
    // optional: retrieve queue's WDF Context
    MY_RX_QUEUE_CONTEXT *rxContext = GetRxQueueContext(RxQueue);

    // If NotificationEnabled is TRUE, enable receive queue's hardware interrupt
    ...
}

VOID
MyEvtRxInterruptDpc(
    _In_ WDFINTERRUPT Interrupt,
    _In_ WDFOBJECT AssociatedObject
    )
{
    MY_INTERRUPT_CONTEXT *interruptContext = GetInterruptContext(Interrupt);

    NetRxQueueNotifyMoreReceivedPacketsAvailable(interruptContext->RxQueue);
}
```

对于 USB 设备或具有软件接收完成机制的任何其他队列，客户端驱动程序应在其自身的上下文中进行跟踪，无论队列的通知是否已启用。 如果启用了通知[**，则请**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netrxqueue/nf-netrxqueue-netrxqueuenotifymorereceivedpacketsavailable)在完成例程（例如，当消息在 USB 连续读取器中变为可用时触发）。 下面的示例演示如何执行此操作。

```C++
VOID
UsbEvtReaderCompletionRoutine(
    _In_ WDFUSBPIPE Pipe,
    _In_ WDFMEMORY Buffer,
    _In_ size_t NumBytesTransferred,
    _In_ WDFCONTEXT Context
)
{
    UNREFERENCED_PARAMETER(Pipe);

    PUSB_RCB_POOL pRcbPool = *((PUSB_RCB_POOL*) Context);
    PUSB_RCB pRcb = (PUSB_RCB) WdfMemoryGetBuffer(Buffer, NULL);

    pRcb->DataOffsetCurrent = 0;
    pRcb->DataWdfMemory = Buffer;
    pRcb->DataValidSize = NumBytesTransferred;

    WdfObjectReference(pRcb->DataWdfMemory);

    ExInterlockedInsertTailList(&pRcbPool->ListHead,
                                &pRcb->Link,
                                &pRcbPool->ListSpinLock);

    if (InterlockedExchange(&pRcbPool->NotificationEnabled, FALSE) == TRUE)
    {
        NetRxQueueNotifyMoreReceivedPacketsAvailable(pRcbPool->RxQueue);
    }
}
```

## <a name="canceling-packet-queues"></a>取消数据包队列

当 OS 停止数据路径时，它将通过调用客户端驱动程序的[*EvtPacketQueueCancel*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacketqueue/nc-netpacketqueue-evt_packet_queue_cancel)回调函数开始。 在此回调中，客户端驱动程序将在框架删除数据包队列之前执行所需的任何处理。 取消传输队列是可选的，具体取决于硬件是否支持正在进行的传输取消，但需要取消接收队列。 

在*EvtPacketQueueCancel*期间，驱动程序会根据需要将数据包返回到操作系统。 有关传输队列和接收队列取消的代码示例，请参阅[取消网络数据](canceling-network-data-with-net-rings.md)和网络环。

在调用驱动程序的*EvtPacketQueueCancel*回调后，框架将继续轮询驱动程序的[*EvtPacketQueueAdvance*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)回调，直到所有数据包和缓冲区都返回到 OS。
