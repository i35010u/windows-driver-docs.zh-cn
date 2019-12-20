---
title: 网环元素管理
description: 从 Windows 10 开始，Windows 现在支持 USB 双重角色控制器。
ms.date: 06/12/2019
ms.localizationpriority: medium
ms.openlocfilehash: dac454983ea6a5b92168176611a0989a4628c469
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210805"
---
# <a name="net-ring-element-management"></a>网环元素管理

按照本主题中的指导来管理网络数据传输过程中的[**NET_RING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ring/ns-ring-_net_ring)结构及其元素。 本主题中的规则说明了客户端驱动程序可以修改哪些网络环元素的成员以及何时（具体取决于数据路径方案）以及一般信息客户端驱动程序应记住这些结构。 

> [!IMPORTANT]
> 在开发过程中，客户端驱动程序应遵循这些说明。 如果客户端驱动程序在使用[驱动程序验证](../devtest/driver-verifier.md)器进行测试时不遵循这些说明，则驱动程序验证程序会报告冲突，并在受测设备上触发 bug 检查。

## <a name="net_ring"></a>NET_RING

启动[**NET_RING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ring/ns-ring-_net_ring)的父数据包队列时，环中的所有索引都将初始化为**0**。

下表描述了客户端驱动程序可以修改的网络环的成员。

| 字段 | 允许修改客户端驱动程序 |
| --- | --- |
| OSReserved1 | 无 |
| ElementStride | 无 |
| NumberOfElements | 无 |
| ElementIndexMask | 无 |
| EndIndex | 无 |
| OSReserved0 | 无 |
| OSReserved2 | 无 |
| BeginIndex | 是（必需） |
| NextIndex | 是（可选）**注意**：框架从不读取**NextIndex**。 |
| Scratch | 是（可选）**注意**：框架永远不会**读取。** |
| 缓冲区 | 无 |

客户端驱动程序不能修改此结构的任何只读成员，也不应在调用[*EvtPacketQueueAdvance*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)时，它们是否会将过去的**EndIndex**增加**BeginIndex** 。

有关网络环中的索引所有权的详细信息，请参阅[净环简介](introduction-to-net-rings.md)。

## <a name="net_packet"></a>NET_PACKET

[**NET_PACKET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/packet/ns-packet-_net_packet)中的字段对数据路径操作的不同上下文都是敏感的。 如果设置了数据包的**Ignore**字段以及驱动程序是否正在接收（Rx）或传输（Tx）数据包，则数据包将更改应用于数据包的规则集。

下表提供了每种方案中的驱动程序的说明。

| Rx 或 Tx | 忽略字段由设置 .。。 | 注释 |
| --- | --- | --- |
| Rx | 客户端驱动程序 | <ul><li>在 Rx 期间，如果需要，客户端驱动程序会将其**忽略**，并且框架将读取它。 客户端驱动程序不需要在 Rx 期间的**任何时间点**都不需要读取。</li><li>如果客户端驱动程序在 Rx 期间设置了**Ignore**字段，则：<ul><li>如果为任何未成功编程到硬件的数据包取消 Rx 操作，则客户端驱动程序必须向 "**忽略**" 字段写入。 有关详细信息，请参阅[取消网络数据和网络环](canceling-network-data-with-net-rings.md)。</li><li>客户端驱动程序不能将资源与数据包相关联，因为它们不会被释放。</li></ul></li><li>如果客户端驱动程序未在 Rx 期间设置 "**忽略**" 字段，则：<ul><li>客户端驱动程序必须填充**布局**中的**FragmentIndex**、 **FragmentCount**和所有字段。</li><li>**FragmentIndex**必须在片段环中的**BeginIndex**和**EndIndex**之间。</li><li>在片段环中， **FragmentCount**不能超过**BeginIndex**和**EndIndex**独占的碎片计数。</li><li>如果客户端驱动程序移动了相应的片段环**BeginIndex**，则必须移动该**BeginIndex** 。</li><li>调用[*EvtPacketQueueAdvance*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)之后，如果客户端驱动程序增加了数据包环**BeginIndex** ，则驱动程序还必须递增片段环**BeginIndex** ，使其超出该数据包的碎片。 换句话说，片段环形**BeginIndex**应移到先前包的片段的**EndIndex** 。</li></ul></ul> |
| Tx | NetAdapterCx | <ul><li>除**暂存**外，客户端驱动程序不得修改任何数据包中的任何字段。</li><li>客户端驱动程序可以读取**Ignore**的值，但绝不能对其进行写入。</li><li>如果已忽略 Tx 数据包，则驱动程序不得读取除可能这样的任何字段 **（如有**必要）。</li></ul> |

### <a name="net_packet_layout"></a>NET_PACKET_LAYOUT

在 Rx 操作期间， [**NET_PACKET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/packet/ns-packet-_net_packet)的 "**布局**" 字段服从以下规则：

- 除**Reserved0**之外的所有字段都必须由客户端驱动程序初始化。
- 如果**Layer2Type**设置为**NetPacketLayer2TypeEthernet**，则**Layer2HeaderLength**必须为**14**或更大。
- 如果**Layer2Type**设置为**NetPacketLayer2TypeNull**，则**Layer2HeaderLength**必须设置为**0**。
- 如果**Layer3Type**是 IPv4 类型，则**Layer3HeaderLength**必须为**20**或更大。
- 如果**Layer3Type**是 IPv6 类型，则**Layer3HeaderLength**必须是**40**或更高版本。
- 如果**Layer4Type**设置为**Tcp**，则**Layer4HeaderLength**必须是**40**或更高版本。
- 如果**Layer4Type**设置为**Udp**，则**Layer4HeaderLength**必须等于或大于**8** 。
- 层类型字段必须位于适当的枚举范围内。

在 Tx 期间不使用**布局**。

## <a name="net_fragment"></a>NET_FRAGMENT

[**NET_FRAGMENT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fragment/ns-fragment-_net_fragment)字段规则取决于驱动程序是否正在接收或传输，以及碎片缓冲区是由驱动程序还是框架附加到数据包。

| Rx 或 Tx | 注释 |
| --- | --- |
| Rx | <ul><li>客户端驱动程序无法写入**OsReserved_Bounced**字段。</li><li>如果驱动程序未附加，则不能修改**容量**，但必须修改**ValidLength**和**Offset** 。</li><li>如果驱动程序正在附加，则必须修改 "**容量**"、" **ValidLength**" 和 "**偏移**"。</li><li> + **ValidLength**的**偏移量**必须小于**容量**。</li></ul> |
| Tx | <ul><li>除**暂存**外，客户端驱动程序不能修改任何字段。</li></ul> |