---
title: 使用环形缓冲区
description: 使用环形缓冲区
ms.assetid: 8A56AA21-264C-4C1A-887E-92C9071E8AB8
keywords:
- NetAdapterCx 使用环形缓冲区，使用环形缓冲区、 NetCx NetAdapterCx PCI 设备环形缓冲区，NetAdapterCx 异步 I/O
ms.date: 03/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 50cf916654fcf6853029454808174b583a05476e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569440"
---
# <a name="using-the-ring-buffer"></a>使用环形缓冲区

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

一个[ **NET_RING_BUFFER** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringbuffer/ns-netringbuffer-_net_ring_buffer)是一个或多个循环缓冲区[ **NET_PACKET** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacket/ns-netpacket-_net_packet) NetAdapterCx 之间共享的结构和客户端。 若要访问队列的数据包环形缓冲区，请先调用**NetRx （德克萨斯州） QueueGetDatapathDescriptor**若要获取队列的数据路径描述符结构，然后调用[NET_DATAPATH_DESCRIPTOR_GET_PACKET_RING_BUFFER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdatapathdescriptor/nf-netdatapathdescriptor-net_datapath_descriptor_get_packet_ring_buffer)宏来获取环形缓冲区。

数据包环形缓冲区中的每个元素被归客户端驱动程序或 NetAdapterCx。 索引成员的值控制所有权。 具体而言，客户端驱动程序拥有从每个元素**BeginIndex**到**EndIndex-1**非独占。

例如，如果**BeginIndex**为 2 和**EndIndex**为 5，客户端驱动程序拥有三个元素： 2、 3 和 4 的索引值的元素。
如果**BeginIndex**等于**EndIndex**，客户端驱动程序不拥有任何元素。

NetAdapterCx 将元素添加到环形缓冲区，通过递增**EndIndex**。 客户端驱动程序通过递增返回的元素的所有权**BeginIndex**。

客户端驱动程序可能会根据需要设置**NextIndex**到它将提交到的硬件的下一个数据包的索引。

![使用环形缓冲区](images/using-the-ring-buffer.gif "使用环形缓冲区")

在此模型中，客户端提交了索引值之间的数据包**BeginIndex**并**NextIndex-1** （含) 到硬件。 索引值之间的数据包**NextIndex**并**EndIndex-1**归客户端，但尚未发送到的硬件。 如果的值**BeginIndex**的值相等**NextIndex**，客户端不具有编程到硬件的任何数据包。

客户端的硬件传输或接收数据后，将推进**BeginIndex**将的数据包的所有权转让给 NetAdapterCx。 如果客户端跟踪数据包完成使用**Completed**标志**NET_PACKET_FRAGMENT**，客户端可以调用[ **NetRingBufferReturnCompletedPackets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapterpacket/nf-netadapterpacket-netringbufferreturncompletedpackets)前进**BeginIndex**自动通过每个已完成数据包。

由于环形缓冲区是循环，最终的索引值环绕缓冲区的末尾，再返回到开始。 若要处理环绕递增环形缓冲区索引时，调用[ **NetRingBufferIncrementIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringbuffer/nf-netringbuffer-netringbufferincrementindex)。

## <a name="pci-device-drivers"></a>PCI 设备驱动程序

在硬件级别 (例如，典型 PCI Nic) 通常使用环形缓冲区的设备的驱动程序操作[ **NET_RING_BUFFER** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringbuffer/ns-netringbuffer-_net_ring_buffer)直接索引。

下面是 PCI 设备驱动程序的典型序列：

1. 调用[ **NetRxQueueGetDatapathDescriptor** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrxqueue/nf-netrxqueue-netrxqueuegetdatapathdescriptor)或[ **NetTxQueueGetDatapathDescriptor** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nettxqueue/nf-nettxqueue-nettxqueuegetdatapathdescriptor)检索队列的数据路径描述符。 可以将此存储在队列的上下文空间，以减少带驱动程序的调用。
2. 使用数据路径描述，可通过调用检索队列的数据包环形缓冲区[NET_DATAPATH_DESCRIPTOR_GET_PACKET_RING_BUFFER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdatapathdescriptor/nf-netdatapathdescriptor-net_datapath_descriptor_get_packet_ring_buffer)。
3. 通过循环直到环形缓冲区编程到硬件的数据包**NextIndex**等于**EndIndex**:
    1. 调用[ **NetRingBufferGetPacketAtIndex** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapterpacket/nf-netadapterpacket-netringbuffergetpacketatindex)上**NextIndex**。
    2. 翻译**NET_PACKET**相关联的硬件数据包描述符到的描述符。
    3. 调用[ **NetRingBufferIncrementIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringbuffer/nf-netringbuffer-netringbufferincrementindex)。
4. 通过循环直到完成数据包**BeginIndex**等于**NextIndex** ，或达到数据包不完整：
    1. 调用[ **NetRingBufferGetPacketAtIndex** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapterpacket/nf-netadapterpacket-netringbuffergetpacketatindex)上**BeginIndex**。
    2. 检测到相关联的硬件描述符如果表示完成。 如果没有，终止。
    3. 转换到的硬件描述符[ **NET_PACKET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacket/ns-netpacket-_net_packet)。
    4. 调用[ **NetRingBufferIncrementIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringbuffer/nf-netringbuffer-netringbufferincrementindex)。

## <a name="device-drivers-with-asynchronous-io"></a>使用异步 I/O 的设备驱动程序

使用异步 I/O 模型，如 USB、 设备为目标的客户端驱动程序的同时还可以修改[ **NET_RING_BUFFER** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringbuffer/ns-netringbuffer-_net_ring_buffer)索引直接，我们建议改为使用更高级别例程管理扩展的顺序完成：

* [**NetRingBufferAdvanceNextPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapterpacket/nf-netadapterpacket-netringbufferadvancenextpacket)
* [**NetRingBufferGetNextPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapterpacket/nf-netadapterpacket-netringbuffergetnextpacket)
* [**NetRingBufferReturnCompletedPackets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapterpacket/nf-netadapterpacket-netringbufferreturncompletedpackets)

下面是使用异步 I/O 的设备驱动程序的典型序列：

1. 调用[ **NetRxQueueGetDatapathDescriptor** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netrxqueue/nf-netrxqueue-netrxqueuegetdatapathdescriptor)或[ **NetTxQueueGetDatapathDescriptor** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nettxqueue/nf-nettxqueue-nettxqueuegetdatapathdescriptor)检索队列的数据路径描述符。
2. 使用数据路径描述，可通过调用检索队列的数据包环形缓冲区[NET_DATAPATH_DESCRIPTOR_GET_PACKET_RING_BUFFER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdatapathdescriptor/nf-netdatapathdescriptor-net_datapath_descriptor_get_packet_ring_buffer)。
3. 循环访问环形缓冲区中的数据包。 通常情况下，执行以下操作在循环中：
    1. 调用[ **NetRingBufferGetNextPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapterpacket/nf-netadapterpacket-netringbuffergetnextpacket)。
    2. 若要接收或传输的程序硬件。 这会启动异步 I/O。
    3. 调用[ **NetRingBufferAdvanceNextPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapterpacket/nf-netadapterpacket-netringbufferadvancenextpacket)。
4. 调用[ **NetRingBufferReturnCompletedPackets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapterpacket/nf-netadapterpacket-netringbufferreturncompletedpackets)。

已逐渐异步 I/O 完成，客户端设置**Completed**标志的第一个关联[ **NET_PACKET_FRAGMENT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacket/ns-netpacket-_net_packet_fragment)到**TRUE**. 这使得[ **NetRingBufferReturnCompletedPackets** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapterpacket/nf-netadapterpacket-netringbufferreturncompletedpackets)完成数据包。 若要访问第一个相关联**NET_PACKET_FRAGMENT**的数据包时，调用[NET_PACKET_GET_FRAGMENT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdatapathdescriptor/nf-netdatapathdescriptor-net_packet_get_fragment)宏替换数据包队列的数据路径描述符和*0*编制索引的参数。
