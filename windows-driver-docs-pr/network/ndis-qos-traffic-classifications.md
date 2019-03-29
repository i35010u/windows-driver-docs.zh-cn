---
title: NDIS QoS 流量分类
description: NDIS QoS 流量分类
ms.assetid: 62D7B69F-A64E-4E3C-9AEA-8C56495E3FF5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4179312c64f862ec8fc7409bb9e63cbc191faf1f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566722"
---
# <a name="ndis-qos-traffic-classifications"></a>NDIS QoS 流量分类


NDIS 服务质量 (QoS) 将分为两类传输，或*出口*，为网络适配器的优先传送的数据包。 流量的每个分类有如下规定：

-   一种分类*条件*基于传出数据包数据中的数据模式。

    从 NDIS 6.30 开始，分类条件基于一个 16 位值，例如，UDP 或 TCP 目标端口或媒体访问控制 (MAC) 以太网类型。

-   一种分类*操作*，它定义要用于处理传出数据包的流量类。

    从 NDIS 6.30 开始，分类操作指定的 802.1p 优先级级别。

**请注意**  流量分类也被称为"应用程序优先级"IEEE 802.1 规范中的。

 

NDIS QoS 流量分类适用于以下类型的传出数据包流量：

-   根据流量卸载到微型端口驱动程序，如通过 Ethernet (FCoE) 或 iSCSI 数据包的光纤通道的数据包。

-   基于连接的管理，并强制实施微型端口驱动程序，如 RDMA 的数据包。

由于 NDIS QoS 流量分类不适用于所生成的操作系统的 TCP/IP 流量，则不需要执行数据包检查微型端口驱动程序。 相反，如果分类条件匹配的数据包类型已卸载或已由驱动程序，它可以简单地分类操作应用到属于该类型的所有数据包。 例如，如果为 FCoE 卸载和分类条件启用微型端口驱动程序指定 iSCSI TCP 端口号 （860 或 3260），该驱动程序可以使所有流出 iSCSI 数据包优先级与为分类操作定义的优先级别。

DCB 组件 (Msdcb.sys) 指定通过 OID 方法请求的流量分类[OID\_QOS\_参数](https://msdn.microsoft.com/library/windows/hardware/hh451835)。 此 OID 请求包含[ **NDIS\_QOS\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451640)结构，它指定的数组[ **NDIS\_QOS\_分类\_元素**](https://msdn.microsoft.com/library/windows/hardware/hh451631)结构。 每个这些结构定义流量分类。

DCB 组件指定*默认*流量被应用到与其他分类条件不匹配的所有传出数据包的分类。 在这种情况下，网络适配器将分配到这些流出数据包的默认分类与相关联的 IEEE 802.1p 优先级。 默认的流量分类具有以下属性：

-   它具有流量分类条件的类型 NDIS\_QOS\_条件\_默认值。

-   它是定义的数组中的第一个流量分类[ **NDIS\_QOS\_分类\_元素**](https://msdn.microsoft.com/library/windows/hardware/hh451631)结构。

有关 DCB 组件的详细信息，请参阅[NDIS QoS 体系结构的数据中心桥接](ndis-qos-architecture-for-data-center-bridging.md)。

 

 





