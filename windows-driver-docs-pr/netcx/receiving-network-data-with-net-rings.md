---
title: 使用 net 环接收网络数据
description: 本主题介绍 NetAdapterCx 客户端驱动程序如何使用 net 环和 net 环迭代器接收网络数据。
ms.assetid: 78D202E2-4123-4F63-9B86-48400C2CCC38
keywords:
- NetAdapterCx Net 环和 net 环迭代器、 NetCx Net 环和 net 环迭代器，NetAdapterCx PCI 设备 net 环 NetAdapterCx 异步 I/O
ms.date: 03/21/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 4d01bdddbbf40a4ad1e7d1f687160f762a42b10c
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905295"
---
# <a name="receiving-network-data-with-net-rings"></a>使用 net 环接收网络数据

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

NetAdapterCx 客户端驱动程序接收网络数据时框架调用其[ *EvtPacketQueueAdvance* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)接收队列的回调函数。 在此回调期间客户端驱动程序指示通过接收排出收到片段和数据包的操作系统，然后发布到的硬件的新缓冲区。

## <a name="receive-rx-post-and-drain-operation-overview"></a>接收 (Rx) 文章和清空操作概述

下面的动画说明了如何简单 PCI 网络接口卡 (NIC) 的客户端驱动程序执行发布和接收 (Rx) 队列的消耗操作。 在此示例方案的片段缓冲区分配，并附加到片段环由操作系统。 此示例假定硬件之间的一对一关系接收队列和 OS 接收队列。

![Net 环 post 并释放用于接收 (Rx) 的操作](images/net_ring_post_and_drain_operations_rx.gif "Net 环 post 并释放用于接收 (Rx) 的操作")

在此动画中，归客户端驱动程序的数据包以浅蓝色和深色突出显示以黄色和橙色突出显示蓝色，并归客户端驱动程序的片段。 更淡的颜色表示*清空*拥有该驱动程序，而较深的颜色表示的元素的子节*发布*驱动程序拥有的元素的子节。

## <a name="receiving-data-in-order"></a>按顺序接收数据

下面是用于接收订单，与每个数据包的一个片段中的数据的驱动程序的典型序列。

1. 调用**NetRxQueueGetRingCollection**检索接收队列环集合结构。 可以将此存储在队列的上下文空间，以减少带驱动程序的调用。 
2. 通过清空 net 环来表示接收到 OS 的数据：
    1. 使用环集合来检索漏迭代器用于通过调用接收队列片段环[ **NetRingGetDrainFragments**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/nf-netringiterator-netringgetdrainfragments)。
    2. 获取数据包迭代器的所有可用数据包数据包环中通过调用[ **NetRingGetAllPackets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/nf-netringiterator-netringgetallpackets)。
    3. 执行一个循环中的以下操作：
        1. 检查硬件是否接收片段。 如果没有，中断该循环。
        2. 通过调用获取片段迭代器的当前片段[ **NetFragmentIteratorGetFragment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/nf-netringiterator-netfragmentiteratorgetfragment)。
        3. 如填写片段的信息，其**ValidLength**根据其匹配的硬件描述符。
        4. 调用此片段中获取数据包[ **NetPacketIteratorGetPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/nf-netringiterator-netpacketiteratorgetpacket)。
        5. 绑定到数据包片段，通过设置数据包**FragmentIndex**片段的片段环和适当地设置的片段数中的当前索引 (在此示例中，它设置为**1**). 
        6. （可选） 填写任何其他数据包信息如校验和信息。
        7. 调用[ **NetFragmentIteratorAdvance** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/nf-netringiterator-netfragmentiteratoradvance)将移动到下一个片段。
        7. 调用[ **NetPacketIteratorAdvance** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/nf-netringiterator-netpacketiteratoradvance)移动到下一步的数据包。
    4. 调用[ **NetFragmentIteratorSet** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/nf-netringiterator-netfragmentiteratorset)并[ **NetPacketIteratorSet** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/nf-netringiterator-netpacketiteratorset)来完成，该值指示接收到的数据包和到其片段OS。
3. 接收到下一个硬件 post 片段缓冲区：    
    1. 使用环集合来检索通过调用 post 迭代器，以供接收队列片段环[ **NetRingGetPostFragments**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/nf-netringiterator-netringgetpostfragments)。
    2. 执行一个循环中的以下操作：
        1. 通过调用获取片段迭代器的当前索引[ **NetFragmentIteratorGetIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/nf-netringiterator-netfragmentiteratorgetindex)。
        2. 发布到匹配的硬件描述符的片段的信息。
        3. 调用[ **NetFragmentIteratorAdvance** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/nf-netringiterator-netfragmentiteratoradvance)将移动到下一个片段。
    3. 调用[ **NetFragmentIteratorSet** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/nf-netringiterator-netfragmentiteratorset)以完成发布到的硬件的片段。

在代码中时，这些步骤可能类似以下形式：

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

## <a name="receiving-data-out-of-order"></a>无序接收数据

与不同[Tx](sending-network-data-with-net-rings.md)队列，客户端驱动程序通常不接收数据无序如果他们有一个操作系统接收每个硬件队列中接收队列。 这与无关的类型的客户端驱动程序的 nic。 是否设备是基于 PCI 的和操作系统分配并拥有接收缓冲区中，或是否设备是基于 USB 的并 USB 堆栈拥有接收缓冲区，客户端驱动程序初始化每个片段收到数据包以及指示到 OS。 顺序在这种情况下并不重要。

如果您的硬件支持每个硬件接收队列的多个 OS 接收队列，必须同步接收缓冲区的访问。 这样做的作用域因此超出本主题以及什么依赖于硬件的设计。
