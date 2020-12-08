---
title: 使用净环取消网络数据
description: 本主题介绍 NetAdapterCx 客户端驱动程序如何使用净环和网络环迭代器来取消网络数据。
keywords:
- NetAdapterCx，NetAdapterCx 取消数据包队列
ms.date: 11/01/2019
ms.localizationpriority: medium
ms.custom: Vib
ms.openlocfilehash: 24b79e92e94ec03c2ca85c15224aaa882e6b4e8e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834389"
---
# <a name="canceling-network-data-with-net-rings"></a>使用网环取消网络数据

NetAdapterCx 客户端驱动程序在框架为数据包队列调用其 [*EvtPacketQueueCancel*](/windows-hardware/drivers/ddi/netpacketqueue/nc-netpacketqueue-evt_packet_queue_cancel) 回调函数时，取消网络数据。 在此回调中，客户端驱动程序将在框架删除数据包队列之前执行所需的任何处理。

### <a name="canceling-a-transmit-queue"></a>取消传输队列

在传输队列的 *EvtPacketQueueCancel* 回调函数中，你有机会完成所有未完成的传输包。 与接收队列不同的是，您不需要这样做。 如果保留未完成的数据包，NetAdapterCx 将为传输队列调用 [*EvtPacketQueueAdvance*](/windows-hardware/drivers/ddi/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance) ，在此过程中，你可以在常规操作过程中处理它们。

如果硬件支持取消正在进行的传输，还应将网络环的 post 数据包迭代器前移到所有已取消的数据包。 这可能类似于以下示例：

```C++
void
MyEvtTxQueueCancel(
    NETPACKETQUEUE TxQueue
)
{
    // Get the transmit queue's context to retrieve the net ring collection
    PMY_TX_QUEUE_CONTEXT txQueueContext = MyGetTxQueueContext(TxQueue);
    NET_RING_COLLECTION const * ringCollection = txQueueContext->RingCollection;
    NET_RING * packetRing = ringCollection->Rings[NET_RING_TYPE_PACKET];
    UINT32 currentPacketIndex = packetRing->BeginIndex;
    UINT32 packetEndIndex = packetRing->EndIndex;

    while (currentPacketIndex != packetEndIndex)
    {
        // Mark this packet as canceled with the scratch field, then move past it
        NET_PACKET * packet = NetRingGetPacketAtIndex(packetRing, currentPacketIndex);
        packet->Scratch = 1;
        currentPacketIndex = NetRingIncrementIndex(packetRing, currentPacketIndex);
    }
    
    packetRing->BeginIndex = packetRing->EndIndex;
}
```

如果你的硬件不支持取消，则此回调无需采取任何措施即可返回。

### <a name="canceling-a-receive-queue"></a>取消接收队列

在接收队列的 *EvtPacketQueueCancel* 回调函数中，必须完成所有未完成的接收数据包。 如果不返回所有数据包，则操作系统不会删除队列，NetAdapterCx 停止为队列调用回调。 

若要返回数据包，你应该首先尝试指示在禁用接收路径时可能已指出的任何接收，然后将所有数据包都设置为忽略，并将所有片段返回到操作系统。 这可能类似于下面的代码示例。

> [!NOTE]
> 此示例提供了指示接收的详细信息。 有关接收数据的代码示例，请参阅 [接收网络数据和净环](receiving-network-data-with-net-rings.md)。

```C++
void
MyEvtRxQueueCancel(
    NETPACKETQUEUE RxQueue
)
{
    // Get the receive queue's context to retrieve the net ring collection
    PMY_RX_QUEUE_CONTEXT rxQueueContext = MyGetRxQueueContext(RxQueue);
    NET_RING_COLLECTION const * ringCollection = rxQueueContext->RingCollection;
    NET_RING * packetRing = ringCollection->Rings[NET_RING_TYPE_PACKET];
    NET_RING * fragmentRing = ringCollection->Rings[NET_RING_TYPE_FRAGMENT];
    UINT32 currentPacketIndex = packetRing->BeginIndex;
    UINT32 packetEndIndex = packetRing->EndIndex;

    // Set hardware register for cancellation
    ...
    //

    // Indicate receives
    ...
    //

    // Get all packets and mark them for ignoring
    currentPacketIndex = packetRing->BeginIndex;
    while(currentPacketIndex != packetEndIndex)
    {
        NET_PACKET * packet = NetRingGetPacketAtIndex(packetRing, currentPacketIndex);
        packet->Ignore = 1;
        currentPacketIndex = NetRingIncrementIndex(packetRing, currentPacketIndex);
    }
    
    packetRing->BeginIndex = packetRing->EndIndex;

    // Return all fragments to the OS
    fragmentRing->BeginIndex = fragmentRing->EndIndex;
}
```
