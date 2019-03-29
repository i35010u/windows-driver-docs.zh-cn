---
title: 数据中心桥接的 NDIS QoS 要求
description: 数据中心桥接的 NDIS QoS 要求
ms.assetid: 09BEFF6C-6887-42BA-A44B-5BFE65DBD69E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8e047c07af150224b55d168418001b1da0ed915
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575461"
---
# <a name="ndis-qos-requirements-for-data-center-bridging"></a>数据中心桥接的 NDIS QoS 要求


若要支持 NDIS 服务质量 (QoS) 的 IEEE 802.1 数据中心桥接 (DCB)，微型端口驱动程序和网络适配器必须支持以下功能：

-   微型端口驱动程序和网络适配器必须支持基于优先级的流控制 (PFC) 指定的 IEEE 802.1Qbb 草案标准。

-   微型端口驱动程序和网络适配器必须支持指定的 IEEE 802.1Qaz 增强传输选择 (ETS) 算法草案标准。

-   微型端口驱动程序和网络适配器必须支持至少三个 NDIS QoS 通信类别，并且必须支持至少两个 ETS 基于流量类。 这两个至少一个基于 ETS 的流量类必须支持 PFC。

    有关流量类的详细信息，请参阅[NDIS QoS 通信类](ndis-qos-traffic-classes.md)。

-   微型端口驱动程序和网络适配器必须支持严格的优先级算法为传输所选内容按照 IEEE 802.1Q-2005 标准。

有关 NDIS QoS、 微型端口驱动程序和网络适配器可以选择性地支持 IEEE 由指定的数据中心桥接交换 (DCBX) 协议 802.1Qaz 草案标准。 若要支持 DCBX，微型端口驱动程序和适配器还必须支持 IEEE 802.1AB 中指定的链接层发现协议 (LLDP) 协议的 2005 标准。

此外，微型端口驱动程序本身必须为 NDIS QoS 支持以下：

-   微型端口驱动程序必须支持 NDIS 6.30 或更高版本的 NDIS。

-   微型端口驱动程序必须支持的对象标识符 (OID) 的方法请求[OID\_QOS\_参数](https://msdn.microsoft.com/library/windows/hardware/hh451835)设置 NDIS QoS 参数。 有关详细信息，请参阅[设置本地 NDIS QoS 参数](setting-local-ndis-qos-parameters.md)。

    **请注意**  NDIS 处理大部分除微型端口驱动程序的 NDIS QoS OID 请求[OID\_QOS\_参数](https://msdn.microsoft.com/library/windows/hardware/hh451835)。

     

-   微型端口驱动程序必须能够解析冲突从远程对等方发送的 DCBX 帧上接收到的 NDIS QoS 参数设置。 该驱动程序解析其本地和远程 NDIS QoS 参数，以确定网络适配器将使用按优先顺序排列的数据包传输其操作的 NDIS QoS 参数之间的冲突。 有关此过程的详细信息，请参阅[解析操作的 NDIS QoS 参数](resolving-operational-ndis-qos-parameters.md)。

-   微型端口驱动程序必须能够发出 NDIS 状态指示其操作的 NDIS QoS 参数更改时。 有关此过程的详细信息，请参阅[对操作的 NDIS QoS 参数，该值指示更改](indicating-changes-to-the-operational-ndis-qos-parameters.md)。

-   微型端口驱动程序必须能够在远程对等方上的 NDIS QoS 参数中检测到更改时发出 NDIS 状态指示。 有关此过程的详细信息，请参阅[对远程 NDIS QoS 参数，该值指示更改](indicating-changes-to-the-remote-ndis-qos-parameters.md)。

 

 





