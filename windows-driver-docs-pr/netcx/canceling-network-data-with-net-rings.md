---
title: 取消使用 net 环的网络数据
description: 本主题介绍 NetAdapterCx 客户端驱动程序如何使用 net 环和 net 环迭代器取消网络数据。
ms.assetid: 009CC1D7-5168-4D7B-9284-04F922D37434
keywords:
- NetAdapterCx NetAdapterCx Net 环和 net 环迭代器取消，取消数据包队列
ms.date: 01/24/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: fc85c6e9a39614c753f33d7a72b760d3294a0fec
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905282"
---
# <a name="canceling-network-data-with-net-rings"></a>取消使用 net 环网络数据

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

NetAdapterCx 客户端驱动程序取消网络数据时框架调用其[ *EvtPacketQueueCancel* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_cancel)数据包队列的回调函数。 此回叫是客户端驱动程序在其中执行所需框架删除数据包队列之前的任何处理。

### <a name="canceling-a-transmit-queue"></a>正在取消的传输队列

在你*EvtPacketQueueCancel*回调函数的传输队列中，您有机会来完成的任何未完成传输数据包。 与不同接收队列中，您不需要执行此操作。 如果将未完成的数据包，NetAdapterCx 调用你[ *EvtPacketQueueAdvance* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)传输队列，其中常规操作过程中处理它们。

如果您取消正在进行的硬件支持传输，您还应转过去的所有已取消的数据包的 net 环 post 数据包迭代器。 这看起来像下面的示例：

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

如果您的硬件不支持取消，此回调可以返回不采取任何操作。

### <a name="canceling-a-receive-queue"></a>正在取消接收队列

在你*EvtPacketQueueCancel*回调函数接收队列，必须完成的任何未完成的接收数据包。 如果未返回所有数据包，操作系统不会删除队列，并 NetAdapterCx 停止队列调用回调。 

若要返回的数据包，你应第一次尝试以指示任何接收可能已指明了时接收路径已被禁用，然后将设置所有数据包可被忽略并返回到操作系统的所有片段。 这看起来像下面的代码示例。

> [!NOTE]
> 此示例中省略了详细信息的该值指示接收。 接收数据的代码示例，请参阅[接收网络数据使用 net 环](receiving-network-data-with-net-rings.md)。

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
