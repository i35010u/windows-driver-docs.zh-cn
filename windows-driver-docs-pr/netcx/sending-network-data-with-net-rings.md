---
title: 使用 net 环发送网络数据
description: 本主题介绍 NetAdapterCx 客户端驱动程序如何使用 net 环和 net 环迭代器发送网络数据。
ms.assetid: 2F3DA1A5-D0C1-4928-80B2-AF41F949FF14
keywords:
- NetAdapterCx Net 环和 net 环迭代器、 NetCx Net 环和 net 环迭代器，NetAdapterCx PCI 设备 net 环 NetAdapterCx 异步 I/O
ms.date: 03/21/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 5c53052e59474ab79bbb7745508d28795a37ca75
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905333"
---
# <a name="sending-network-data-with-net-rings"></a>使用 net 环发送网络数据

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

NetAdapterCx 客户端驱动程序发送网络数据时框架调用其[ *EvtPacketQueueAdvance* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)传输队列的回调函数。 在此回调中，客户端驱动程序发布到的硬件，从队列的片段环形缓冲区，然后释放到操作系统的片段和已完成的数据包。

## <a name="transmit-tx-post-and-drain-operation-overview"></a>传输 （德克萨斯州） 文章并清空操作概述

下面的动画演示了如何简单 PCI 网络接口卡 (NIC) 的客户端驱动程序执行发布和传输 （德克萨斯州） 队列清空操作。  

![Net 环 post 并释放用于传输 (Tx) 的操作](images/net_ring_post_and_drain_operations_tx.gif "Net 环 post 和排出操作的传输 （德克萨斯州）")

在此动画中，归客户端驱动程序的数据包以浅蓝色和深色突出显示以黄色和橙色突出显示蓝色，并归客户端驱动程序的片段。 更淡的颜色表示*清空*拥有该驱动程序，而较深的颜色表示的元素的子节*发布*驱动程序拥有的元素的子节。

## <a name="sending-data-in-order"></a>按顺序发送数据

下面是典型的 post 和驱动程序的设备将传输顺序，如简单 PCI NIC 中的数据的流失序列

1. 调用**NetTxQueueGetRingCollection**检索传输队列的环集合结构。 可以将此存储在队列的上下文空间，以减少带驱动程序的调用。 
2. 发布到的硬件的数据：    
    1. 使用环集合来检索通过调用 post 迭代器的传输队列的数据包环[ **NetRingGetPostPackets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/nf-netringiterator-netringgetpostpackets)。
    2. 执行一个循环中的以下操作：
        1. 通过调用获取数据包[ **NetPacketIteratorGetPacket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/nf-netringiterator-netpacketiteratorgetpacket)使用数据包迭代器。
        2. 检查是否应忽略此数据包。 如果应忽略它，请跳到步骤 6 的此循环。 否则，继续。
        3. 此数据包片段的片段迭代器获取通过调用[ **NetPacketIteratorGetFragments**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/nf-netringiterator-netpacketiteratorgetfragments)。
        4. 执行一个循环中的以下操作：
            1. 调用[ **NetFragmentIteratorGetFragment** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/nf-netringiterator-netfragmentiteratorgetfragment)与要获取片段的片段迭代器。
            2. 翻译**NET_FRAGMENT**相关联的硬件片段描述符到的描述符。
            3. 调用[ **NetFragmentIteratorAdvance** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/nf-netringiterator-netfragmentiteratoradvance)对于此数据包将移动到下一个片段。
        5. 更新片段圈**下一步**索引以匹配片段迭代器的当前**索引**，表示该发布到硬件已完成。
        6. 调用[ **NetPacketIteratorAdvance** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/nf-netringiterator-netpacketiteratoradvance)移动到下一步的数据包。
    3. 调用[ **NetPacketIteratorSet** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/nf-netringiterator-netpacketiteratorset)以完成发布到的硬件的数据包。
3. 排出完成传输到 OS 的数据包：
    1. 使用环集合可通过调用检索漏迭代器的传输队列的数据包环[ **NetRingGetDrainPackets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/nf-netringiterator-netringgetdrainpackets)。
    2. 执行一个循环中的以下操作：
        1. 通过调用获取数据包[ **NetPacketIteratorGetPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/nf-netringiterator-netpacketiteratorgetpacket)。
        2. 检查数据包是否已完成传输。 如果没有，中断该循环。
        2. 调用[ **NetPacketIteratorAdvance** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/nf-netringiterator-netpacketiteratoradvance)移动到下一步的数据包。
    3. 调用[ **NetPacketIteratorSet** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/nf-netringiterator-netpacketiteratorset)以完成对操作系统处于排出数据包。

这些步骤可能如下所示在代码中。 请注意，为了清楚起见省略了特定于硬件的详细信息，例如如何发布到的硬件或刷新成功 post 事务描述符。

```cpp
void
MyEvtTxQueueAdvance(
    NETPACKETQUEUE TxQueue
)
{
    // Get the transmit queue's context to retrieve the net ring collection
    PMY_TX_QUEUE_CONTEXT txQueueContext = MyGetTxQueueContext(TxQueue);
    NET_RING_COLLECTION const * Rings = txQueueContext->Rings;

    //
    // Post data to hardware
    //
    NET_RING_PACKET_ITERATOR packetIterator = NetRingGetPostPackets(Rings);
    while(NetPacketIteratorHasAny(&packetIterator))
    {
        NET_PACKET* packet = NetPacketIteratorGetPacket(&packetIterator);        
        if(!packet->Ignore)
        {
            NET_FRAGMENT_ITERATOR fragmentIterator = NetPacketIteratorGetFragments(&packetIterator);
            UINT32 packetIndex = NetPacketIteratorGetIndex(&packetIterator);
            
            for(txQueueContext->PacketTransmitControlBlocks[packetIndex]->numTxDescriptors = 0; 
                NetFragmentIteratorHasAny(&fragmentIterator); 
                txQueueContext->PacketTransmitControlBlocks[packetIndex]->numTxDescriptors++)
            {
                NET_FRAGMENT* fragment = NetFragmentIteratorGetFragment(&fragmentIterator);

                // Post fragment descriptor to hardware
                ...
                //

                NetFragmentIteratorAdvance(&fragmentIterator);
            }

            //
            // Update the fragment ring's Next index to indicate that posting is complete and prepare for draining
            //
            fragmentIterator.Iterator.Rings->Rings[NET_RING_TYPE_FRAGMENT]->NextIndex = NetFragmentIteratorGetIndex(&fragmentIterator);
        }
        NetPacketIteratorAdvance(&packetIterator);
    }
    NetPacketIteratorSet(&packetIterator);

    //
    // Drain packets if completed
    //
    packetIterator = NetRingGetDrainPackets(Rings);
    while(NetPacketIteratorHasAny(&packetIterator))
    {        
        NET_PACKET* packet = NetPacketIteratorGetPacket(&packetIterator);
        
        // Test packet for transmit completion by checking hardware ownership flags in the packet's last fragment
        ..
        //
        
        NetPacketIteratorAdvance(&packetIterator);
    }
    NetPacketIteratorSet(&packetIterator);
}
```

## <a name="sending-data-out-of-order"></a>无序发送数据

驱动程序的设备可能完成传输顺序，请从订单中的设备的主要区别在于人员分配传输缓冲区以及该驱动程序如何处理传输完成的测试。 为按顺序传输的是支持 DMA 的 PCI NIC，操作系统通常会分配、 附加，并最终拥有片段缓冲区。 然后，按顺序，客户端驱动程序可以测试每个片段的相应硬件所有权标志，期间*EvtPacketQueueAdvance*。

与此模型中，请考虑一个典型的基于 USB 的 nic。 在此情况下，USB 堆栈拥有传输的内存缓冲区，这些缓冲区可能位于其他位置在系统内存中。 USB 堆栈指示完成向客户端驱动程序顺序，因此，客户端驱动程序需要在其完成回调例程期间单独记录数据包的完成状态。 若要执行此操作，客户端驱动程序可以使用的数据包**Scratch**字段中，也可以使用其他某种方法将信息存储在其队列上下文空间等。 然后，在调用[ *EvtPacketQueueAdvance*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)，客户端驱动程序将检查数据包完成测试此信息。 
