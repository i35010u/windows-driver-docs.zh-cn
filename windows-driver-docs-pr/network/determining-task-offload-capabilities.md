---
title: 确定任务卸载功能
description: 确定任务卸载功能
ms.assetid: 9348a595-7bc0-467e-aeaf-e23100c99524
keywords:
- 任务卸载，WDK TCP/IP 传输，功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: edad6c3a8cdf34009d5e353534e6488506c40b2c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381411"
---
# <a name="determining-task-offload-capabilities"></a>确定任务卸载功能





NDIS 支持任务卸载的服务增强窗体的 NDIS 5.1 和前面的任务将卸载服务。 有关如何确定连接的详细信息将卸载功能，请参阅[卸载功能确定连接](determining-connection-offload-capabilities.md)。

NDIS 提供卸载硬件功能和基础微型端口适配器添加到协议中的驱动程序的当前配置[ **NDIS\_绑定\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters)结构。 NDIS 提供任务卸载硬件功能和当前配置中的筛选器驱动程序为基础的微型端口适配器[ **NDIS\_筛选器\_附加\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_filter_attach_parameters)结构。

管理应用程序使用对象标识符 (OID) 查询来获取任务的微型端口适配器卸载功能。 但是，过量驱动程序应避免使用 OID 的查询。 协议驱动程序必须处理该基础驱动程序报表中的任务卸载功能的更改。 微型端口驱动程序可以报告任务中的更改将卸载状态指示中的功能。 状态指示的列表，请参阅[NDIS 6.0 TCP/IP 卸载状态指示](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-tcp-ip-offload-status-indications)。

管理应用程序 （或基础驱动程序） 可以通过查询来确定网络接口卡 (NIC) 的当前任务卸载配置[OID\_TCP\_卸载\_当前\_配置](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config)OID。

[ **NDIS\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload)与关联的结构[OID\_TCP\_卸载\_当前\_配置](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config)指定以下项目：

-   标头信息，其中包括 TCP/IP 传输支持的任务卸载版本。

-   校验和卸载的信息，在[ **NDIS\_TCP\_IP\_校验和\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload)结构。

-   大型将卸载版本 1 (LSOV1) 发送信息，请在[ **NDIS\_TCP\_LARGE\_发送\_卸载\_V1** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_tcp_large_send_offload_v1)结构。

-   Internet 协议安全 (IPsec) 信息中[ **NDIS\_IPSEC\_卸载\_V1** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v1)结构。

-   大型将卸载版本 2 (LSOV2) 发送信息，请在[ **NDIS\_TCP\_LARGE\_发送\_卸载\_V2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_tcp_large_send_offload_v2)结构。

-   中的 Internet 协议安全 (IPsecvOV) 信息[ **NDIS\_IPSEC\_卸载\_V2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v2)结构。

以下主题包含有关每种类型的卸载服务的特定信息：

-   [报告 NIC 的校验和功能](reporting-a-nic-s-checksum-capabilities.md)
-   [报告的 NIC LSOV1 TCP 数据包分段功能](reporting-a-nic-s-lsov1-tcp-packet-segmentation-capabilities.md)
-   [报告的 NIC LSOV2 TCP 数据包分段功能](reporting-a-nic-s-lsov2-tcp-packet-segmentation-capabilities.md)
-   [报告 NIC 的 IPsec 功能](reporting-a-nic-s-ipsec-capabilities.md)
    - \[IPsec 任务卸载功能已弃用，不应使用。\]

 

 





