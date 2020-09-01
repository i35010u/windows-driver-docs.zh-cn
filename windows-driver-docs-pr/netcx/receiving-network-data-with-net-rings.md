---
title: 使用净环接收网络数据
description: 本主题介绍 NetAdapterCx 客户端驱动程序如何使用净环和网络环迭代器来接收网络数据。
ms.assetid: 78D202E2-4123-4F63-9B86-48400C2CCC38
keywords:
- NetAdapterCx 网络环和网络环迭代器、NetCx 网络环和网络环迭代器、NetAdapterCx PCI 设备网络环、NetAdapterCx 异步 i/o
ms.date: 11/04/2019
ms.localizationpriority: medium
ms.custom: Vib
ms.openlocfilehash: e37105f0d811b7a00c2a2b1fbd8bc32a705837a7
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210215"
---
# <a name="receiving-network-data-with-net-rings"></a>使用网环接收网络数据

当框架为接收队列调用其 [*EvtPacketQueueAdvance*](/windows-hardware/drivers/ddi/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance) 回调函数时，NetAdapterCx 客户端驱动程序将收到网络数据。 在此回调过程中，客户端驱动程序通过将接收到的片段和数据包排出到操作系统中来指示接收，然后将新的缓冲区发布到硬件。

## <a name="receive-rx-post-and-drain-operation-overview"></a>接收 (Rx) post 和排出操作概述

以下动画说明了简单 PCI 网络接口卡 (NIC 的客户端驱动程序如何) 为 receive (Rx) 队列执行 post 和排出操作。 在此示例方案中，段缓冲区由 OS 分配并附加到片段循环。 此示例假设硬件接收队列和 OS 接收队列之间具有一对一关系。

![接收 (Rx) 的净铃声 post 和排出操作 ](images/net_ring_post_and_drain_operations_rx.gif "接收 (Rx) 的净铃声 post 和排出操作")

在此动画中，客户端驱动程序拥有的数据包以浅蓝色和深蓝突出显示，并且客户端驱动程序拥有的片段以黄色和橙色突出显示。 较亮的颜色代表驱动程序拥有的元素的 *排水管* 子节，而较暗的颜色表示驱动程序所拥有的元素的 *post* 子节。

## <a name="receiving-data-in-order"></a>按顺序接收数据

下面是按顺序接收数据的驱动程序的典型序列，每个数据包一个片段。

1. 调用 [**NetRxQueueGetRingCollection**](/windows-hardware/drivers/ddi/netrxqueue/nf-netrxqueue-netrxqueuegetringcollection) 可检索接收队列的循环集合结构。 可以将其存储在队列的上下文空间中以减少对驱动程序的调用。 使用 "环" 集合来检索接收队列的碎片环和数据包环的排水管迭代器。
2. 通过排出净环指示收到的数据到操作系统：
    1. 分配 UINT32 变量以跟踪片段环的当前索引和数据包环的当前索引。 将这些变量设置为其各自的网络环的 **BeginIndex** ，即环的排水管子部分的开头。 通过将 UINT32 变量设置为片段环的 **NextIndex**，将其分配给片段环的排出段的末尾。
    2. 在循环中执行以下操作：
        1. 检查是否已由硬件接收了片段。 如果不是，则跳出循环。
        2. 调用 [**NetRingGetFragmentAtIndex**](/windows-hardware/drivers/ddi/ring/nf-ring-netringgetpacketatindex) 以获取片段。
        3. 基于其匹配的硬件描述符填写片段的信息，例如其 **ValidLength**。
        4. 通过调用 [**NetRingGetPacketAtIndex**](/windows-hardware/drivers/ddi/ring/nf-ring-netringgetpacketatindex)获取此片段的数据包。
        5. 通过将包的 **FragmentIndex** 设置为片段中片段的当前索引，将该片段绑定到数据包，并设置在此示例中适当地 (，并将其设置为 **1**) 。 
        6. （可选）填写任何其他数据包信息，如校验和信息。
        7. 通过调用  [**NetRingIncrementIndex**](/windows-hardware/drivers/ddi/ring/nf-ring-netringincrementindex)来提升碎片索引。
        7. 通过调用  [**NetRingIncrementIndex**](/windows-hardware/drivers/ddi/ring/nf-ring-netringincrementindex)推进数据包索引。
    3. 将片段环的 **BeginIndex** 更新为当前片段索引变量，并将数据包环的 **BeginIndex** 更新为当前数据包索引，以确定接收的数据包及其对操作系统的碎片。
3. 对于下一次接收，将段缓冲区发送到硬件：    
    1. 将当前片段索引设置为片段环的 **NextIndex**，即环的 post 子节的开头。 将片段结束索引设置为片段环的 **EndIndex**。
    2. 在循环中执行以下操作：
        1. 将片段的信息发布到匹配的硬件描述符。
        2. 通过调用  [**NetRingIncrementIndex**](/windows-hardware/drivers/ddi/ring/nf-ring-netringincrementindex)来提升碎片索引。
    3. 将片段环的 **NextIndex** 更新为当前片段索引变量，以完成将碎片发送到硬件的情况。

这些步骤在代码中可能如下所示：

```cpp
void
MyEvtRxQueueAdvance(
    NETPACKETQUEUE RxQueue
)
{
    //
    // Retrieve the receive queue's ring collection and net rings. 
    // This example stores the Rx queue's ring collection in its queue context space.
    //
    PMY_RX_QUEUE_CONTEXT rxQueueContext = MyGetRxQueueContext(RxQueue);
    NET_RING_COLLECTION const * ringCollection = rxQueueContext->RingCollection;
    NET_RING * packetRing = ringCollection->Rings[NET_RING_TYPE_PACKET];
    NET_RING * fragmentRing = ringCollection->Rings[NET_RING_TYPE_FRAGMENT];
    UINT32 currentPacketIndex = 0;
    UINT32 currentFragmentIndex = 0;
    UINT32 fragmentEndIndex = 0;

    //
    // Indicate receives by draining the rings
    //
    currentPacketIndex = packetRing->BeginIndex;
    currentFragmentIndex = fragmentRing->BeginIndex;
    fragmentEndIndex = fragmentRing->NextIndex;
    while(currentFragmentIndex != fragmentEndIndex)
    {
        // Test for fragment reception. Break if fragment has not been received.
        ...
        //

        NET_FRAGMENT * fragment = NetRingGetFragmentAtIndex(fragmentRing, currentFragmentIndex);
        fragment->ValidLength = ... ;
        NET_PACKET * packet = NetRingGetPacketAtIndex(packetRing, currentPacketIndex);
        packet->FragmentIndex = currentFragmentIndex;
        packet->FragmentCount = 1;

        if(rxQueueContext->IsChecksumExtensionEnabled)
        {
            // Fill in checksum info
            ...
            //
        }        

        currentFragmentIndex = NetRingIncrementIndex(fragmentRing, currentFragmentIndex);
        currentPacketIndex = NetRingIncrementIndex(packetRing, currentPacketIndex);
    }
    fragmentRing->BeginIndex = currentFragmentIndex;
    packetRing->BeginIndex = currentPacketIndex;

    //
    // Post fragment buffers to hardware
    //
    currentFragmentIndex = fragmentRing->NextIndex;
    fragmentEndIndex = fragmentRing->EndIndex;
    while(currentFragmentIndex != fragmentEndIndex)
    {
        // Post fragment information to hardware descriptor
        ...
        //

        currentFragmentIndex = NetRingIncrementIndex(fragmentRing, currentFragmentIndex);
    }
    fragmentRing->NextIndex = currentFragmentIndex;
}
```

## <a name="receiving-data-out-of-order"></a>按顺序接收数据

与 [Tx](sending-network-data-with-net-rings.md) 队列不同的是，如果客户端驱动程序的每个硬件接收队列都有一个 OS 接收队列，则这些驱动程序通常不会按顺序接收数据。 这与客户端驱动程序的 NIC 类型无关。 无论设备是基于 PCI 的，操作系统分配并拥有接收缓冲区，还是设备是基于 USB 的并且 USB 堆栈拥有接收缓冲区，客户端驱动程序都将为收到的每个片段初始化数据包，并将其指示到操作系统。 在这种情况下，顺序并不重要。

如果硬件支持每个硬件接收队列有多个 OS 接收队列，则必须同步对接收缓冲区的访问。 此操作的范围超出了本主题的范围，并取决于您的硬件设计。