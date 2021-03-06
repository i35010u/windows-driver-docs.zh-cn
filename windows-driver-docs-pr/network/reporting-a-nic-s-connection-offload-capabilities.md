---
title: 报告 NIC 的连接卸载功能
description: 报告 NIC 的连接卸载功能
keywords:
- 连接卸载 WDK TCP/IP 传输，报告功能
- 报告连接卸载功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1980fe33f3acdf95b67fa4f54e843424e128fcfe
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248383"
---
# <a name="reporting-a-nics-connection-offload-capabilities"></a>报告 NIC 的连接卸载功能





NDIS 微型端口驱动程序在 [**ndis \_ TCP \_ 连接 \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload) 结构中指定 NIC 的当前连接卸载配置。 微型端口驱动程序必须在 [**NDIS \_ 微型端口 \_ 适配器 \_ 卸载 \_ 特性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_offload_attributes) 结构中包含当前的连接卸载配置。 微型端口驱动程序从 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数调用 [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)函数，并传入 NDIS \_ 微型端口 \_ TCP \_ 连接 \_ 卸载 \_ 特性中的信息。

微型端口驱动程序必须报告连接卸载功能的更改。 驱动程序请求堆栈暂停，并通过发出状态指示来上载所有连接。  (有关 NDIS \_ 状态 \_ 卸载暂停的信息 \_ ，请参阅 [完整的 TCP 卸载](full-tcp-offload.md)。在任何配置更改完成后 ) ，驱动程序会请求堆栈通过发出状态指示来重新启动并重新查询微型端口适配器的卸载功能。  (有关 NDIS \_ 状态 \_ 卸载恢复的信息 \_ ，请参阅完整的 TCP 卸载。 ) 

为了响应 [OID \_ tcp \_ 连接 \_ 卸载的 \_ 当前 \_ 配置](./oid-tcp-connection-offload-current-config.md)，Ndis 返回 ndis [**\_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员中的 [**ndis \_ TCP \_ 连接 \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload)结构。 NDIS 使用微型端口驱动程序提供的信息。

有关指定连接卸载功能的详细信息，请参阅 [NDIS 6.0 TCP 烟囱卸载文档](full-tcp-offload.md)中的初始化卸载目标。

 

