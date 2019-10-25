---
title: NDIS QoS 流量类
description: NDIS QoS 流量类
ms.assetid: 0DE61F97-7173-4D91-90F3-20EAFB810251
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d829028d1310601948a316ad37b1d8d5286b17e2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833762"
---
# <a name="ndis-qos-traffic-classes"></a>NDIS QoS 流量类


NDIS 服务质量（QoS）流量类指定一组策略，这些策略确定网络适配器如何处理传输或*传出*数据包的优先级传递。 每个交通类指定适用于出口数据包的下列策略：

<a href="" id="priority-level-and-flow-control"></a>优先级别和流控制  
此策略定义 IEEE 802.1 p 优先级级别和出口流量的可选流控制算法。

有关详细信息，请参阅[优先级别和流控制](priority-levels-and-flow-control.md)。

<a href="" id="traffic-selection-algorithms--tsas-"></a>流量选择算法（TSAs）  
此策略指定网络适配器如何从其传输队列中选择要传送的传出流量。 例如，适配器可以选择基于 IEEE 802.1 p 优先级的传出数据包或分配给每个通信类的出口带宽的百分比。

有关详细信息，请参阅[传输选择算法（TSAs）](transmission-selection-algorithms--tsas-.md)。

**注意**  仅支持增强型传输选择（ETS） TSA 的带宽分配。 有关详细信息，请参阅[增强的传输选择（ETS）算法](enhanced-transmission-selection--ets--algorithm.md)。

 

流量类通过[OID\_QOS\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-parameters)的对象标识符（oid）方法请求来指定。 此 OID 请求包含一个[**ndis\_QOS\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构，该结构指定以下 NDIS QOS 参数：

-   要在网络适配器上配置的流量类的数目。 每个通信类都由零到（**NumTrafficClasses**–1）范围内的一个值标识，其中**NumTrafficClasses**是[**NDIS\_QOS\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构的成员。

    **请注意**  从 Ndis 6.30 开始，ndis qos 最多支持 NDIS\_QOS\_最大\_流量\_类（8）通信类。 网络适配器必须支持至少三个通信类。

     

-   与流量类关联的 802.1 p 优先级别。

-   与流量类关联的 TSA。

-   分配给每个使用 ETS TSA 的流量类的传输带宽。

[\_QOS\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-parameters)的 oid 方法请求还指定了流量分类。 这些分类定义出站数据包和 IEEE 802.1 p 优先级级别之间的关系。 有关详细信息，请参阅[NDIS QoS 流量分类](ndis-qos-traffic-classifications.md)。

 

 





