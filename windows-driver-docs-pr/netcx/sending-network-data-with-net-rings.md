---
title: 使用净环发送网络数据
description: 本主题介绍 NetAdapterCx 客户端驱动程序如何使用净环和网络环迭代器发送网络数据。
ms.assetid: 2F3DA1A5-D0C1-4928-80B2-AF41F949FF14
keywords:
- NetAdapterCx 网络环和网络环迭代器、NetCx 网络环和网络环迭代器、NetAdapterCx PCI 设备网络环、NetAdapterCx 异步 i/o
ms.date: 11/01/2019
ms.localizationpriority: medium
ms.custom: Vib
ms.openlocfilehash: 26a2670ba00cb15eff935d5d0892bac05124a465
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75208997"
---
# <a name="sending-network-data-with-net-rings"></a>使用网环发送网络数据

当框架为传输队列调用其[*EvtPacketQueueAdvance*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)回调函数时，NetAdapterCx 客户端驱动程序将发送网络数据。 在此回调过程中，客户端驱动程序会将队列片段中的缓冲区发送到硬件，然后将完成的数据包和碎片排出回操作系统。

## <a name="transmit-tx-post-and-drain-operation-overview"></a>传输（Tx） post 和排出操作概述

以下动画说明了简单 PCI 网络接口卡（NIC）的客户端驱动程序如何为传输（Tx）队列执行 post 和排出操作。  

![用于传输的网络环 post 和排出操作（Tx）](images/net_ring_post_and_drain_operations_tx.gif "用于传输的网络环 post 和排出操作（Tx）")

在此动画中，客户端驱动程序拥有的数据包以浅蓝色和深蓝突出显示，并且客户端驱动程序拥有的片段以黄色和橙色突出显示。 较亮的颜色代表驱动程序拥有的元素的*排水管*子节，而较暗的颜色表示驱动程序所拥有的元素的*post*子节。

## <a name="sending-data-in-order"></a>按顺序发送数据

下面是驱动程序的典型 post 和排出序列，其设备按顺序传输数据，如简单 PCI NIC。

1. 调用[**NetTxQueueGetRingCollection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nettxqueue/nf-nettxqueue-nettxqueuegetringcollection)以检索传输队列的循环集合结构。 可以将其存储在队列的上下文空间中以减少对驱动程序的调用。 使用 "环" 集合来检索传输队列的数据包环。
2. 将数据发布到硬件：        
    1. 为数据包索引分配一个 UINT32 变量并将其设置为数据包环的**NextIndex**，这是环的 post 子节的开头。
    2. 在循环中执行以下操作：
        1. 通过使用数据包索引调用[**NetRingGetPacketAtIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ring/nf-ring-netringgetpacketatindex)来获取数据包。
        2. 检查是否应忽略此数据包。 如果应忽略此循环，请跳到此循环的步骤6。 否则，请继续。
        3. 获取此数据包的片段。 从环集合中检索传输队列的片段环，从数据包的**FragmentIndex**成员检索数据包片段的开头，并通过使用数据包的**FragmentCount**调用[**NetRingIncrementIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ring/nf-ring-netringincrementindex)来检索数据包的碎片结尾。
        4. 在循环中执行以下操作：
            1. 调用[**NetRingGetFragmentAtIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ring/nf-ring-netringgetpacketatindex)以获取片段。
            2. 将**NET_FRAGMENT**描述符转换为关联的硬件片段描述符。
            3. 通过调用[**NetRingIncrementIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ring/nf-ring-netringincrementindex)来提升碎片索引。
        5. 更新片段环的**下一个**索引，以匹配片段迭代器的当前**索引**，这表示发布到硬件完成。
        6. 通过调用[**NetRingIncrementIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ring/nf-ring-netringincrementindex)推进数据包索引。
    3. 将数据包环的**NextIndex**更新为数据包索引，以完成将数据包发送到硬件的工作。
3. 排出已完成将数据包传输到操作系统：
    1. 将数据包索引设置为数据包环的**BeginIndex**，即环的排水管子部分的开头。
    2. 在循环中执行以下操作：
        1. 通过使用数据包索引调用[**NetRingGetPacketAtIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ring/nf-ring-netringgetpacketatindex)来获取数据包。
        2. 检查数据包是否已完成传输。 如果没有，则中断循环。
        3. 通过调用[**NetRingIncrementIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ring/nf-ring-netringincrementindex)推进数据包索引。
    3. 将数据包环的**BeginIndex**更新为数据包索引，以完成将数据包发送到硬件的工作。

这些步骤在代码中可能与此类似。 请注意，特定于硬件的详细信息，例如如何向硬件发布描述符或刷新成功的 post 事务，以清楚地说明。

```cpp
void
MyEvtTxQueueAdvance(
    NETPACKETQUEUE TxQueue
)
{
    //
    // Retrieve the transmit queue's ring collection and packet ring. 
    // This example stores the Tx queue's ring collection in its queue context space.
    //
    PMY_TX_QUEUE_CONTEXT txQueueContext = MyGetTxQueueContext(TxQueue);
    NET_RING_COLLECTION const * ringCollection = txQueueContext->RingCollection;
    NET_RING * packetRing = ringCollection->Rings[NET_RING_TYPE_PACKET];
    UINT32 currentPacketIndex = 0;

    //
    // Post data to hardware
    //      
    currentPacketIndex = packetRing->NextIndex;
    while(currentPacketIndex != packetRing->EndIndex)
    {
        NET_PACKET * packet = NetRingGetPacketAtIndex(packetRing, currentPacketIndex);        
        if(!packet->Ignore)
        {
            NET_RING * fragmentRing = ringCollection->Rings[NET_RING_TYPE_FRAGMENT];
            UINT32 currentFragmentIndex = packet->FragmentIndex;
            UINT32 fragmentEndIndex = NetRingIncrementIndex(fragmentRing, currentFragmentIndex + packet->FragmentCount - 1);
            
            for(txQueueContext->PacketTransmitControlBlocks[packetIndex]->numTxDescriptors = 0; 
                currentFragmentIndex != fragmentEndIndex; 
                txQueueContext->PacketTransmitControlBlocks[packetIndex]->numTxDescriptors++)
            {
                NET_FRAGMENT * fragment = NetRingGetFragmentAtIndex(fragmentRing, currentFragmentIndex);

                // Post fragment descriptor to hardware
                ...
                //

                currentFragmentIndex = NetRingIncrementIndex(fragmentRing, currentFragmentIndex);
            }

            //
            // Update the fragment ring's Next index to indicate that posting is complete and prepare for draining
            //
            fragmentRing->NextIndex = currentFragmentIndex;
        }
        currentPacketIndex = NetRingIncrementIndex(packetRing, currentPacketIndex);
    }
    packetRing->NextIndex = currentPacketIndex;

    //
    // Drain packets if completed
    //
    currentPacketIndex = packetRing->BeginIndex;
    while(currentPacketIndex != packetRing->NextIndex)
    {        
        NET_PACKET * packet = NetRingGetPacketAtIndex(packetRing, currentPacketIndex); 
        
        // Test packet for transmit completion by checking hardware ownership flags in the packet's last fragment
        // Break if transmit is not complete
        ...
        //
        
        currentPacketIndex = NetRingIncrementIndex(packetRing, currentPacketIndex);
    }
    packetRing->BeginIndex = currentPacketIndex;
}
```

## <a name="sending-data-out-of-order"></a>按顺序发送数据

对于设备可能按顺序完成传输的驱动程序，与按序设备的主要区别在于谁分配传输缓冲区，以及驱动程序如何处理传输完成的测试。 对于具有 DMA 功能的 PCI NIC 的按序传输，操作系统通常会分配、附加并最终拥有片段缓冲区。 然后，在*EvtPacketQueueAdvance*期间，客户端驱动程序可以测试每个片段的相应硬件所有权标志。

与此模型不同的是，请考虑使用典型的基于 USB 的 NIC。 在这种情况下，USB 堆栈拥有用于传输的内存缓冲区，这些缓冲区可能位于系统内存中的其他位置。 USB 堆栈按顺序指示客户端驱动程序的完成，因此，客户端驱动程序需要在其完成回调例程期间单独记录数据包的完成状态。 为此，客户端驱动程序可以使用数据包的**暂存**字段，也可以使用其他方法，例如在其队列上下文空间中存储信息。 然后，在调用[*EvtPacketQueueAdvance*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)时，客户端驱动程序会检查此信息以进行数据包完成测试。 
