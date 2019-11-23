---
title: 查询 NDIS QoS 参数
description: 查询 NDIS QoS 参数
ms.assetid: 875D39BA-D70D-4450-9F64-D08EAB54BDC2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 769406c8a8a83e80baf334ddd41c51d0397b2f35
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844892"
---
# <a name="querying-ndis-qos-parameters"></a>查询 NDIS QoS 参数


使用过量协议和筛选器驱动程序，可以通过以下方式查询网络适配器的 NDIS 服务质量（QoS）参数：

-   过量驱动程序可以通过[OID\_qos\_操作\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-operational-parameters)的对象标识符（oid）查询请求来查询操作 NDIS QoS 参数。

-   过量驱动程序可以通过 oid [\_qos 查询请求\_远程\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-remote-parameters)来查询远程 NDIS QoS 参数。

**请注意**  过量驱动程序无法查询本地 NDIS QoS 参数。

 

有关本地、远程和操作 NDIS QoS 参数的详细信息，请参阅 " [Ndis Qos 参数概述](overview-of-ndis-qos-parameters.md)"。

NDIS 处理微型端口驱动程序的这些 OID 请求，并返回[**NDIS\_qos\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构内请求的 QoS 参数。 NDIS 按以下方式处理这些 OID 请求：

-   当 NDIS 处理[\_QOS\_operation\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-operational-parameters)的 OID 的 oid 查询请求时，它将返回它已从上一个 NDIS 缓存的操作 NDIS QOS 参数[ **\_状态\_QOS\_操作\_参数\_更改**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)了微型端口驱动程序发出的状态指示。 当驱动程序的操作 QoS 参数首次解析或稍后更改时，驱动程序会发出此状态指示。

    如果过量驱动程序在微型[ **\_状态\_QOS\_运行\_参数**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)之前发出 OID 查询请求，\_更改状态指示，ndis 将返回[**NDIS\_QOS\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构，其中所有成员（**标头**成员除外）均设置为零。

    **请注意**，如果微型端口驱动程序发出[**ndis\_状态\_QOS\_操作\_参数\_更改**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)状态指示（其成员（**标头**成员除外））设置为零[ **，则  ** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters) ndis 还会返回此结构。\_\_

     

-   当 NDIS\_QOS 处理 Oid 的 OID 查询请求时[\_远程\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-remote-parameters)时，它将返回它已从以前的 NDIS 缓存的远程 ndis QOS 参数[ **\_状态\_QOS\_远程\_参数\_更改**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-remote-parameters-change)了微型端口驱动程序发出的状态指示。 当驱动程序的远程 QoS 参数首次解析或稍后更改时，驱动程序会发出此状态指示。

    如果过量驱动程序在微型[ **\_状态\_QOS\_远程\_参数**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-remote-parameters-change)之后发出 OID 查询请求，\_更改状态指示，ndis 将返回[**NDIS\_qos\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构，其中所有成员（**标头**成员除外）均设置为零。

    **请注意**，如果微型端口驱动程序发出[**ndis\_状态\_QOS\_操作\_参数\_更改**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)状态指示（其成员（**标头**成员除外））设置为零[ **，则  ** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters) ndis 还会返回此结构。\_\_

     

 

 





