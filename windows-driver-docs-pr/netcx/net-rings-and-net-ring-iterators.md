---
title: Net 环和 net 环迭代器简介
description: 本主题介绍 net 环和 net 环迭代器。
ms.assetid: 8A56AA21-264C-4C1A-887E-92C9071E8AB8
keywords:
- Net 环和 net 环迭代器，NetCx 简介 net 环和 net 环迭代器，NetAdapterCx PCI 设备 net 环，NetAdapterCx 异步 I/O NetAdapterCx 简介
ms.date: 07/01/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: e67eaf4d6e21b4ad7e291e8a627b25f696fd1035
ms.sourcegitcommit: 6f74454e7ed5e703e4e4b363b6816652950e6a51
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2019
ms.locfileid: "67608513"
---
# <a name="introduction-to-net-rings-and-net-ring-iterators"></a>Net 环和 net 环迭代器简介

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

## <a name="netring-overview"></a>NET_RING 概述

一个**NET_RING**是 NetAdapterCx 和客户端驱动程序之间共享的网络数据的循环缓冲区。 客户端驱动程序中的每个数据包队列具有两个环：*数据包环*核心数据包描述符和一个*片段环*每个数据包片段描述符。

有关数据包描述符的详细信息，请参阅[数据包描述符和扩展](packet-descriptors-and-extensions.md)。

在数据包环中的每个核心描述符具有用于查找该数据包片段描述符的片段环中的索引。 另一种数据结构， **NET_RING_COLLECTION**，如以下关系图中所示的数据包环和片段环一起为指定的数据包队列的分组。

![多环布局](images/multi-ring.png) 

数据包的每个队列都具有其自己**NET_RING_COLLECTION**结构和其自己的数据包环，，因此，片段环，以及这些环中的描述符。 因此，网络数据传输操作中的每个数据包队列是完全独立的。 若要了解有关数据包队列的详细信息，请参阅[传输和接收队列](transmit-and-receive-queues.md)。

## <a name="netring-element-ownership"></a>NET_RING 元素的所有权

在每个元素**NET_RING**归客户端驱动程序或 NetAdapterCx。 由三个索引，将标记的部分控制所有权**NET_RING**。 这些索引是下表中所述。 将移动这些索引，执行哪些客户端驱动程序调用的行为[Net 环迭代器接口](#net-ring-iterator-interface-overview)，由描述*发布*并*清空*语义。 

| **NET_RING**索引名称 | 描述 | 所需的网络数据传输 | 修改者 |
| --- | --- | --- | --- |
| BeginIndex | 中的元素范围的开头**NET_RING**拥有 NIC 客户端驱动程序。 **BeginIndex**也是开头*清空*一部分**NET_RING**。 当**BeginIndex**就会递增，驱动程序*清空后*到 OS 的元素从它们的环和传输的所有权。 | 是 | NIC 客户端驱动程序，通过 Net 环迭代器接口 API 调用 |
| NextIndex | 开头*发布*一部分**NET_RING**。 **NextIndex**将客户端驱动程序拥有的环的一部分划分为 post 和漏小节。 当**NextIndex**就会递增，驱动程序*文章*硬件和环的流失部分缓冲区传输到缓冲区。 | 否 | NIC 客户端驱动程序，通过 Net 环迭代器接口 API 调用 |
| EndIndex | 中的元素范围的末尾**NET_RING**拥有 NIC 客户端驱动程序。 客户端驱动程序最多拥有元素**EndIndex-1**非独占。 | 是 | NetAdapterCx |

在数据包队列的过程中使用 net 环迭代器操作这些索引[ *EvtPacketQueueAdvance* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)回调是客户端驱动程序如何在系统和网络接口之间传输网络数据卡 (NIC) 的硬件。

客户端驱动程序拥有从每个元素**BeginIndex**到**EndIndex-1**非独占。 例如，如果**BeginIndex**为 2 和**EndIndex**为 5，客户端驱动程序拥有三个元素： 2、 3 和 4 的索引值的元素。

如果**BeginIndex**等于**EndIndex**，客户端驱动程序不拥有任何元素。

NetAdapterCx 发到环形缓冲区的元素通过递增**EndIndex**。 客户端驱动程序耗尽缓冲区，并通过前调的环漏迭代器，递增返回的元素的所有权**BeginIndex**。

**NextIndex**对于客户端驱动程序，若要使用，是可选的提供为了方便起见，在分隔的 post 和漏子部分中，客户端驱动程序的部分中的环。

元素之间的索引值**NextIndex**并**EndIndex-1**非独占归客户端，但您尚未发布到的硬件。 如果**NextIndex**等于**BeginIndex**，客户端驱动程序不具有任何已完成的缓冲区将传输到操作系统。 如果**NextIndex**等于**EndIndex**，客户端驱动程序不具有任何缓冲区来发布到硬件。

因为 net 环是循环，最终的索引值环绕缓冲区的末尾，再返回到开始。 NetAdapterCx 自动处理包装沿环的索引值，当客户端驱动程序调用适当的方法下, 一节中所述。

有关管理 net 环中的元素的特定信息，请参阅[Net 环元素管理](net-ring-element-management.md)。

## <a name="net-ring-iterator-interface-overview"></a>Net 环迭代器接口概述

NIC 客户端驱动程序执行 post，并通过调入清空操作 net 环*Net 环迭代器接口*。 一个[ **NET_RING_ITERATOR** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/ns-netringiterator-_net-ring-iterator)是一个小结构，包含对 post 和消耗的索引引用**NET_RING**它所属。 

每个**NET_RING**可以有多个迭代器。 例如，数据包环可能涵盖环的流失部分的迭代器 (*清空迭代器*)，涵盖环的 post 部分的迭代器 (*发布迭代器*)，和一个迭代器介绍了这两个 post 和消耗的部分。 同样，片段环可以具有相同的迭代器。

为了方便客户端驱动程序来控制每个迭代器的每个环，网络接口的环迭代器时，可将迭代器为两个类别：[**NET_RING_PACKET_ITERATOR** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/ns-netringiterator-_net-ring-packet-iterator)并[ **NET_RING_FRAGMENT_ITERATOR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/ns-netringiterator-_net-ring-fragment-iterator)。 这些是周围的包装结构**NET_RING_ITERATOR**和所有 Net 环迭代器接口 API 调用中使用。 客户端驱动程序不应使用**NET_RING_ITERATOR**直接。 相反，它们应适当类型的迭代器用于给定 net 环 （数据包或片段）。

通过获取、 改进，并设置 net 环迭代器，客户端驱动程序发送和接收数据包队列内的网络数据。 客户端驱动程序还在 net 环迭代器访问的环元素上调用方法。

Net 环迭代器的数据结构和方法的完整列表，请参阅[Netringiterator.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringiterator/)。

## <a name="sending-and-receiving-network-data-with-net-rings-and-net-ring-iterators"></a>发送和接收网络数据使用 net 环和 net 环迭代器

请参阅有关 net 环中的发送和收到网络数据的详细信息和代码示例的以下主题。

[使用 net 环发送网络数据](sending-network-data-with-net-rings.md)

[使用 net 环接收网络数据](receiving-network-data-with-net-rings.md)
