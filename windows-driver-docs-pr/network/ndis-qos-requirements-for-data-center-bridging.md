---
title: 数据中心桥接的 NDIS QoS 要求
description: 数据中心桥接的 NDIS QoS 要求
ms.assetid: 09BEFF6C-6887-42BA-A44B-5BFE65DBD69E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fbc3341bee2c04bd85b4747cd8b20b87fcc8579
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213909"
---
# <a name="ndis-qos-requirements-for-data-center-bridging"></a>数据中心桥接的 NDIS QoS 要求


若要支持 (QoS) IEEE 802.1 数据中心桥接 (DCB) ，微型端口驱动程序和网络适配器必须支持以下各项：

-   小型端口驱动程序和网络适配器必须支持基于优先级的流控制 (PFC) 由 IEEE 802.1 Q b b 草案标准指定。

-   小型端口驱动程序和网络适配器必须支持 ETS) 算法的增强的传输选择， (由 IEEE 802.1 Qaz 草案标准指定。

-   微型端口驱动程序和网络适配器必须支持至少三个 NDIS QoS 通信类，并且必须支持至少两个基于 ETS 的通信类。 对于这两个，至少一个基于 ETS 的通信类必须支持 PFC。

    有关流量类的详细信息，请参阅 [NDIS QoS 流量类](ndis-qos-traffic-classes.md)。

-   小型端口驱动程序和网络适配器必须支持 IEEE 802.1 Q-2005 标准指定的传输选择的严格优先级算法。

对于 NDIS QoS，微型端口驱动程序和网络适配器可以根据 IEEE 802.1 Qaz 草案标准的指定，支持数据中心桥接 Exchange (DCBX) 协议。 为支持 DCBX，微型端口驱动程序和适配器还必须支持 802.1 2005 标准中指定的链接层发现协议 (LLDP) 协议。

此外，对于 NDIS QoS，微型端口驱动程序本身必须支持以下各项：

-   微型端口驱动程序必须支持 NDIS 6.30 或更高版本的 NDIS。

-   微型端口驱动程序必须支持 [oid \_ qos \_ 参数](./oid-qos-parameters.md) (oid) 方法请求的对象标识符才能设置 NDIS qos 参数。 有关详细信息，请参阅 [设置本地 NDIS QoS 参数](setting-local-ndis-qos-parameters.md)。

    **注意**   NDIS 处理微型端口驱动程序的大多数 NDIS QoS OID 请求（ [OID \_ qos \_ 参数](./oid-qos-parameters.md)除外）。

     

-   微型端口驱动程序必须能够解决在从远程对等方发送的 DCBX 帧上收到的冲突的 NDIS QoS 参数设置。 驱动程序解决其本地和远程 NDIS QoS 参数之间的冲突，以确定网络适配器用于确定优先级的数据包传输的操作 NDIS QoS 参数。 有关此过程的详细信息，请参阅 [解析操作 NDIS QoS 参数](resolving-operational-ndis-qos-parameters.md)。

-   微型端口驱动程序必须能够在其操作 NDIS QoS 参数发生更改时发出 NDIS 状态指示。 有关此过程的详细信息，请参阅 [指示对操作 NDIS QoS 参数的更改](indicating-changes-to-the-operational-ndis-qos-parameters.md)。

-   当微型端口驱动程序检测到远程对等方上的 NDIS QoS 参数发生变化时，它必须能够发出 NDIS 状态指示。 有关此过程的详细信息，请参阅 [指示对远程 NDIS QoS 参数所做的更改](indicating-changes-to-the-remote-ndis-qos-parameters.md)。

 

