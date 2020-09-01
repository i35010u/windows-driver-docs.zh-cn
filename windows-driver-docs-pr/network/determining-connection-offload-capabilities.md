---
title: 确定连接卸载功能
description: 确定连接卸载功能
ms.assetid: 9a7c40dd-7151-462f-b30b-0444a4177ff9
keywords:
- 连接卸载 WDK TCP/IP 传输，功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c7ff884e71e9fe634a2bb545c6656a549385fc6
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209791"
---
# <a name="determining-connection-offload-capabilities"></a>确定连接卸载功能





NDIS 支持两种类型的卸载服务： TCP/IP 卸载服务，它们是 NDIS 5.1 及更低版本的任务卸载服务和连接卸载服务的增强形式。

NDIS 为 [**ndis \_ 绑定 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters) 结构中的协议驱动程序提供卸载硬件功能和基础微型端口适配器的当前配置。 NDIS 提供任务卸载硬件功能和基础微型端口适配器的当前配置，以便在 [**NDIS \_ 筛选器 \_ 附加 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters) 结构中筛选驱动程序。

管理应用程序使用对象标识符 (OID) 查询来获取微型端口适配器的 TCP/IP 卸载功能。 但过量驱动程序应避免使用 OID 查询。 协议驱动程序必须处理基础驱动程序报告的 TCP/IP 卸载功能中的更改。 微型端口驱动程序可以报告状态指示中任务卸载功能的更改。 有关状态指示的列表，请参阅 [NDIS Tcp/ip 卸载状态指示](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-tcp-ip-offload-status-indications)。

 (或过量驱动程序) 的管理应用程序可以通过查询 [OID \_ TCP \_ 连接 \_ 卸载 \_ 当前的 \_ 配置](./oid-tcp-connection-offload-current-config.md) OID 来确定 NIC 的当前连接卸载配置。 与 OID tcp 连接卸载 "当前配置" 关联的 [**NDIS \_ tcp \_ 连接 \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload) 结构 \_ \_ \_ \_ \_ 指定微型端口适配器的当前连接卸载配置。

 

