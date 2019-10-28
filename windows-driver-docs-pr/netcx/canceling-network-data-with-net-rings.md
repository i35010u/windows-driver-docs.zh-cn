---
title: 使用净环取消网络数据
description: 本主题介绍 NetAdapterCx 客户端驱动程序如何使用净环和网络环迭代器来取消网络数据。
ms.assetid: 009CC1D7-5168-4D7B-9284-04F922D37434
keywords:
- NetAdapterCx，NetAdapterCx 取消数据包队列
ms.date: 01/24/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: a5d363f9161b5ea322c0951d84430b68ceeba0e4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838286"
---
# <a name="canceling-network-data-with-net-rings"></a>使用网环取消网络数据

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

NetAdapterCx 客户端驱动程序在框架为数据包队列调用其[*EvtPacketQueueCancel*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacketqueue/nc-netpacketqueue-evt_packet_queue_cancel)回调函数时，取消网络数据。 在此回调中，客户端驱动程序将在框架删除数据包队列之前执行所需的任何处理。

### <a name="canceling-a-transmit-queue"></a>取消传输队列

在传输队列的*EvtPacketQueueCancel*回调函数中，你有机会完成所有未完成的传输包。 与接收队列不同的是，您不需要这样做。 如果保留未完成的数据包，NetAdapterCx 将为传输队列调用[*EvtPacketQueueAdvance*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance) ，在此过程中，你可以在常规操作过程中处理它们。

如果硬件支持取消正在进行的传输，还应将网络环的 post 数据包迭代器前移到所有已取消的数据包。 这可能类似于以下示例：

```C++
void
MyEvtTxQueueCancel(
    NETPACKETQUEUE TxQueue
)
{
    // Get the transmit queue's context to retrieve the net ring collection
    PMY_TX_QUEUE_CONTEXT txQueueContext = MyGetTxQueueContext(TxQueue);
    NET_RING_COLLECTION const * rings = txQueueContext->Rings;

    NET_RING_PACKET_ITERATOR packetIterator = NetRingGetPostPackets(rings);
    while (NetPacketIteratorHasAny(&packetIterator))
    {
        // Mark this packet as canceled with the scratch field, then move past it
        NetPacketIteratorGetPacket(&packetIterator)->Scratch = 1;
        NetPacketIteratorAdvance(&packetIterator);
    }
    NetPacketIteratorSet(&packetIterator);
}
```

如果你的硬件不支持取消，则此回调无需采取任何措施即可返回。

### <a name="canceling-a-receive-queue"></a>取消接收队列

在接收队列的*EvtPacketQueueCancel*回调函数中，必须完成所有未完成的接收数据包。 如果不返回所有数据包，则操作系统不会删除队列，NetAdapterCx 停止为队列调用回调。 

若要返回数据包，你应该首先尝试指示在禁用接收路径时可能已指出的任何接收，然后将所有数据包都设置为忽略，并将所有片段返回到操作系统。 这可能类似于下面的代码示例。

> [!NOTE]
> 此示例提供了指示接收的详细信息。 有关接收数据的代码示例，请参阅[接收网络数据和净环](receiving-network-data-with-net-rings.md)。

```C++
void
MyEvtRxQueueCancel(
    NETPACKETQUEUE RxQueue
)
{
    // Get the receive queue's context to retrieve the net ring collection
    PMY_RX_QUEUE_CONTEXT rxQueueContext = MyGetRxQueueContext(RxQueue);
    NET_RING_COLLECTION const * rings = rxQueueContext->Rings;

    // Set hardware register for cancellation
    ...
    //

    // Indicate receives
    ...
    //

    // Get all packets and mark them for ignoring
    NET_RING_PACKET_ITERATOR packetIterator = NetRingGetAllPackets(rings);
    while(NetPacketIteratorHasAny(&packetIterator))
    {
        NetPacketIteratorGetPacket(&packetIterator)->Ignore = 1;
        NetPacketIteratorAdvance(&packetIterator);
    }
    NetPacketIteratorSet(&packetIterator);

    // Return all fragments to the OS
    NET_RING_FRAGMENT_ITERATOR fragmentIterator = NetRingGetAllFragments(rings);
    NetFragmentIteratorAdvanceToTheEnd(&fragmentIterator);
    NetFragmentIteratorSet(&fragmentIterator);
}
```
