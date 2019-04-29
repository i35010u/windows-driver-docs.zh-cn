---
title: 数据中心桥接概述
description: 数据中心桥接概述
ms.assetid: FEB3FDBB-8A3C-4907-A6D0-CB5E94BCFEFF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2d945df6ce4df8239e7174ab70116953e2611b8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380580"
---
# <a name="overview-of-data-center-bridging"></a>数据中心桥接概述


IEEE 802.1 数据中心桥接 (DCB) 是一系列定义一个统一的标准 802.3 以太网媒体接口或*fabric*、 局域网 (LAN) 和存储区域网络 (SAN) 技术。 DCB 扩展当前 802.1x 桥接规范，以支持通过数据中心内相同的网络构造基于 LAN 的和基于 SAN 的应用程序共存。 DCB 还支持通过定义链接级别策略防止数据包丢失的技术，例如通过 Ethernet (FCoE) 和 iSCSI、 光纤通道。

DCB 包括指定如何网络设备进行互操作统一的数据中心结构中的以下 802.1 草稿标准：

<a href="" id="priority-based-flow-control--pfc-"></a>基于优先级的流控制 (PFC)  
在 IEEE 802.1Qbb 中指定 PFC 草案标准。 此标准是 DCB 接口 framework 的一部分。

PFC 支持通过显著减少由于拥塞的数据包丢失数据的可靠传递。 这允许丢失区分协议，如 FCoE，与传统丢失半协议通过在相同的统一构造共存。

PFC 指定直接连接的对等方之间的链接级别流量控制机制。 PFC 类似于 IEEE 802.3 暂停帧，但改为在单独的 802.1p 优先级级别上进行操作。 这允许接收端暂停发送器上任何优先级别。

PFC 的详细信息，请参阅[基于优先级的流控制 (PFC)](priority-based-flow-control--pfc.md)。

<a href="" id="enhanced-transmission-selection--ets-"></a>增强的传输选择 (ETS)  
ETS 是传输选择算法 (TSA)，IEEE 802.1Qaz 中指定的草案标准。 此标准是 DCB 接口 framework 的一部分。

ETS 分配分配给不同的 IEEE 802.1p 优先级级别的流量类之间的带宽。 每个流量类分配 directlyconnected 对等方之间的数据链路上的可用带宽的百分比。 如果流量类不使用其已分配的带宽，ETS 允许其他通信类，以使用流量类未使用的可用带宽。

ETS 的详细信息，请参阅[增强传输选择 (ETS) 算法](enhanced-transmission-selection--ets--algorithm.md)。

<a href="" id="data-center-bridging-exchange--dcbx--protocol"></a>数据中心桥接交换 (DCBX) 协议  
IEEE 802.1Qaz 还指定数据中心桥接交换 (DCBX) 协议草案标准。 DCBX 允许两个 directlyconnected 对等方之间交换 DCB 配置参数。 这样，这些对等方可以调整和优化服务质量 (QoS) 参数，以优化通过连接的数据传输。

DCBX 还用于检测冲突之间的网络适配器的 QoS 参数设置 (*本地对等方*) 和远程对等方。 根据本地和远程 QoS 参数设置，微型端口驱动程序，解决这些冲突并派生一组操作的 QoS 参数。 网络适配器按优先顺序排列的远程对等方的数据包传输使用这些操作的参数。 有关驱动程序如何解决其操作的 NDIS QoS 参数设置的详细信息，请参阅[解析操作的 NDIS QoS 参数](resolving-operational-ndis-qos-parameters.md)。

DCBX 包含结转链接层发现协议 (LLDP) 数据包的 DCB 类型-长度-值 (TLV) 设置。 在 IEEE 802.1AB 中指定 LLDP-2005 标准。

**请注意**  DCBX 指定本地对等方在任何给定时间维护只有一个远程对等方的配置参数。 因此，网络适配器保留只有一组本地、 远程和操作的 NDIS QoS 参数。

 

每个流量类 ETS 和 PFC 配置设置是与 IEEE 802.1p 优先级级别相关联。 优先级别指定为 3 位值的数据包内 802.1Q 标记。 对于 NDIS 的数据包，由指定的 802.1p 优先级级别**UserPriority**的成员[ **NDIS\_NET\_缓冲区\_列表\_8021Q\_INFO** ](https://msdn.microsoft.com/library/windows/hardware/ff566565)结构，它是与数据包的相关联[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构。

有关优先级级别的详细信息，请参阅[IEEE 802.1p 优先级](ieee-802-1p-priority-levels.md)。

 

 





