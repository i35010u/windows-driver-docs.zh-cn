---
title: 传输和接收队列
description: 传输和接收队列
ms.assetid: 4BF61CDF-4B62-47EB-936A-7DE81D62678A
keywords:
- NetAdapterCx 传输和接收队列，NetCx 传输和接收队列
ms.date: 01/24/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: d8a103df6facbd9d0144902462c744e209d96d43
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903945"
---
# <a name="transmit-and-receive-queues"></a>传输和接收队列

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

## <a name="overview"></a>概述

*数据包队列*，或*数据路径队列*NetAdapterCx 以启用客户端驱动程序进行建模其硬件功能，例如硬件中引入的对象传输和更为明确地接收队列中的软件驱动程序. 本主题说明如何使用传输和接收队列中 NetAdapterCx。 

当客户端驱动程序调用[ **NET_ADAPTER_DATAPATH_CALLBACKS_INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-net_adapter_datapath_callbacks_init)，通常是从其[ *EVT_WDF_DRIVER_DEVICE_ADD* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)事件回调函数，它提供了两个队列创建回调：[*EVT_NET_ADAPTER_CREATE_TXQUEUE* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nc-netadapter-evt_net_adapter_create_txqueue)并[ *EVT_NET_ADAPTER_CREATE_RXQUEUE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nc-netadapter-evt_net_adapter_create_rxqueue)。 客户端创建传输，并分别接收这些回调中的队列。

Framework 转换到低功耗状态之前清空队列，并将其删除然后再删除该适配器。

## <a name="creating-packet-queues"></a>创建数据包队列

创建传输队列或接收队列中，数据包队列时客户端必须提供以下三个回调函数的指针：

- [*EVT_PACKET_QUEUE_ADVANCE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)
- [*EVT_PACKET_QUEUE_SET_NOTIFICATION_ENABLED*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_set_notification_enabled)
- [*EVT_PACKET_QUEUE_CANCEL*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_cancel)

此外，客户端可以初始化队列配置结构后提供这些可选的回调函数：

- [*EVT_PACKET_QUEUE_START*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_start)
- [*EVT_PACKET_QUEUE_STOP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_stop)

### <a name="creating-a-transmit-queue"></a>创建传输队列

NetAdapterCx 调用[ *EVT_NET_ADAPTER_CREATE_TXQUEUE* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nc-netadapter-evt_net_adapter_create_txqueue)最末尾[强化序列](power-up-sequence-for-a-netadaptercx-client-driver.md)。 在此回调期间客户端驱动程序通常执行以下操作：

- 可以选择注册开始和停止队列的回调。
- 调用[ **NetTxQueueInitGetQueueId** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nettxqueue/nf-nettxqueue-nettxqueueinitgetqueueid)可检索要设置的传输队列的标识符。
- 调用[ **NetTxQueueCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nettxqueue/nf-nettxqueue-nettxqueuecreate)分配一个队列。 
    - 如果[ **NetTxQueueCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nettxqueue/nf-nettxqueue-nettxqueuecreate)发生故障， *EvtNetAdapterCreateTxQueue*回调函数应返回一个错误代码。
- 查询数据包扩展偏移量。

下面的示例显示了这些步骤可能会在代码中如下所示。 此示例为清楚起见离职错误处理代码。

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
    NET_PACKET_EXTENSION_QUERY extension;
    NET_PACKET_EXTENSION_QUERY_INIT(
        &extension,
        NET_PACKET_EXTENSION_CHECKSUM_NAME,
        NET_PACKET_EXTENSION_CHECKSUM_VERSION_1);

    NetTxQueueGetExtension(txQueue, &extension, &queueContext->ChecksumExtension);

    // Query Large Send Offload packet extension offset and store it in the context
    NET_PACKET_EXTENSION_QUERY_INIT(
        &extension,
        NET_PACKET_EXTENSION_LSO_NAME,
        NET_PACKET_EXTENSION_LSO_VERSION_1);
    
    NetTxQueueGetExtension(txQueue, &extension, &queueContext->LsoExtension);

    return status;
}
```

### <a name="creating-a-receive-queue"></a>创建接收队列

若要创建从接收队列[ *EVT_NET_ADAPTER_CREATE_RXQUEUE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nc-netadapter-evt_net_adapter_create_rxqueue)，使用相同的模式作为传输队列，调用[ **NetRxQueueCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrxqueue/nf-netrxqueue-netrxqueuecreate). 

下面的示例演示如何创建接收队列可能会在代码中查找。 此示例为清楚起见离职错误处理代码。

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
    NET_PACKET_EXTENSION_QUERY extension;
    NET_PACKET_EXTENSION_QUERY_INIT(
        &extension,
        NET_PACKET_EXTENSION_CHECKSUM_NAME,
        NET_PACKET_EXTENSION_CHECKSUM_VERSION_1); 
          
    NetRxQueueGetExtension(rxQueue, &extension, &queueContext->ChecksumExtension);

    return status;
}
```

## <a name="polling-model"></a>轮询模型

NetAdapter 数据路径是轮询模型，和上一个数据包队列的轮询操作是完全独立于其他队列。 下图中所示，通过调用高级回调的客户端驱动程序的队列实现轮询模型：

![轮询流](images/polling.png)

## <a name="advancing-packet-queues"></a>前移数据包队列

数据包队列上的轮询操作序列如下所示：

1. 操作系统为传输或接收的客户端驱动程序的缓冲区。
2. 客户端驱动程序的硬件的数据包。
3. 客户端驱动程序对操作系统返回的已完成的数据包。

轮询操作发生在客户端驱动程序中[ *EvtPacketQueueAdvance* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)回调函数。 通过调用基础数据结构提供支持客户端驱动程序中的每个数据包队列*net 环*，其中包含或链接到系统内存中的实际网络数据缓冲区。 期间*EvtPacketQueueAdvance*，客户端驱动程序进行发送和接收通过使用 net 环操作*net 环迭代器*，因为数据是硬件和操作系统之间的传输缓冲区所有权传输或接收。

有关 net 环和 net 环迭代器的详细信息，请参阅[Net 环和 net 环迭代器](net-rings-and-net-ring-iterators.md)。

有关实现的示例*EvtPacketQueueAdvance*传输队列中，请参阅[发送网络数据使用 net 环](sending-network-data-with-net-rings.md)。 有关实现的示例*EvtPacketQueueAdvance*接收队列中，请参阅[接收网络数据使用 net 环](receiving-network-data-with-net-rings.md)。

## <a name="enabling-and-disabling-packet-queue-notification"></a>启用和禁用数据包队列通知

当客户端驱动程序收到数据包队列的 net 环中新的数据包时，NetAdapterCx 调用客户端驱动程序[ *EvtPacketQueueSetNotificationEnabled* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_set_notification_enabled)回调函数。 此回调到客户端驱动程序轮询指示 (的*EvtPacketQueueAdvance*或*EvtPacketQueueCancel*) 将停止，并且不会继续，直到客户端驱动程序调用[ **NetTxQueueNotifyMoreCompletedPacketsAvailable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nettxqueue/nf-nettxqueue-nettxqueuenotifymorecompletedpacketsavailable)或[ **NetRxQueueNotifyMoreReceivedPacketsAvailable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrxqueue/nf-netrxqueue-netrxqueuenotifymorereceivedpacketsavailable)。 通常情况下，PCI 设备使用此回调以启用 Tx 或 Rx 中断。 一旦收到中断，可以再次禁用中断，客户端驱动程序调用**NetTxQueueNotifyMoreCompletedPacketsAvailable**或**NetRxQueueNotifyMoreReceivedPacketsAvailable**若要触发的框架，以开始再次轮询。

### <a name="enabling-and-disabling-notification-for-a-transmit-queue"></a>启用和禁用传输队列的通知

对于 PCI NIC 启用传输队列通知通常意味着启用传输队列的硬件中断。 当硬件中断触发时，客户端调用[ **NetTxQueueNotifyMoreCompletedPacketsAvailable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nettxqueue/nf-nettxqueue-nettxqueuenotifymorecompletedpacketsavailable)从其 DPC。

同样，对于 PCI NIC，禁用队列通知意味着禁用中断与队列关联。

对于具有异步 I/O 模型的设备，客户端通常使用的内部标志来跟踪已启用的状态。 异步操作完成后，完成处理程序将检查此标志和调用[ **NetTxQueueNotifyMoreCompletedPacketsAvailable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nettxqueue/nf-nettxqueue-nettxqueuenotifymorecompletedpacketsavailable)如果将其设置。

如果调用 NetAdapterCx *EvtPacketQueueSetNotificationEnabled*与*NotificationEnabled*设置为**FALSE**，客户端不能调用[ **NetTxQueueNotifyMoreCompletedPacketsAvailable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nettxqueue/nf-nettxqueue-nettxqueuenotifymorecompletedpacketsavailable)直到 NetAdapterCx 接下来，调用此回调函数*NotificationEnabled*设置为**TRUE**.

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

### <a name="enabling-and-disabling-notification-for-a-receive-queue"></a>启用和禁用通知接收队列

PCI nic，启用接收队列通知看起来非常类似于传输队列。 这通常意味着启用接收队列的硬件中断。 当硬件中断触发时，客户端调用[ **NetRxQueueNotifyMoreReceivedPacketsAvailable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrxqueue/nf-netrxqueue-netrxqueuenotifymorereceivedpacketsavailable)从其 DPC。

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

USB 设备或软件的任何其他队列接收完成机制，客户端驱动程序应在跟踪其自己的上下文中是否启用队列的通知。 完成例程 （一条消息变为可用 USB 持续读取器中时的示例中触发），调用[ **NetRxQueueNotifyMoreReceivedPacketsAvailable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrxqueue/nf-netrxqueue-netrxqueuenotifymorereceivedpacketsavailable)如果通知是已启用。 下面的示例演示如何执行此操作。

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

## <a name="canceling-packet-queues"></a>正在取消数据包队列

当操作系统停止数据路径时，开始通过调用客户端驱动程序[ *EvtPacketQueueCancel* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_cancel)回调函数。 此回叫是客户端驱动程序在其中执行所需框架删除数据包队列之前的任何处理。 取消的传输队列是可选的取决于硬件是否支持取消操作正在进行传输，但取消接收队列是必需。 

期间*EvtPacketQueueCancel*，驱动程序使用 net 环迭代器根据需要对操作系统返回的数据包。 代码示例的传输队列和接收队列取消，请参阅[取消网络数据使用 net 环](canceling-network-data-with-net-rings.md)。

调用驱动程序的后*EvtPacketQueueCancel*回调，框架将继续，若要轮询的驱动程序[ *EvtPacketQueueAdvance* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)回调之前的所有数据包和缓冲区已返回到操作系统。
