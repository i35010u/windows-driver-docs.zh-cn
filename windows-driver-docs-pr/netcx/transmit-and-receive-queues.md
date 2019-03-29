---
title: 传输和接收队列
description: 传输和接收队列
ms.assetid: 4BF61CDF-4B62-47EB-936A-7DE81D62678A
keywords:
- NetAdapterCx 传输和接收队列，NetCx 传输和接收队列
ms.date: 03/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3696a29cbdaf4e4a08b08a7f3ef583c243c0c950
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577130"
---
# <a name="transmit-and-receive-queues"></a>传输和接收队列

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

*数据包队列*，或*数据路径队列*NetAdapterCx 以启用客户端驱动程序进行建模其硬件功能，例如硬件中引入的对象传输和更为明确地接收队列中的软件驱动程序. 本主题说明如何使用传输和接收队列中 NetAdapterCx。 

## <a name="creating-transmit-and-receive-queues"></a>创建传输和接收队列

当客户端驱动程序调用[ **NET_ADAPTER_DATAPATH_CALLBACKS_INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-net_adapter_datapath_callbacks_init)，通常是从其[ *EVT_WDF_DRIVER_DEVICE_ADD* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)事件回调函数，它提供了两个队列创建回调：[*EVT_NET_ADAPTER_CREATE_TXQUEUE* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nc-netadapter-evt_net_adapter_create_txqueue)并[ *EVT_NET_ADAPTER_CREATE_RXQUEUE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nc-netadapter-evt_net_adapter_create_rxqueue)。 客户端创建传输，并分别接收这些回调中的队列。

例如，客户端通过调用创建传输队列[ **NetTxQueueCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nettxqueue/nf-nettxqueue-nettxqueuecreate) ，如下所示：

```C++
NTSTATUS
MyEvtAdapterCreateTxQueue(
    NETADAPTER Adapter, 
    PNETTXQUEUE_INIT NetTxQueueInit
)
{
    NETPACKETQUEUE txQueue;

    // Allocate and initialize the tx queue configuration structure
    NET_PACKET_QUEUE_CONFIG txQueueConfig;
    NET_PACKET_QUEUE_CONFIG_INIT(&txQueueConfig, 
                                 EvtTxQueueAdvance,
                                 EvtTxQueueSetNotificationEnabled,
                                 EvtTxQueueCancel);

    // Optional: set the tx queue's start and stop callbacks
    txQueueConfig.EvtStart = EvtTxQueueStart;
    txQueueConfig.EvtStop = EvtTxQueueStop;

    // Assign fixed size data type as per packet context
    NET_TXQUEUE_CONFIG_SET_DEFAULT_PACKET_CONTEXT_TYPE(&txConfig, MY_CONTEXT);

    // Create the queue
    NTSTATUS status = NetTxQueueCreate(NetTxQueueInit,
                                       WDF_NO_OBJECT_ATTRIBUTES,
                                       &txQueueConfig,
                                       &txQueue);

    return status;
}
```

若要创建从接收队列[ *EVT_NET_ADAPTER_CREATE_RXQUEUE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nc-netadapter-evt_net_adapter_create_rxqueue)，使用相同的模式来调用[ **NetRxQueueCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrxqueue/nf-netrxqueue-netrxqueuecreate)。 有关示例，请参阅[ *EVT_NET_ADAPTER_CREATE_RXQUEUE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nc-netadapter-evt_net_adapter_create_rxqueue)。

Framework 转换到低功耗状态之前清空队列，并将其删除然后再删除该适配器。

## <a name="implementing-queue-callbacks"></a>实现队列回调

创建传输队列或接收队列中，数据包队列时客户端必须提供以下三个回调函数的指针：

- [*EVT_PACKET_QUEUE_ADVANCE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)
- [*EVT_PACKET_QUEUE_SET_NOTIFICATION_ENABLED*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_set_notification_enabled)
- [*EVT_PACKET_QUEUE_CANCEL*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_cancel)

此外，客户端可以初始化队列配置结构后提供这些可选的回调函数：

- [*EVT_PACKET_QUEUE_START*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_start)
- [*EVT_PACKET_QUEUE_STOP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_stop)

在客户端需要在每个事件的回调函数中执行操作中看到每个这些页面的详细信息。

## <a name="polling-model"></a>轮询模型

NetAdapter 数据路径是轮询模型，和上一个数据包队列的轮询操作是完全独立于其他队列。 下图中所示，通过调用高级回调的客户端驱动程序的队列实现轮询模型：

![轮询流](images/polling.png)

有关代码示例，请参阅[ *EVT_PACKET_QUEUE_ADVANCE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)。

轮询操作序列如下所示：

1. 操作系统为传输或接收的客户端驱动程序的缓冲区。
2. 客户端驱动程序的硬件的数据包。
3. 客户端驱动程序对操作系统返回的已完成的数据包。
