---
title: 增强的传输选择 (ETS) 算法
description: 增强的传输选择 (ETS) 算法
ms.assetid: 952ECB1E-96AD-4717-8E49-68558E7E9AD4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2314820381f4ce2a6e5b568383763ffd809f8023
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379419"
---
# <a name="enhanced-transmission-selection-ets-algorithm"></a>增强的传输选择 (ETS) 算法


增强传输选择 (ETS) 是由 IEEE 802.1Qaz 指定传输选择算法 (TSA) 标准草案。 此标准是 framework 的 IEEE 802.1 数据中心桥接 (DCB) 接口的一部分。

在其中优先级较高的流量阻止优先级较低的流量的情况下可能会导致传输所选内容取决于 IEEE 802.1p 优先级级别。 ETS 最少量的带宽，并将其分配到分配给不同的 802.1p 优先级级别的通信类别，从而确保公平度。

每个流量类被分配的直接连接的对等方之间的数据链接上的可用带宽的百分比。 如果流量类不使用其已分配的带宽，ETS 允许其他通信类，以使用流量类未使用的可用带宽。

NDIS 服务质量 (QoS) 通信类定义的 OID 方法请求通过[OID\_QOS\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-parameters)。 此 OID 请求包含[ **NDIS\_QOS\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_qos_parameters)指定以下流量类特性的结构：

-   流量类的指定数目**NumTrafficClasses**成员。

-   流量类使用的 TSA。 这通过指定**TsaAssignmentTable**成员。 如果流量类的表元素设置为 NDIS\_QOS\_TSA\_ETS，流量类使用 ETS TSA。

-   分配给流量类的 802.1p 优先级。 流量类可以分配给一个或多个优先级别。 但是，每个优先级别只能分配到一个通信类。

    有关详细信息，请参阅[流量类优先级分配](traffic-class-priority-assignment.md)。

-   流量类分配的带宽。 这通过指定**TcBandwidthAssignmentTable**成员。 此表时才有效使用 ETS TSA 的通信类。

    ETS 带宽分配的详细信息，请参阅[带宽分配](bandwidth-allocation.md)。

有关优先级级别的详细信息，请参阅[IEEE 802.1p 优先级](ieee-802-1p-priority-levels.md)。

 

 





