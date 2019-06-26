---
title: NDIS QoS 流量类
description: NDIS QoS 流量类
ms.assetid: 0DE61F97-7173-4D91-90F3-20EAFB810251
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1d60685e6bb08405adf399517c441ccf9bdd0c2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369162"
---
# <a name="ndis-qos-traffic-classes"></a>NDIS QoS 流量类


NDIS 服务质量 (QoS) 通信类指定一组策略，以确定网络适配器如何处理传输，或*出口*，为优先传送的数据包。 每个流量类指定应用于传出数据包的以下策略：

<a href="" id="priority-level-and-flow-control"></a>优先级别和流控制  
此策略定义的传出流量的 IEEE 802.1p 优先级级别和可选的流控制算法。

有关详细信息，请参阅[优先级别和流控制](priority-levels-and-flow-control.md)。

<a href="" id="traffic-selection-algorithms--tsas-"></a>流量选择算法 (TSAs)  
此策略指定如何将网络适配器选择从其传输队列交付的出口流量。 例如，适配器可以选择基于 IEEE 802.1p 优先级或分配给每个流量类的出口带宽的百分比的传出数据包。

有关详细信息，请参阅[传输选择算法 (TSAs)](transmission-selection-algorithms--tsas-.md)。

**请注意**  带宽分配仅支持为增强传输选择 (ETS) TSA。 有关详细信息，请参阅[增强传输选择 (ETS) 算法](enhanced-transmission-selection--ets--algorithm.md)。

 

流量类指定的对象标识符 (OID) 的方法请求通过[OID\_QOS\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-parameters)。 此 OID 请求包含[ **NDIS\_QOS\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构，它指定以下的 NDIS QoS 参数：

-   流量类上的网络适配器配置的数目。 从零到范围中的值来标识每个流量类 (**NumTrafficClasses**-1)，其中**NumTrafficClasses**属于[ **NDIS\_QOS\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构。

    **请注意**  从 NDIS 6.30，NDIS QoS 支持最多为 NDIS\_QOS\_最大\_流量\_类 (8) 通信类。 网络适配器必须支持至少三个通信类。

     

-   流量类与关联的 802.1p 优先级级别。

-   TSA 与流量类相关联。

-   分配到每个流量类，该类使用 ETS TSA 的传输带宽。

OID 的方法请求[OID\_QOS\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-parameters)还指定流量分类。 这些分类定义流出数据包和 IEEE 802.1p 优先级级别之间的关系。 有关详细信息，请参阅[NDIS QoS 流量分类](ndis-qos-traffic-classifications.md)。

 

 





