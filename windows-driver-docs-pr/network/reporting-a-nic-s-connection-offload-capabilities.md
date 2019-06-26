---
title: 报告 NIC 的连接卸载功能
description: 报告 NIC 的连接卸载功能
ms.assetid: a9bf798b-382c-4904-b0b2-ed1e54f9c36b
keywords:
- 连接将卸载 WDK TCP/IP 传输，报告功能
- 报告连接卸载功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f6c5d7bbeecc5473ebc5f72225075aa2405f230
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373293"
---
# <a name="reporting-a-nics-connection-offload-capabilities"></a>报告 NIC 的连接卸载功能





NDIS 微型端口驱动程序指定当前连接卸载配置中的 nic [ **NDIS\_TCP\_连接\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload)结构。 微型端口驱动程序必须包括中的当前连接卸载配置[ **NDIS\_微型端口\_适配器\_卸载\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_offload_attributes)结构。 微型端口驱动程序调用[ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)函数从[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)函数并传递中信息在 NDIS\_微型端口\_TCP\_连接\_卸载\_属性。

微型端口驱动程序必须报告更改在连接中的卸载功能。 驱动程序请求要暂停，并上载的所有连接发出的状态指示的堆栈。 (有关信息 NDIS\_状态\_卸载\_暂停，请参阅[完整 TCP 卸载](full-tcp-offload.md)。)任何配置更改完成后，驱动程序将请求重新启动并重新发出状态指示查询微型端口适配器的卸载功能的堆栈。 (有关信息 NDIS\_状态\_卸载\_恢复操作，请参阅完整 TCP 卸载。)

中的查询响应[OID\_TCP\_连接\_卸载\_当前\_配置](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-connection-offload-current-config)，NDIS 返回[ **NDIS\_TCP\_连接\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload)结构**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构。 NDIS 使用微型端口驱动程序提供的信息。

有关指定连接详细信息将卸载功能，请参阅初始化中卸载的目标[NDIS 6.0 TCP 烟囱卸载文档](full-tcp-offload.md)。

 

 





