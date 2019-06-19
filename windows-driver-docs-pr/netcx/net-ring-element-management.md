---
title: 网环元素管理
description: 在 Windows 中，从 Windows 10 开始中现在支持 USB 双角色控制器。
ms.date: 06/12/2019
ms.localizationpriority: medium
ms.openlocfilehash: 030ba41a3f62f31c24b7fe66808089eb6d3e0aed
ms.sourcegitcommit: 280ab1c75f30404c63d2c011549f7af16ad56f31
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2019
ms.locfileid: "67235839"
---
# <a name="net-ring-element-management"></a>网环元素管理

遵循中来管理本主题指导你[ **NET_RING** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ring/ns-ring-_net_ring)结构和其元素期间网络数据传输。 本主题中的规则描述 net 环元素客户端驱动程序的成员才能修改和时间，具体取决于数据路径方案中，以及常规信息客户端驱动程序应记住这些结构。 

> [!IMPORTANT]
> 客户端驱动程序开发的所有阶段应遵循以下说明操作。 如果客户端驱动程序不符合这些指示与测试时[Driver Verifier](../devtest/driver-verifier.md)，驱动程序验证工具将报告冲突，并触发待测试设备上的 bug 检查。

## <a name="netring"></a>NET_RING

当[ **NET_RING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ring/ns-ring-_net_ring)的启动父数据包队列，环中的所有索引都初始化为**0**。

下表描述哪些成员 net 环形驱动程序可以修改该客户端。

| 字段 | 允许修改客户端驱动程序 |
| --- | --- |
| OSReserved1 | 否 |
| ElementStride | 否 |
| NumberOfElements | 否 |
| ElementIndexMask | 否 |
| EndIndex | 否 |
| OSReserved0 | 否 |
| OSReserved2 | 否 |
| BeginIndex | 是 （必需） |
| NextIndex | （可选） 是**注意**:框架永远不会读取**NextIndex**。 |
| Scratch | （可选） 是**注意**:框架永远不会读取**Scratch**。 |
| 缓冲区 | 否 |

客户端驱动程序必须修改此结构中，任何读取只有成员也不将它们不断递增**BeginIndex**过去**EndIndex**调用[ *EvtPacketQueueAdvance*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)。

有关 net 环中的索引所有权的详细信息，请参阅[Net 环和 net 环迭代器](net-rings-and-net-ring-iterators.md)。

## <a name="netpacket"></a>NET_PACKET

中的字段[ **NET_PACKET** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/packet/ns-packet-_net_packet)易不同的上下文的数据路径进行操作。 是否数据包**忽略**字段是组和驱动程序是否正在接收 (Rx) 或传输 （德克萨斯州） 数据包更改应用于该数据包的规则集。

下表提供有关每个方案中的驱动程序说明。

| Rx 或 Tx | 忽略设置字段... | 说明 |
| --- | --- | --- |
| Rx | 客户端驱动程序 | <ul><li>在 Rx 中，客户端驱动程序设置**忽略**如果有必要和 framework 读取它。 客户端驱动程序不需要读取**忽略**Rx 期间任何时候。</li><li>如果客户端驱动程序设置**忽略**Rx，然后在字段：<ul><li>客户端驱动程序必须将写入**忽略**字段时取消任何未被成功编程到硬件的数据包的 Rx 操作。 有关详细信息，请参阅[取消网络数据使用 net 环](canceling-network-data-with-net-rings.md)。</li><li>因为它们不会释放客户端驱动程序必须将资源关联的数据包。</li></ul></li><li>如果客户端驱动程序不会设置**忽略**Rx，然后在字段：<ul><li>客户端驱动程序必须填充**FragmentIndex**， **FragmentCount**，和中的所有字段**布局**。</li><li>**FragmentIndex**必须介于**BeginIndex**非独占和**EndIndex**片段环中排他。</li><li>**FragmentCount**不能超过的之间的片段计数**BeginIndex**非独占和**EndIndex**片段环中排他。</li><li>客户端驱动程序必须移动的数据包环**BeginIndex**改用相应的片段环**BeginIndex**。</li><li>在调用[ *EvtPacketQueueAdvance*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)，如果客户端驱动程序递增数据包环**BeginIndex**然后驱动程序还必须递增片段环**BeginIndex**过去的片段以获取该数据包。 换而言之，片段环**BeginIndex**应迁移到**EndIndex**的上一个数据包片段。</li></ul></ul> |
| Tx | NetAdapterCx | <ul><li>客户端驱动程序不能修改除外的任何数据包中的任何字段**Scratch**。</li><li>客户端驱动程序可以读取的值**忽略**但必须永远不会将写入到它。</li><li>如果忽略 Tx 数据包，则驱动程序必须读取除可能的任何字段**Scratch**，如果有必要。</li></ul> |

### <a name="netpacketlayout"></a>NET_PACKET_LAYOUT

在 Rx 操作期间**布局**字段[ **NET_PACKET** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/packet/ns-packet-_net_packet)时要遵循以下规则：

- 所有字段除外**Reserved0**必须由客户端驱动程序初始化。
- 如果**Layer2Type**设置为**NetPacketLayer2TypeEthernet**，然后**Layer2HeaderLength**必须是**14**或更高版本。
- 如果**Layer2Type**设置为**NetPacketLayer2TypeNull**，然后**Layer2HeaderLength**必须设置为**0**。
- 如果**Layer3Type**为 IPv4 类型，则**Layer3HeaderLength**必须是**20**或更高版本。
- 如果**Layer3Type**为 IPv6 类型，则**Layer3HeaderLength**必须是**40**或更高版本。
- 如果**Layer4Type**设置为**Tcp**，然后**Layer4HeaderLength**必须是**40**或更高版本。
- 如果**Layer4Type**设置为**Udp**，然后**Layer4HeaderLength**必须是**8**或更高版本。
- 层类型字段必须在相应枚举范围内。

**布局**Tx 期间不使用。

## <a name="netfragment"></a>NET_FRAGMENT

[**NET_FRAGMENT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fragment/ns-fragment-_net_fragment)字段规则依赖于驱动程序是否接收或传输，以及是否片段缓冲区附加到数据包由驱动程序或框架。

| Rx 或 Tx | 说明 |
| --- | --- |
| Rx | <ul><li>客户端驱动程序无法写入**OsReserved_Bounced**字段。</li><li>如果未附加驱动程序，请**容量**不能修改，但**ValidLength**并**偏移量**必须进行修改。</li><li>如果附加驱动程序，然后**容量**， **ValidLength**，并**偏移量**必须全都可以修改。</li><li>**偏移量** + **ValidLength**必须是小于**容量**。</li></ul> |
| Tx | <ul><li>客户端驱动程序不能修改任何字段除外**Scratch**。</li></ul> |