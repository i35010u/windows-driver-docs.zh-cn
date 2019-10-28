---
title: 使用净环接收网络数据
description: 本主题介绍 NetAdapterCx 客户端驱动程序如何使用净环和网络环迭代器来接收网络数据。
ms.assetid: 78D202E2-4123-4F63-9B86-48400C2CCC38
keywords:
- NetAdapterCx 网络环和网络环迭代器、NetCx 网络环和网络环迭代器、NetAdapterCx PCI 设备网络环、NetAdapterCx 异步 i/o
ms.date: 03/21/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 3c25e65e5f8db55661071a07eec3de9e54c2b87a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838275"
---
# <a name="receiving-network-data-with-net-rings"></a>使用网环接收网络数据

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

当框架为接收队列调用其[*EvtPacketQueueAdvance*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)回调函数时，NetAdapterCx 客户端驱动程序将收到网络数据。 在此回调过程中，客户端驱动程序通过将接收到的片段和数据包排出到操作系统中来指示接收，然后将新的缓冲区发布到硬件。

## <a name="receive-rx-post-and-drain-operation-overview"></a>接收（Rx） post 和排出操作概述

以下动画说明了简单 PCI 网络接口卡（NIC）的客户端驱动程序如何为接收（Rx）队列执行 post 和排出操作。 在此示例方案中，段缓冲区由 OS 分配并附加到片段循环。 此示例假设硬件接收队列和 OS 接收队列之间具有一对一关系。

![用于接收的网络环 post 和排出操作（Rx）](images/net_ring_post_and_drain_operations_rx.gif "用于接收的网络环 post 和排出操作（Rx）")

在此动画中，客户端驱动程序拥有的数据包以浅蓝色和深蓝突出显示，并且客户端驱动程序拥有的片段以黄色和橙色突出显示。 较亮的颜色代表驱动程序拥有的元素的*排水管*子节，而较暗的颜色表示驱动程序所拥有的元素的*post*子节。

## <a name="receiving-data-in-order"></a>按顺序接收数据

下面是按顺序接收数据的驱动程序的典型序列，每个数据包一个片段。

1. 调用**NetRxQueueGetRingCollection**可检索接收队列的循环集合结构。 可以将其存储在队列的上下文空间中以减少对驱动程序的调用。 
2. 通过排出净环指示收到的数据到操作系统：
    1. 使用 "环" 集合可以通过调用[**NetRingGetDrainFragments**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringiterator/nf-netringiterator-netringgetdrainfragments)来检索接收队列的碎片循环的排出迭代器。
    2. 通过调用[**NetRingGetAllPackets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringiterator/nf-netringiterator-netringgetallpackets)获取数据包循环中所有可用数据包的数据包迭代器。
    3. 在循环中执行以下操作：
        1. 检查是否已由硬件接收了片段。 如果不是，则跳出循环。
        2. 通过调用[**NetFragmentIteratorGetFragment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringiterator/nf-netringiterator-netfragmentiteratorgetfragment)获取片段迭代器的当前片段。
        3. 基于其匹配的硬件描述符填写片段的信息，例如其**ValidLength**。
        4. 通过调用[**NetPacketIteratorGetPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringiterator/nf-netringiterator-netpacketiteratorgetpacket)获取此片段的数据包。
        5. 通过将包的**FragmentIndex**设置为片段中片段的当前索引，并适当地设置段的数量（在本示例中，将其设置为**1**），将该片段绑定到数据包。 
        6. （可选）填写任何其他数据包信息，如校验和信息。
        7. 调用[**NetFragmentIteratorAdvance**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringiterator/nf-netringiterator-netfragmentiteratoradvance)以移到下一个片段。
        7. 调用[**NetPacketIteratorAdvance**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringiterator/nf-netringiterator-netpacketiteratoradvance)以移到下一个数据包。
    4. 调用[**NetFragmentIteratorSet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringiterator/nf-netringiterator-netfragmentiteratorset)和[**NetPacketIteratorSet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringiterator/nf-netringiterator-netpacketiteratorset) ，以确定接收的数据包及其对 OS 的碎片。
3. 对于下一次接收，将段缓冲区发送到硬件：    
    1. 使用环集合可以通过调用[**NetRingGetPostFragments**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringiterator/nf-netringiterator-netringgetpostfragments)来检索接收队列的片段循环的 post 迭代器。
    2. 在循环中执行以下操作：
        1. 通过调用[**NetFragmentIteratorGetIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringiterator/nf-netringiterator-netfragmentiteratorgetindex)获取片段迭代器的当前索引。
        2. 将片段的信息发布到匹配的硬件描述符。
        3. 调用[**NetFragmentIteratorAdvance**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringiterator/nf-netringiterator-netfragmentiteratoradvance)以移到下一个片段。
    3. 调用[**NetFragmentIteratorSet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringiterator/nf-netringiterator-netfragmentiteratorset)来完成将碎片发送到硬件的情况。

这些步骤在代码中可能如下所示：

```cpp
void
MyEvtRxQueueAdvance(
    NETPACKETQUEUE RxQueue
)
{
    // Get the receive queue's context to retrieve the net ring collection
    PMY_RX_QUEUE_CONTEXT rxQueueContext = MyGetRxQueueContext(RxQueue);
    NET_RING_COLLECTION const * Rings = rxQueueContext->Rings;

    //
    // Indicate receives by draining the rings
    //
    NET_RING_FRAGMENT_ITERATOR fragmentIterator = NetRingGetDrainFragments(Rings);
    NET_RING_PACKET_ITERATOR packetIterator = NetRingGetAllPackets(Rings);
    while(NetFragmentIteratorHasAny(&fragmentIterator))
    {
        UINT32 currentFragmentIndex = NetFragmentIteratorGetIndex(&fragmentIterator);

        // Test for fragment reception
        ...
        //

        NET_FRAGMENT* fragment = NetFragmentIteratorGetFragment(&fragmentIterator);
        fragment->ValidLength = ... ;
        NET_PACKET* packet = NetPacketIteratorGetPacket(&packetIterator);
        packet->FragmentIndex = currentFragmentIndex;
        packet->FragmentCount = 1;

        if(rxQueueContext->IsChecksumExtensionEnabled)
        {
            // Fill in checksum info
            ...
            //
        }        

        NetFragmentIteratorAdvance(&fragmentIterator);
        NetPacketIteratorAdvance(&packetIterator);
    }
    NetFragmentIteratorSet(&fragmentIterator);
    NetFragmentIteratorSet(&packetIterator);

    //
    // Post fragment buffers to hardware
    //
    fragmentIterator = NetRingGetPostFragments(Rings);
    while(NetFragmentIteratorHasAny(&fragmentIterator))
    {
        UINT32 currentFragmentIndex = NetFragmentIteratorGetIndex(&fragmentIterator);

        // Post fragment information to hardware descriptor
        ...
        //

        NetFragmentIteratorAdvance(&fragmentIterator);
    }
    NetFragmentIteratorSet(&fragmentIterator);
}
```

## <a name="receiving-data-out-of-order"></a>按顺序接收数据

与[Tx](sending-network-data-with-net-rings.md)队列不同的是，如果客户端驱动程序的每个硬件接收队列都有一个 OS 接收队列，则这些驱动程序通常不会按顺序接收数据。 这与客户端驱动程序的 NIC 类型无关。 无论设备是基于 PCI 的，操作系统分配并拥有接收缓冲区，还是设备是基于 USB 的并且 USB 堆栈拥有接收缓冲区，客户端驱动程序都将为收到的每个片段初始化数据包，并将其指示到操作系统。 在这种情况下，顺序并不重要。

如果硬件支持每个硬件接收队列有多个 OS 接收队列，则必须同步对接收缓冲区的访问。 此操作的范围超出了本主题的范围，并取决于您的硬件设计。
