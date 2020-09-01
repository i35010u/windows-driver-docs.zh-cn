---
title: IEEE 802.1p 优先级
description: IEEE 802.1p 优先级
ms.assetid: C7EB3D85-544E-4898-A456-843621F6488D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e0e0ab2b7e4898b507b18b22ca0db56d9c426a9
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207931"
---
# <a name="ieee-8021p-priority-levels"></a>IEEE 802.1p 优先级


Ieee 802.1 p 已由 IEEE 802.1 任务组指定，以解决服务质量 (QoS) 的流量优先级。 802.1 p 不是单独的 IEEE 802.1 标准，但在 IEEE 802.1 Q-2005 标准的附录 G 中定义。

IEEE 802.1 p 定义了一个名为优先级码位的3位字段 (PCP) 在 IEEE 802.1 Q 标记中。 对于 NDIS 数据包，802.1 p PCP 值由与数据包的[**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构关联的[**NDIS \_ 网络 \_ 缓冲区 \_ 列表 \_ 8021Q \_ INFO**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_net_buffer_list_8021q_info)结构的**UserPriority**成员指定。

PCP 值定义了8个优先级，具有7个最高优先级，1个优先级最低。 默认情况下，优先级为0。 每个优先级别定义一 *类服务* ，用于标识传输的数据包的单独通信类。

 

