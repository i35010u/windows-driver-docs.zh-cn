---
title: 带宽分配
description: 带宽分配
ms.assetid: 775B4085-6028-441F-9D52-341077FF1647
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e24d2f66f9ad5fe97e215d65009510f4e9a8175
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835274"
---
# <a name="bandwidth-allocation"></a>带宽分配


带宽分配是增强型传输选择（ETS）算法的一个组件。 ETS 是在 IEEE 802.1 Qaz 草案标准中指定的。 此标准是适用于 IEEE 802.1 数据中心桥接（DCB）接口的框架的一部分。

在 ETS 下，将为每个通信类分配一个可用于在两个直接连接的对等方之间传输数据包的带宽百分比。 如果分配给流量类的带宽未完全使用，则 ETS 允许具有不同 IEEE 802.1 p 优先级级别的流量类共享未使用的带宽。

通过[**ndis\_QoS\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构指定 Ndis 服务质量（QoS）参数。 **TcBandwidthAssignmentTable**成员包含一个数组，该数组指定使用 ETS 算法的流量类的带宽分配。

有关优先级别的详细信息，请参阅[IEEE 802.1 p Priority 级别](ieee-802-1p-priority-levels.md)。

 

 





