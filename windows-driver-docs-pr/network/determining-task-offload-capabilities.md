---
title: 确定任务卸载功能
description: 确定任务卸载功能
ms.assetid: 9348a595-7bc0-467e-aeaf-e23100c99524
keywords:
- 任务卸载 WDK TCP/IP 传输，功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3f30d33bb144f1790cc656f9fb0193ffea8a076
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838148"
---
# <a name="determining-task-offload-capabilities"></a>确定任务卸载功能





NDIS 支持作为 NDIS 5.1 及更早任务卸载服务的增强形式的任务卸载服务。 有关如何确定连接卸载功能的详细信息，请参阅[确定连接卸载功能](determining-connection-offload-capabilities.md)。

NDIS 向[**ndis\_绑定\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)结构中的协议驱动程序提供卸载硬件功能和基础微型端口适配器的当前配置。 NDIS 提供基本微型端口适配器的任务卸载硬件功能和当前配置，以筛选 NDIS\_筛选器中的驱动程序[ **\_附加\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)结构。

管理应用程序使用对象标识符（OID）查询来获取微型端口适配器的任务卸载功能。 但过量驱动程序应避免使用 OID 查询。 协议驱动程序必须处理基础驱动程序报告的任务卸载功能中的更改。 微型端口驱动程序可以报告状态指示中任务卸载功能的更改。 有关状态指示的列表，请参阅[NDIS 6.0 Tcp/ip 卸载状态指示](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-tcp-ip-offload-status-indications)。

管理应用程序（或过量驱动程序）可通过查询[oid\_TCP\_卸载\_当前\_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config) oid 来确定网络接口卡（NIC）的当前任务卸载配置。

与 OID 关联的[**NDIS\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)结构[\_TCP\_卸载\_当前\_配置](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config)指定以下各项：

-   标头信息，包括 TCP/IP 传输支持的任务卸载版本。

-   [**NDIS\_TCP\_IP\_校验和\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload)结构中的校验和卸载信息。

-   LSOV1\_中的大量发送卸载版本1（）信息[ **\_大型\_发送\_卸载\_V1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_large_send_offload_v1)结构。

-   NDIS\_IPSEC 中的 Internet 协议安全（IPsec）信息[ **\_卸载\_V1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v1)结构。

-   [**NDIS\_TCP\_大规模\_发送\_卸载\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_large_send_offload_v2)结构中的大量发送卸载版本2（LSOV2）信息。

-   NDIS\_IPSEC 中的 Internet 协议安全性（IPsecvOV）信息[ **\_卸载\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v2)结构。

以下主题包含每种类型的卸载服务的特定信息：

-   [报告 NIC 的校验和功能](reporting-a-nic-s-checksum-capabilities.md)
-   [报告 NIC 的 LSOV1 TCP 数据包分段功能](reporting-a-nic-s-lsov1-tcp-packet-segmentation-capabilities.md)
-   [报告 NIC 的 LSOV2 TCP 数据包分段功能](reporting-a-nic-s-lsov2-tcp-packet-segmentation-capabilities.md)
-   [报告 NIC 的 IPsec 功能](reporting-a-nic-s-ipsec-capabilities.md)
    - \[IPsec 任务卸载功能已弃用，不应使用。\]

 

 





