---
title: Net 环元素管理
description: 在 Windows 中，从 Windows 10 开始中现在支持 USB 双角色控制器。
ms.date: 06/12/2019
ms.localizationpriority: medium
ms.openlocfilehash: 3fbe601e67fed2d7f30c3afb3ac13d8dced57582
ms.sourcegitcommit: 91b989fc3256267fab89c36b1fa54ff039dcc687
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "67148817"
---
# <a name="net-ring-element-management"></a>Net 环元素管理

测试与你 NetAdapterCx 客户端驱动程序时[Driver Verifier](../devtest/driver-verifier.md)，遵循中来管理本主题指导你[ **NET_RING** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ring/ns-ring-_net_ring)结构和其元素。 本主题中的规则描述 net 环元素客户端驱动程序的成员才能修改和时间，具体取决于数据路径方案中，以及常规信息客户端驱动程序应记住这些结构。 如果客户端驱动程序不符合以下说明操作，驱动程序验证工具将报告冲突，并触发待测试设备上的 bug 检查。

## <a name="netring"></a>NET_RING

当[ **NET_RING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ring/ns-ring-_net_ring)的启动父数据包队列，环中的所有索引都初始化为**0**。

下表描述哪些成员 net 环形驱动程序可以修改该客户端。

| 字段 | 允许修改客户端驱动程序 | 必需或可选修改 | 
| --- | --- | --- |
| OSReserved1 | 否 | 不可用  |
| ElementStride | 否 | 不可用 |
| NumberOfElements | 否 | 不可用 |
| ElementIndexMask | 否 | 不可用 |
| EndIndex | 否 | 不可用 |
| OSReserved0 | 否 | 不可用 |
| OSReserved2 | 否 | 不可用 |
| BeginIndex | 是 | 必需 |
| NextIndex | 是 | 可选 |
| Scratch | 是 | 可选 |
| 缓冲区 | 否 | 不可用 |

如果 net 环中出现以下任何将驱动程序验证程序报告冲突：

- If **BeginIndex** \> **EndIndex**
- 如果修改任何只读的字段

框架永远不会读取**NextIndex**或**Scratch**。

## <a name="netpacket"></a>NET_PACKET

中的字段[ **NET_PACKET** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/packet/ns-packet-_net_packet)易不同的上下文的数据路径进行操作。 是否数据包**忽略**字段是组和驱动程序是否正在接收 (Rx) 或传输 （德克萨斯州） 数据包更改应用于该数据包的规则集。

下表提供有关每个方案中的驱动程序说明。

| Rx 或 Tx | 忽略字段集 | 说明 |
| --- | --- | --- |
| Rx | 是 | <ul><li>没有为客户端驱动程序读取无意义的方式**忽略**期间 Rx 字段。</li><li>客户端驱动程序必须将写入**忽略**字段时取消 Rx 操作。</li><li>如果**忽略**设置期间 Rx，框架不会读取的任何其他字段。 因此，客户端驱动程序必须将关联资源与数据包因为它们不会被释放。</li></ul> |
| Rx | 否 | <ul><li>客户端驱动程序必须填充**FragmentIndex**， **FragmentCount**，和中的所有字段**布局**。</li><li>**FragmentIndex**必须介于**BeginIndex**非独占和**EndIndex**片段环中排他。</li><li>**FragmentCount**不能超过的之间的片段计数**BeginIndex**非独占和**EndIndex**片段环中排他。</li><li>如果客户端驱动程序移动片段将驱动程序验证程序报告冲突**BeginIndex**但不是数据包**BeginIndex**。</li><li>在调用[ *EvtPacketQueueAdvance*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacketqueue/nc-netpacketqueue-evt_packet_queue_advance)，如果客户端驱动程序递增数据包环**BeginIndex**然后驱动程序还必须递增片段环**BeginIndex**过去的片段以获取该数据包。 换而言之，片段环**BeginIndex**应迁移到**EndIndex**的上一个数据包片段。</li></ul> |
| Tx | 两者 | <ul><li>客户端驱动程序不能修改除外的任何数据包中的任何字段**Scratch**。</li></ul> |
| Tx | 是 | <ul><li>客户端驱动程序可以读取的值**忽略**但必须永远不会将写入到它。</li><li>如果忽略 Tx 数据包，则驱动程序必须读取除可能的任何字段**Scratch**，如果有必要。</li></ul> |

### <a name="netpacketlayout"></a>NET_PACKET_LAYOUT

**布局**字段[ **NET_PACKET** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/packet/ns-packet-_net_packet)时要遵循以下规则：

- 所有字段除外**Reserved0**必须由客户端驱动程序初始化。
- 如果**Layer2Type**设置为**NetPacketLayer2TypeEthernet**，然后**Layer2HeaderLength**必须是**14**或更高版本。
- 如果**Layer2Type**设置为**NetPacketLayer2TypeNull**，然后**Layer2HeaderLength**必须设置为**0**。
- 如果**Layer3Type**为 IPv4 类型，则**Layer3HeaderLength**必须是**20**或更高版本。
- 如果**Layer3Type**为 IPv6 类型，则**Layer3HeaderLength**必须是**40**或更高版本。
- 如果**Layer4Type**设置为**Tcp**，然后**Layer4HeaderLength**必须是**40**或更高版本。
- 如果**Layer4Type**设置为**Udp**，然后**Layer4HeaderLength**必须是**8**或更高版本。
- 层类型字段必须在相应枚举范围内。

## <a name="netfragment"></a>NET_FRAGMENT

[**NET_FRAGMENT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fragment/ns-fragment-_net_fragment)字段规则依赖于驱动程序是否接收或传输，以及是否片段缓冲区附加到数据包由驱动程序或框架。

| Rx 或 Tx | 说明 |
| --- | --- |
| Rx | <ul><li>客户端驱动程序无法写入**OsReserved_Bounced**字段。</li><li>如果驱动程序*不*附加，然后**容量**不能修改，但**ValidLength**并**偏移量**必须进行修改。</li><li>如果该驱动程序*是*附加，然后**容量**， **ValidLength**，以及**偏移量**必须全都可以修改。</li><li>**偏移量**必须是小于**ValidLength**。</li><li>**ValidLength**必须是小于**容量。**
| Tx | <ul><li>客户端驱动程序不能修改任何字段除外**Scratch**。</li></ul> |