---
title: 增强的传输选择 (ETS) 算法
description: 增强的传输选择 (ETS) 算法
ms.assetid: 952ECB1E-96AD-4717-8E49-68558E7E9AD4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16fe042990e221972b542c577ff8af4302cfd652
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838122"
---
# <a name="enhanced-transmission-selection-ets-algorithm"></a>增强的传输选择 (ETS) 算法


增强的传输选择（ETS）是由 IEEE 802.1 Qaz 草案标准指定的传输选择算法（TSA）。 此标准是适用于 IEEE 802.1 数据中心桥接（DCB）接口的框架的一部分。

仅基于 IEEE 802.1 p 优先级级别的传输选择可能会导致更高优先级的流量阻止降低优先级的流量。 ETS 通过允许将最小数量的带宽分配给分配给不同 802.1 p 优先级级别的流量类，确保了公平。

为每个通信类分配了直接连接的对等方之间的数据链路上的可用带宽的百分比。 如果流量类不使用其分配的带宽，ETS 允许其他流量类使用流量类未使用的可用带宽。

通过 oid [\_qos 方法\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-parameters)定义 NDIS 服务质量（QoS）通信类。 此 OID 请求包含一个[**NDIS\_QOS\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构，该结构指定以下流量类属性：

-   **NumTrafficClasses**成员指定的流量类的数目。

-   流量类使用的 TSA。 这由**TsaAssignmentTable**成员指定。 如果流量类的表元素设置为 NDIS\_QOS\_TSA\_ETS，则该流量类将使用 ETS TSA。

-   分配给交通类的 802.1 p 优先级。 流量类可以分配给一个或多个优先级别。 但是，每个优先级别只能分配给一个通信类。

    有关详细信息，请参阅[流量类优先级分配](traffic-class-priority-assignment.md)。

-   为流量类分配的带宽。 这由**TcBandwidthAssignmentTable**成员指定。 此表仅对使用 ETS TSA 的流量类有效。

    有关 ETS 带宽分配的详细信息，请参阅[带宽分配](bandwidth-allocation.md)。

有关优先级别的详细信息，请参阅[IEEE 802.1 p Priority 级别](ieee-802-1p-priority-levels.md)。

 

 





