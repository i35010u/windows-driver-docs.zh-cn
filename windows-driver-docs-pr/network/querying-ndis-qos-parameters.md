---
title: 查询 NDIS QoS 参数
description: 查询 NDIS QoS 参数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a380c394b4786c773e4145cd9933d79548927c61
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793382"
---
# <a name="querying-ndis-qos-parameters"></a>查询 NDIS QoS 参数


使用过量协议和筛选器驱动程序，可以通过以下方式查询网络适配器 (QoS) 参数的 NDIS 质量：

-   过量驱动程序可以通过对象标识符查询操作 NDIS QoS 参数， (oid) 查询 [oid \_ qos \_ 操作 \_ 参数](./oid-qos-operational-parameters.md)的请求。

-   过量驱动程序可以通过 oid [ \_ qos \_ 远程 \_ 参数](./oid-qos-remote-parameters.md)的 oid 查询请求来查询远程 NDIS QoS 参数。

**注意**  过量驱动程序无法查询本地 NDIS QoS 参数。

 

有关本地、远程和操作 NDIS QoS 参数的详细信息，请参阅 " [Ndis Qos 参数概述](overview-of-ndis-qos-parameters.md)"。

NDIS 处理微型端口驱动程序的这些 OID 请求，并返回 [**NDIS \_ qos \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters) 结构内请求的 qos 参数。 NDIS 按以下方式处理这些 OID 请求：

-   当 NDIS 处理 [oid \_ QOS \_ 操作 \_ 参数](./oid-qos-operational-parameters.md)的 oid 查询请求时，它将返回其已从先前的 [**ndis \_ 状态 \_ qos \_ 操作 \_ 参数 \_**](./ndis-status-qos-operational-parameters-change.md) 缓存的操作 NDIS qos 参数更改了由微型端口驱动程序颁发的状态指示。 当驱动程序的操作 QoS 参数首次解析或稍后更改时，驱动程序会发出此状态指示。

    如果过量驱动程序在微型端口驱动程序发出 OID 查询请求之前发出 OID 查询请求，则 [**ndis \_ 状态 \_ QOS \_ 操作 \_ 参数 \_ 更改**](./ndis-status-qos-operational-parameters-change.md) 状态指示，ndis 将返回 [**NDIS \_ QOS \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters) 结构，其中所有成员都 (的 **标头** 成员除外) 设置为零。

    **注意**  如果微型端口驱动程序发出 [**ndis \_ 状态 \_ qos \_ 操作 \_ 参数 \_ 更改**](./ndis-status-qos-operational-parameters-change.md) 状态指示，而 ndis [**\_ QOS \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters) 结构的成员 (的成员与 **标头** 成员的异常) 设置为零，ndis 还会返回此结构。

     

-   当 NDIS 处理 [oid \_ QOS \_ 远程 \_ 参数](./oid-qos-remote-parameters.md)的 oid 查询请求时，它将返回从上一 [**ndis \_ 状态 \_ qos \_ 远程 \_ 参数 \_**](./ndis-status-qos-remote-parameters-change.md) 缓存的远程 NDIS qos 参数，该参数更改了微型端口驱动程序颁发的状态指示。 当驱动程序的远程 QoS 参数首次解析或稍后更改时，驱动程序会发出此状态指示。

    如果过量驱动程序在微型端口驱动程序发出 OID 查询请求之前发出 OID 查询请求，则 [**ndis \_ 状态 \_ QOS \_ 远程 \_ 参数 \_ 更改**](./ndis-status-qos-remote-parameters-change.md) 状态指示，ndis 将返回 [**NDIS \_ QOS \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters) 结构，其中所有成员都 (的 **标头** 成员除外) 设置为零。

    **注意**  如果微型端口驱动程序发出 [**ndis \_ 状态 \_ qos \_ 操作 \_ 参数 \_ 更改**](./ndis-status-qos-operational-parameters-change.md) 状态指示，而 ndis [**\_ QOS \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters) 结构的成员 (的成员与 **标头** 成员的异常) 设置为零，ndis 还会返回此结构。

     

 

