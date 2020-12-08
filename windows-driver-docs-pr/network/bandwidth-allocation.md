---
title: 带宽分配
description: 带宽分配
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29604158a1b63b98f4121150a0f9fdd2b50a308a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805249"
---
# <a name="bandwidth-allocation"></a>带宽分配


带宽分配是增强型传输选择 (ETS) 算法的一个组件。 ETS 是在 IEEE 802.1 Qaz 草案标准中指定的。 此标准是适用于 IEEE 802.1 数据中心桥接 (DCB) 接口的框架的一部分。

在 ETS 下，将为每个通信类分配一个可用于在两个直接连接的对等方之间传输数据包的带宽百分比。 如果分配给流量类的带宽未完全使用，则 ETS 允许具有不同 IEEE 802.1 p 优先级级别的流量类共享未使用的带宽。

通过 [**ndis \_ QoS \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters) 结构指定 Ndis 服务质量 (QoS) 参数。 **TcBandwidthAssignmentTable** 成员包含一个数组，该数组指定使用 ETS 算法的流量类的带宽分配。

有关优先级别的详细信息，请参阅 [IEEE 802.1 p Priority 级别](ieee-802-1p-priority-levels.md)。

 

