---
title: 报告 NIC 的连接卸载功能
description: 报告 NIC 的连接卸载功能
ms.assetid: a9bf798b-382c-4904-b0b2-ed1e54f9c36b
keywords:
- 连接卸载 WDK TCP/IP 传输，报告功能
- 报告连接卸载功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: afe818385736c1926b6ecc73103452f85a41bf0c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842060"
---
# <a name="reporting-a-nics-connection-offload-capabilities"></a>报告 NIC 的连接卸载功能





NDIS 微型端口驱动程序在[**ndis\_TCP\_连接\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload)结构中指定当前的连接卸载配置。 微型端口驱动程序必须在[**NDIS\_微型端口\_适配器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_offload_attributes)中包括当前连接卸载配置，\_卸载\_属性结构。 微型端口驱动程序从[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数调用[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)函数，并将 NDIS\_微型端口中的信息传入\_TCP\_连接\_卸载\_特性。

微型端口驱动程序必须报告连接卸载功能的更改。 驱动程序请求堆栈暂停，并通过发出状态指示来上载所有连接。 （有关 NDIS\_状态的信息\_卸载\_暂停，请参阅[完整的 TCP 卸载](full-tcp-offload.md)。）完成任何配置更改后，驱动程序会请求堆栈通过发出状态指示来重新启动并重新查询微型端口适配器的卸载功能。 （有关 NDIS\_状态的信息\_卸载\_恢复，请参阅完整的 TCP 卸载。）

为了响应[OID\_tcp\_连接的查询\_卸载\_当前\_配置](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-connection-offload-current-config)，Ndis 在 InformationBuffer 中返回[**ndis\_TCP\_\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload)结构 [**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的成员。 NDIS 使用微型端口驱动程序提供的信息。

有关指定连接卸载功能的详细信息，请参阅[NDIS 6.0 TCP 烟囱卸载文档](full-tcp-offload.md)中的初始化卸载目标。

 

 





