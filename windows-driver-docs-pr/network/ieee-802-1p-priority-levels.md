---
title: IEEE 802.1p 优先级
description: IEEE 802.1p 优先级
ms.assetid: C7EB3D85-544E-4898-A456-843621F6488D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa371d0aa3c86aebf8416254adbb34a248ff273e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823824"
---
# <a name="ieee-8021p-priority-levels"></a>IEEE 802.1p 优先级


Ieee 802.1 p 已由 IEEE 802.1 任务组指定，以解决服务质量（QoS）的流量优先级。 802.1 p 不是单独的 IEEE 802.1 标准，但在 IEEE 802.1 Q-2005 标准的附录 G 中定义。

IEEE 802.1 p 定义了一个名为的3位字段，该字段称为优先级码位（PCP）。 对于 NDIS 数据包，802.1 p PCP 值由[**NDIS\_NET\_缓冲器\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_net_buffer_list_8021q_info)的**UserPriority**成员指定，与数据包的[**NET\_缓冲区相关联\_8021Q\_INFO 结构\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构。

PCP 值定义了8个优先级，具有7个最高优先级，1个优先级最低。 默认情况下，优先级为0。 每个优先级别定义一*类服务*，用于标识传输的数据包的单独通信类。

 

 





