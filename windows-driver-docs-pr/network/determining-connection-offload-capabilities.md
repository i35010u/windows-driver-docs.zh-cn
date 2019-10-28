---
title: 确定连接卸载功能
description: 确定连接卸载功能
ms.assetid: 9a7c40dd-7151-462f-b30b-0444a4177ff9
keywords:
- 连接卸载 WDK TCP/IP 传输，功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05c2dec3eb0bf58f82a85be6bc0c24f430850f61
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838150"
---
# <a name="determining-connection-offload-capabilities"></a>确定连接卸载功能





NDIS 支持两种类型的卸载服务： TCP/IP 卸载服务，它们是 NDIS 5.1 及更低版本的任务卸载服务和连接卸载服务的增强形式。

NDIS 向[**ndis\_绑定\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)结构中的协议驱动程序提供卸载硬件功能和基础微型端口适配器的当前配置。 NDIS 提供基本微型端口适配器的任务卸载硬件功能和当前配置，以筛选 NDIS\_筛选器中的驱动程序[ **\_附加\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)结构。

管理应用程序使用对象标识符（OID）查询来获取微型端口适配器的 TCP/IP 卸载功能。 但过量驱动程序应避免使用 OID 查询。 协议驱动程序必须处理基础驱动程序报告的 TCP/IP 卸载功能中的更改。 微型端口驱动程序可以报告状态指示中任务卸载功能的更改。 有关状态指示的列表，请参阅[NDIS Tcp/ip 卸载状态指示](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-tcp-ip-offload-status-indications)。

管理应用程序（或过量驱动程序）可通过查询 Oid\_TCP\_连接来确定 NIC 的当前连接卸载配置， [\_卸载\_当前\_配置](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-connection-offload-current-config)OID。 [**NDIS\_tcp\_连接\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload)与 OID 关联的卸载结构\_TCP\_\_当前\_配置指定微型端口适配器的当前连接卸载配置。

 

 





