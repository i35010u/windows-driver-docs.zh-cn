---
title: IEEE 802.1p 优先级
description: IEEE 802.1p 优先级
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6cf1ab24ada27eea795db14fe6d681e11461cde
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102249088"
---
# <a name="ieee-8021p-priority-levels"></a>IEEE 802.1p 优先级


Ieee 802.1 p 已由 IEEE 802.1 任务组指定，以解决服务质量 (QoS) 的流量优先级。 802.1 p 不是单独的 IEEE 802.1 标准，但在 IEEE 802.1 Q-2005 标准的附录 G 中定义。

IEEE 802.1 p 定义了一个名为优先级码位的3位字段 (PCP) 在 IEEE 802.1 Q 标记中。 对于 NDIS 数据包，802.1 p PCP 值由与数据包的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list)结构关联的 [**NDIS \_ 网络 \_ 缓冲区 \_ 列表 \_ 8021Q \_ INFO**](/windows-hardware/drivers/ddi/nbl8021q/ns-nbl8021q-ndis_net_buffer_list_8021q_info)结构的 **UserPriority** 成员指定。

PCP 值定义了8个优先级，具有7个最高优先级，1个优先级最低。 默认情况下，优先级为0。 每个优先级别定义一 *类服务* ，用于标识传输的数据包的单独通信类。

 

