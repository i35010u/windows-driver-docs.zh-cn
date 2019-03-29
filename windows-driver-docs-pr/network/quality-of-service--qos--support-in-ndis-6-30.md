---
title: NDIS 6.30 中的服务质量 (QoS) 支持
description: NDIS 6.30 中的服务质量 (QoS) 支持
ms.assetid: B425C05C-0F65-4F94-AECD-0BAD35DA441F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5411b0ee5d87e8b6575023e04d2cc8995bc1478e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568237"
---
# <a name="quality-of-service-qos-support-in-ndis-630"></a>NDIS 6.30 中的服务质量 (QoS) 支持


NDIS 6.30 和更高版本的服务质量 (QoS) 提供支持。 微型端口驱动程序使用 NDIS QoS 通信优先级的传输，或*出口*，通过使用 IEEE 802.1 数据中心桥接 (DCB) 兼容的网络适配器的数据包。

IEEE 802.1 数据中心桥接 (DCB) 是一系列的标准，用于定义统一的 802.3 以太网媒体接口或为本地局域网 (LAN) 和存储区域网络 (SAN) 技术的结构。 DCB 扩展当前 802.1x 桥接规范，以支持通过数据中心内相同的网络构造基于 LAN 和 SAN 的应用程序共存。 DCB 还支持通过定义链接级别策略防止数据包丢失的技术，例如通过 Ethernet (FCoE) 和 iSCSI、 光纤通道。

DCB 的 NDIS QoS 支持实现微型端口驱动程序以使用指定的一组策略的流量类进行配置。 每个策略确定的网络适配器如何处理为优先传送的传出数据包。

每个流量类指定应用于传出数据包的以下策略：

<a href="" id="priority-level-and-flow-control"></a>优先级别和流控制  
此策略定义的传出流量的 IEEE 802.1p 优先级级别和可选的流控制算法。

<a href="" id="traffic-selection-algorithms--tsas-"></a>流量选择算法 (TSAs)  
此策略指定如何将网络适配器选择从其传输队列交付的出口流量。 例如，适配器可以选择基于 IEEE 802.1p 优先级或分配给每个流量类的出口带宽的百分比的传出数据包。

有关 DCB 的 NDIS QoS 支持的详细信息，请参阅[的数据中心桥接的 NDIS QoS](ndis-qos-for-data-center-bridging.md)。

 

 





