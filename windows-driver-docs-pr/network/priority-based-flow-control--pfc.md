---
title: 基于优先级的流控制 (PFC)
description: 基于优先级的流控制 (PFC)
ms.assetid: 9DD8A66F-273F-4E5A-99EF-33C2EDF3240C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 247af69aa834da65e41f92382016382176f9dd5c
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215202"
---
# <a name="priority-based-flow-control-pfc"></a>基于优先级的流控制 (PFC)


在 IEEE 802.1 Q b b 草案标准中指定 (PFC) 的基于优先级的流控制。 此标准是适用于 IEEE 802.1 数据中心桥接 (DCB) 接口的框架的一部分。

PFC 可通过适用于局域网 (LAN) 和存储区域网络 (SAN) 技术的统一802.3 以太网媒体接口（或 *构造*）启用流控制。 PFC 旨在消除网络链路上的拥塞导致的数据包丢失。 这允许丢失敏感的协议（如光纤通道 over 以太网 (FCoE) ）与同一统一结构上传统的不区分大小写的协议共存。

PFC 指定直接连接的对等方之间的链接层流控制机制。 PFC 类似于 IEEE 802.3 暂停帧，而是对单个 802.1 p 优先级别进行操作。 这允许接收方在任何 802.1 p 优先级级别暂停发送器。

PFC 使用802.3 暂停帧，并将其扩展到以下 PFC 字段：

-   一个8位掩码，用于指定应暂停的 802.1 p 优先级别。

-   每个优先级的计时器值，指定应将该优先级级别的流量暂停多长时间。

当接收方发送含 PFC 数据的802.3 暂停帧时，开关会阻止将具有指定优先级别的帧传输到连接到接收器的端口。 当计时器值过期时，开关会恢复端口上已暂停帧的传输。

通过 [**ndis \_ QoS \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters) 结构指定 Ndis 服务质量 (QoS) 参数。 **PfcEnable**成员包含一个位图，其中每个位指定是否对 802.1 p 优先级启用 PFC。

有关优先级别的详细信息，请参阅 [IEEE 802.1 p Priority 级别](ieee-802-1p-priority-levels.md)。

 

