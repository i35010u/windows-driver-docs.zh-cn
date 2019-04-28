---
title: 解析 NDIS QoS 操作参数
description: 解析 NDIS QoS 操作参数
ms.assetid: F6C486B4-ABD5-413A-9E2D-283D83802C2B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 103d6b3425deaad36e9428ce5c55276acdf8db70
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341361"
---
# <a name="resolving-operational-ndis-qos-parameters"></a>解析 NDIS QoS 操作参数


操作 NDIS 服务质量 (QoS) 参数是那些微型端口驱动程序使用通过数据链路连接到远程对等通信优先级。 派生而来的微型端口驱动程序，或*解析*，其操作的 NDIS QoS 参数从以下项之一：

-   微型端口驱动程序本地管理本地 NDIS QoS 参数。 微型端口驱动程序如何获取其本地 QoS 参数的详细信息，请参阅[设置本地 NDIS QoS 参数](setting-local-ndis-qos-parameters.md)。

-   微型端口驱动程序收到的数据链接上的远程对等远程 NDIS QoS 参数。 微型端口驱动程序如何获取其远程 QoS 参数的详细信息，请参阅[接收远程 NDIS QoS 参数](receiving-remote-ndis-qos-parameters.md)。

本地、 远程和操作的 NDIS QoS 参数包含以下类型的数据：

-   优先级别和流控制设置。 这些设置用于定义传输，IEEE 802.1p 优先级级别和可选的流控制算法或*出口*，流量。

    有关详细信息，请参阅[优先级别和流控制](priority-levels-and-flow-control.md)。

-   流量选择算法 (TSA) 设置。 这些设置定义的网络适配器如何从其传输队列选择传出流量。

    例如，适配器可以使用严格的优先级 TSA 并选择仅根据 IEEE 802.1p 优先级的流出数据包。 适配器也可以使用增强传输选择 (ETS) TSA 减少基于其带宽分配的流量类之间的传出流量。

    有关详细信息，请参阅[传输选择算法 (TSAs)](transmission-selection-algorithms--tsas-.md)。

-   指定对包含数据相匹配的分类条件，如 EtherType 或目标的 TCP 端口的数据包的 IEEE 802.1p 优先级级别的分配的流量分类。 有关详细信息，请参阅[NDIS QoS 流量分类](ndis-qos-traffic-classifications.md)。

    **请注意**  流量分类也被称为"应用程序优先级"IEEE 802.1 规范中的。

     

微型端口驱动程序通过遵循以下准则来解析其本地或远程 NDIS QoS 参数从其运行设置：

-   如果启用了本地数据中心桥接交换 (DCBX) 愿意状态，微型端口驱动程序必须解析其操作的 QoS 参数从其远程 QoS 参数。

    有关微型端口驱动程序如何处理远程 NDIS QoS 参数的详细信息，请参阅[接收远程 NDIS QoS 参数](receiving-remote-ndis-qos-parameters.md)。

-   如果禁用了本地 DCBX 愿意状态，微型端口驱动程序必须解析其操作的 QoS 参数从其本地 QoS 参数。

    有关微型端口驱动程序如何处理本地 NDIS QoS 参数的详细信息，请参阅[设置本地 NDIS QoS 参数](setting-local-ndis-qos-parameters.md)。

-   微型端口驱动程序也可以解决基于由独立硬件供应商 (IHV) 定义的任何专有 QoS 设置其操作的 QoS 参数。 该驱动程序可以仅执行此操作未配置远程对等方或本地操作系统的 QoS 参数。

-   其操作的 QoS 参数或者解决第一次或更高版本更改时，微型端口驱动程序必须发出 NDIS 状态指示。 例如，驱动程序可能会更改其操作的 NDIS QoS 参数，因为它从其远程对等方接收到一组不同的 QoS 参数。 有关如何生成此状态指示的详细信息，请参阅[对操作的 NDIS QoS 参数，该值指示更改](indicating-changes-to-the-operational-ndis-qos-parameters.md)。

有关本地 DCBX 愿意状态，请参阅[管理本地 DCBX 愿意状态](managing-the-local-dcbx-willing-state.md)。

有关用于解析 QoS 操作参数的方法的详细信息，请参阅 IEEE 802.1Qaz 草案标准。

 

 





