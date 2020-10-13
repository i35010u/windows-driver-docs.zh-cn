---
title: 解析 NDIS QoS 操作参数
description: 解析 NDIS QoS 操作参数
ms.assetid: F6C486B4-ABD5-413A-9E2D-283D83802C2B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b226adcdd2d1a292219ab13b031feb4d48091f0
ms.sourcegitcommit: db9d058a9e592d4c47c67fc14f04f0ddc3aa92af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/13/2020
ms.locfileid: "91989849"
---
# <a name="resolving-operational-ndis-qos-parameters"></a>解析 NDIS QoS 操作参数


操作 NDIS 服务质量 (QoS) 参数是小型端口驱动程序用于通过数据链路连接到远程对等方的流量优先级的参数。 微型端口驱动程序从以下其中一项派生或 *解析*其操作的 NDIS QoS 参数：

-   在小型端口驱动程序上本地管理的本地 NDIS QoS 参数。 有关微型端口驱动程序如何获取其本地 QoS 参数的详细信息，请参阅 [设置本地 NDIS Qos 参数](setting-local-ndis-qos-parameters.md)。

-   小型端口驱动程序从远程对等节点上的数据链接接收的远程 NDIS QoS 参数。 有关微型端口驱动程序如何获取其远程 QoS 参数的详细信息，请参阅 [接收远程 NDIS Qos 参数](receiving-remote-ndis-qos-parameters.md)。

本地、远程和操作 NDIS QoS 参数由以下类型的数据组成：

-   优先级别和流控制设置。 这些设置定义 IEEE 802.1 p 优先级以及用于传输或 *传出*流量的可选流控制算法。

    有关详细信息，请参阅 [优先级别和流控制](ieee-802-1p-priority-levels.md)。

-   流量选择算法 (TSA) 设置。 这些设置定义网络适配器如何从其传输队列中选择传出流量。

    例如，适配器可以使用 strict 优先级的 TSA，并选择仅基于 IEEE 802.1 p 优先级的传出数据包。 适配器还可以使用增强的传输选择 (ETS) TSA，它们会根据流量分配来 moderates 流量类之间的传出流量。

    有关详细信息，请参阅 [传输选择算法 (TSAs) ](transmission-selection-algorithms--tsas-.md)。

-   指定为包含与分类条件匹配的数据（如 EtherType 或目标 TCP 端口）的数据包指定 IEEE 802.1 p 优先级别分配的流量分类。 有关详细信息，请参阅 [NDIS QoS 流量分类](ndis-qos-traffic-classifications.md)。

    **注意**   流量分类也称为 IEEE 802.1 规范中的 "应用程序优先级"。

     

微型端口驱动程序通过遵循以下准则，解析其本地或远程 NDIS QoS 参数的操作设置：

-   如果已启用 "本地数据中心桥接 Exchange (DCBX) " 已启用 "，则微型端口驱动程序必须从其远程 QoS 参数解析其操作 QoS 参数。

    有关微型端口驱动程序如何处理远程 NDIS QoS 参数的详细信息，请参阅 [接收远程 Ndis Qos 参数](receiving-remote-ndis-qos-parameters.md)。

-   如果已禁用本地 DCBX，则微型端口驱动程序必须从其本地 QoS 参数解析其操作 QoS 参数。

    有关微型端口驱动程序如何处理本地 NDIS QoS 参数的详细信息，请参阅 [设置本地 Ndis Qos 参数](setting-local-ndis-qos-parameters.md)。

-   微型端口驱动程序还可以根据独立硬件供应商 (IHV) 定义的任何专有 QoS 设置来解析其操作 QoS 参数。 对于不是由对等方进行远程配置或由操作系统本地配置的 QoS 参数，驱动程序只能执行此操作。

-   小型端口驱动程序必须在其操作 QoS 参数首次解析或稍后更改时发出 NDIS 状态指示。 例如，驱动程序可能会更改其操作 NDIS QoS 参数，因为它从其远程对等机接收了一组不同的 QoS 参数。 有关如何生成此状态指示的详细信息，请参阅 [指示对操作 NDIS QoS 参数的更改](indicating-changes-to-the-operational-ndis-qos-parameters.md)。

有关本地 DCBX 适用状态的详细信息，请参阅 [管理本地 DCBX 适用的状态](managing-the-local-dcbx-willing-state.md)。

有关用于解析 QoS 操作参数的方法的详细信息，请参阅 IEEE 802.1 Qaz 草案标准。

 

 





