---
title: 基于优先级的流控制 (PFC)
description: 基于优先级的流控制 (PFC)
ms.assetid: 9DD8A66F-273F-4E5A-99EF-33C2EDF3240C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f6eca784b20a3ab4eb370449e8156a6ffca3022
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328027"
---
# <a name="priority-based-flow-control-pfc"></a>基于优先级的流控制 (PFC)


基于优先级的流控制 (PFC) 指定在 IEEE 802.1Qbb 草案标准。 此标准是 framework 的 IEEE 802.1 数据中心桥接 (DCB) 接口的一部分。

PFC 启用流控制统一 802.3 以太网媒体接口或*fabric*、 局域网 (LAN) 和存储区域网络 (SAN) 技术。 PFC 用于避免由于网络链接上的拥塞的数据包丢失。 这允许丢失区分协议，如通过 Ethernet (FCoE) 的光纤通道与传统丢失半协议通过在相同的统一构造共存。

PFC 指定直接连接的对等方之间的链路层流控制机制。 PFC 类似于 IEEE 802.3 暂停帧，但改为在单独的 802.1p 优先级级别上进行操作。 这允许接收端暂停发送器上任何的 802.1p 优先级级别。

PFC 使用 802.3 暂停帧，并将其扩展具有以下 PFC 字段：

-   应暂停指定的 802.1p 优先级级别的 8 位掩码。

-   指定应多长时间暂停该优先级级别的流量的每个优先级计时器值。

当接收方发送 PFC 数据 802.3 暂停帧时，交换机会阻止具有到在其连接接收方的端口的指定的优先级级别的帧传输。 计时器值过期时，此开关恢复暂停帧的端口上的传输。

通过指定 NDIS 服务质量 (QoS) 参数[ **NDIS\_QOS\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451640)结构。 **PfcEnable**成员包含的位图，每一位指定是否为的 802.1p 优先级级别启用 PFC。

有关优先级级别的详细信息，请参阅[IEEE 802.1p 优先级](ieee-802-1p-priority-levels.md)。

 

 





