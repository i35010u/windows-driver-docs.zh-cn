---
title: NDIS QoS 流量类
description: NDIS QoS 流量类
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e1d75e31433eaa114beeddaa9d08e5329db28e4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801545"
---
# <a name="ndis-qos-traffic-classes"></a>NDIS QoS 流量类


) 流量类的 NDIS 服务质量 (QoS 指定一组策略，这些策略确定网络适配器如何处理传输（或 *传出*）用于确定优先级的传送的数据包。 每个交通类指定适用于出口数据包的下列策略：

<a href="" id="priority-level-and-flow-control"></a>优先级别和流控制  
此策略定义 IEEE 802.1 p 优先级级别和出口流量的可选流控制算法。

有关详细信息，请参阅 [优先级别和流控制](ieee-802-1p-priority-levels.md)。

<a href="" id="traffic-selection-algorithms--tsas-"></a>流量选择算法 (TSAs)   
此策略指定网络适配器如何从其传输队列中选择要传送的传出流量。 例如，适配器可以选择基于 IEEE 802.1 p 优先级的传出数据包或分配给每个通信类的出口带宽的百分比。

有关详细信息，请参阅 [传输选择算法 (TSAs) ](transmission-selection-algorithms--tsas-.md)。

**注意**  仅 (ETS) TSA 的增强传输选择支持带宽分配。 有关详细信息，请参阅 [ (ETS) 算法的增强传输选择](enhanced-transmission-selection--ets--algorithm.md)。

 

流量类通过对象标识符 (oid [ \_ QOS \_ 参数](./oid-qos-parameters.md)的 oid) 方法请求来指定。 此 OID 请求包含用于指定以下 NDIS QoS 参数的 [**ndis \_ qos \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters) 结构：

-   要在网络适配器上配置的流量类的数目。 每个交通类都由零到 (**NumTrafficClasses**– 1) 的范围内的一个值标识，其中 **NumTrafficClasses** 是 [**NDIS \_ QOS \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters) 结构的成员。

    **注意**  从 NDIS 6.30 开始，NDIS QoS 最多支持 NDIS \_ qos \_ 最大 \_ 流量 \_ 类 (8) 通信类。 网络适配器必须支持至少三个通信类。

     

-   与流量类关联的 802.1 p 优先级别。

-   与流量类关联的 TSA。

-   分配给每个使用 ETS TSA 的流量类的传输带宽。

[Oid \_ QOS \_ 参数](./oid-qos-parameters.md)的 oid 方法请求还指定了流量分类。 这些分类定义出站数据包和 IEEE 802.1 p 优先级级别之间的关系。 有关详细信息，请参阅 [NDIS QoS 流量分类](ndis-qos-traffic-classifications.md)。

 

