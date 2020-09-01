---
title: 流量类优先级分配
description: 流量类优先级分配
ms.assetid: 846AC7E6-28D9-4610-9493-BE547869AB15
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 586125f66db765fe6e6b73e09e53ce15bbace806
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215811"
---
# <a name="traffic-class-priority-assignment"></a>流量类优先级分配


 (ETS) 算法的增强的传输选择将指定一个方法，通过该方法可向流量类分配 802.1 p 优先级别。 ETS 是在 IEEE 802.1 Qaz 草案标准中指定的。 此标准是适用于 IEEE 802.1 数据中心桥接 (DCB) 接口的框架的一部分。

) 流量类的 NDIS 服务质量 (QoS 指定一组策略来确定网络适配器如何处理传输（或 *传出*）数据包。 在 ETS 下，为每个通信类分配一个 IEEE 802.1 p 优先级，用于传输数据包。 流量类可以分配给一个或多个 IEEE 802.1 p 优先级级别。 但是，每个 IEEE 802.1 p 优先级级别只能分配给一个通信类。

通过 [**ndis \_ qos \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters) 结构指定 ndis qos 参数。 **PriorityAssignmentTable**成员包含一个数组，该数组指定每个通信类的优先级分配。

有关优先级别的详细信息，请参阅 [IEEE 802.1 p Priority 级别](ieee-802-1p-priority-levels.md)。

 

