---
title: NDIS 6.30 中的服务质量 (QoS) 支持
description: NDIS 6.30 中的服务质量 (QoS) 支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2895dcf4c3fb9b0b18ab48d85c84c8fa9b957e4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821229"
---
# <a name="quality-of-service-qos-support-in-ndis-630"></a>NDIS 6.30 中的服务质量 (QoS) 支持


NDIS 6.30 和更高版本为服务质量 (QoS) 提供支持。 小型端口驱动程序使用 NDIS QoS 实现流量优先级，通过网络适配器传输或 *传出* 数据包，该网络适配器符合 IEEE 802.1 数据中心桥接 (DCB) 。

IEEE 802.1 数据中心桥接 (DCB) 是一系列标准，用于定义适用于局域网 (LAN) 和存储区域网络 (SAN) 技术的统一802.3 以太网媒体接口或构造。 DCB 扩展了当前802.1 桥接规范，以支持在数据中心内的同一网络结构上共存基于 LAN 和 SAN 的应用程序。 通过定义阻止数据包丢失的链接级别策略，DCB 还支持通过以太网 (FCoE) 和 iSCSI 光纤通道的技术。

通过 NDIS QoS 对 DCB 的支持，可以使用指定一组策略的流量类配置微型端口驱动程序。 每个策略确定网络适配器如何处理传出数据包以确定优先级。

每个交通类指定适用于出口数据包的下列策略：

<a href="" id="priority-level-and-flow-control"></a>优先级别和流控制  
此策略定义 IEEE 802.1 p 优先级级别和出口流量的可选流控制算法。

<a href="" id="traffic-selection-algorithms--tsas-"></a>流量选择算法 (TSAs)   
此策略指定网络适配器如何从其传输队列中选择要传送的传出流量。 例如，适配器可以选择基于 IEEE 802.1 p 优先级的传出数据包或分配给每个通信类的出口带宽的百分比。

有关 NDIS QoS 对 DCB 的支持的详细信息，请参阅 [用于数据中心桥接的 Ndis qos](ndis-qos-for-data-center-bridging.md)。

 

 





