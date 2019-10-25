---
title: 网环和网环迭代器的简介
description: 本主题介绍了网络环和网络环迭代器。
ms.assetid: 8A56AA21-264C-4C1A-887E-92C9071E8AB8
keywords:
- NetAdapterCx 介绍网络环和网络环迭代器、NetCx 介绍网络环和网络环迭代器、NetAdapterCx PCI 设备网络环、NetAdapterCx 异步 i/o
ms.date: 07/01/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 7ece878b12451d110a9f247e36ba654b3fde28b2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835523"
---
# <a name="introduction-to-net-rings-and-net-ring-iterators"></a>网环和网环迭代器的简介

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

## <a name="net_ring-overview"></a>NET_RING 概述

**NET_RING**是在 NetAdapterCx 和客户端驱动程序之间共享的网络数据的循环缓冲区。 客户端驱动程序中的每个数据包队列都有两个环：核心数据包描述符的*数据包环*，以及每个数据包的碎片描述符的*碎片环*。

有关数据包描述符的详细信息，请参阅[数据包描述符和扩展](packet-descriptors-and-extensions.md)。

数据包环中的每个核心描述符都在片段环中包含用于查找数据包的片段描述符的索引。 另一种数据结构**NET_RING_COLLECTION**将数据包环和分段环组集中给给定的数据包队列，如下图所示。

![多环布局](images/multi-ring.png) 

每个数据包队列都有其自己的**NET_RING_COLLECTION**结构，因此，在这些环中，它自己的数据包环、片段环和说明符。 因此，每个数据包队列的网络数据传输操作都是完全独立的。 若要了解有关数据包队列的详细信息，请参阅[传输和接收队列](transmit-and-receive-queues.md)。

## <a name="net_ring-element-ownership"></a>NET_RING 元素所有权

**NET_RING**中的每个元素都属于客户端驱动程序或 NetAdapterCx。 所有权由三个索引控制，这三个索引标记**NET_RING**的各部分。 下表描述了这些索引。 使用*post*和*排出*语义来描述移动这些索引的操作，这些客户端驱动程序通过调用[Net 环形迭代器接口](#net-ring-iterator-interface-overview)来执行此操作。 

| **NET_RING**索引名称 | 描述 | 传输网络数据所必需的 | 修改者 |
| --- | --- | --- | --- |
| BeginIndex | NIC 客户端驱动程序拥有的**NET_RING**中的元素范围的开头。 **BeginIndex**也是**NET_RING**的*排水管*部分的开头。 当**BeginIndex**增加时，驱动程序将从环中*排出*元素，并将它们的所有权转移到 OS。 | “是” | NIC 客户端驱动程序，通过 Net 环形迭代器接口 API 调用 |
| NextIndex | **NET_RING**的*post*部分的开头。 **NextIndex**将客户端驱动程序所拥有的环形部分分成了 post 和排水管部分。 当**NextIndex**增加时，驱动程序会将缓冲区*发送*到硬件，并将缓冲区传输到环的排出区。 | 无 | NIC 客户端驱动程序，通过 Net 环形迭代器接口 API 调用 |
| EndIndex | NIC 客户端驱动程序拥有的**NET_RING**中的元素范围的末尾。 客户端驱动程序拥有的元素最多**EndIndex-1** （含）。 | “是” | NetAdapterCx |

在数据包队列的[*EvtPacketQueueAdvance*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)回调期间，使用 net 环形迭代器操作这些索引是客户端驱动程序在系统和网络接口卡（NIC）硬件之间传输网络数据的方式。

客户端驱动程序拥有从**BeginIndex**到**EndIndex 的**每个元素，其中包含。 例如，如果**BeginIndex**为2， **EndIndex**为5，则客户端驱动程序将拥有三个元素：索引值为2、3和4的元素。

如果**BeginIndex**等于**EndIndex**，则客户端驱动程序不拥有任何元素。

NetAdapterCx 通过递增**EndIndex**将元素发布到环形缓冲区。 客户端驱动程序会耗尽缓冲区并返回元素的所有权，方法是：向前增加**BeginIndex**。

对于要使用的客户端驱动程序， **NextIndex**是可选的，为方便起见，可以分隔环的客户端驱动程序部分的 post 和排出子节。

索引值介于**NextIndex**和**EndIndex-1**之间的元素由客户端拥有，但尚未发布到硬件。 如果**NextIndex**等于**BeginIndex**，则客户端驱动程序不会有任何已完成的缓冲区传输到 OS。 如果**NextIndex**等于**EndIndex**，则客户端驱动程序不会有任何要发布到硬件的缓冲区。

因为网络环是圆形的，所以，最终索引值会绕过缓冲区的末尾并返回到开始处。 当客户端驱动程序调用适当的方法时，NetAdapterCx 会自动处理环绕圆圈的索引值，如以下部分所述。

有关管理网络环中的元素的特定信息，请参阅[网络环元素管理](net-ring-element-management.md)。

## <a name="net-ring-iterator-interface-overview"></a>网络环迭代器接口概述

NIC 客户端驱动程序通过调入*网络环迭代器接口*，对网络环执行 post 和排出操作。 [**NET_RING_ITERATOR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringiterator/ns-netringiterator-_net-ring-iterator)是一个小型结构，其中包含对其所属**NET_RING**的 post 和排出索引的引用。 

每个**NET_RING**可以有多个迭代器。 例如，数据包环可能包含一个迭代器，该迭代器涵盖环的排出部分（*排出迭代器*）、涵盖环的 post 部分的迭代器（ *post 迭代*器）以及同时涵盖 post 和排出部分的迭代器。 同样，片段环可以具有相同的迭代器。

为了便于客户端驱动程序控制每个环的每个迭代器，Net 环形迭代器接口将迭代器分为两类： [**NET_RING_PACKET_ITERATOR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringiterator/ns-netringiterator-_net-ring-packet-iterator)和[**NET_RING_FRAGMENT_ITERATOR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringiterator/ns-netringiterator-_net-ring-fragment-iterator)。 这些是围绕**NET_RING_ITERATOR**的包装结构，并用于所有 NET 环形迭代器接口 API 调用。 客户端驱动程序不应直接使用**NET_RING_ITERATOR** 。 相反，它们应为给定的网络环（数据包或片段）使用适当类型的迭代器。

通过获取、前进和设置网络环形迭代器，客户端驱动程序会在其数据包队列中发送和接收网络数据。 客户端驱动程序还会调用网络环迭代器上的方法以访问环的元素。

有关 net 环形迭代器数据结构和方法的完整列表，请参阅[Netringiterator](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringiterator/)。

## <a name="sending-and-receiving-network-data-with-net-rings-and-net-ring-iterators"></a>通过网络环和网络环迭代器发送和接收网络数据

请参阅以下主题，了解有关在 net 振铃中发送和收到网络数据的详细信息和代码示例。

[用网络环发送网络数据](sending-network-data-with-net-rings.md)

[接收带网络环的网络数据](receiving-network-data-with-net-rings.md)
