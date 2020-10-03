---
title: 确定任务卸载功能
description: 确定任务卸载功能
ms.assetid: 9348a595-7bc0-467e-aeaf-e23100c99524
keywords:
- 任务卸载 WDK TCP/IP 传输，功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50f4892a0d3413c25c9b9bb8d965de4829851e50
ms.sourcegitcommit: e2de6b9ffb5c7356deb864f9da879533f49b25bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/03/2020
ms.locfileid: "91702608"
---
# <a name="determining-task-offload-capabilities"></a>确定任务卸载功能





NDIS 支持作为 NDIS 5.1 及更早任务卸载服务的增强形式的任务卸载服务。 有关如何确定连接卸载功能的详细信息，请参阅 [确定连接卸载功能](determining-connection-offload-capabilities.md)。

NDIS 为 [**ndis \_ 绑定 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters) 结构中的协议驱动程序提供卸载硬件功能和基础微型端口适配器的当前配置。 NDIS 提供任务卸载硬件功能和基础微型端口适配器的当前配置，以便在 [**NDIS \_ 筛选器 \_ 附加 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters) 结构中筛选驱动程序。

管理应用程序使用对象标识符 (OID) 查询来获取微型端口适配器的任务卸载功能。 但过量驱动程序应避免使用 OID 查询。 协议驱动程序必须处理基础驱动程序报告的任务卸载功能中的更改。 微型端口驱动程序可以报告状态指示中任务卸载功能的更改。 有关状态指示的列表，请参阅 [NDIS 6.0 Tcp/ip 卸载状态指示](ndis-status-task-offload-current-config.md)。

 (或过量驱动程序) 的管理应用程序可以通过查询 [oid \_ TCP \_ 卸载 \_ 当前 \_ 配置](./oid-tcp-offload-current-config.md) OID 来确定网络接口卡的当前任务卸载配置 (NIC) 。

与[OID \_ TCP \_ 卸载 \_ 当前 \_ 配置](./oid-tcp-offload-current-config.md)关联的[**NDIS \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)结构指定以下各项：

-   标头信息，包括 TCP/IP 传输支持的任务卸载版本。

-   [**NDIS \_ TCP \_ IP \_ 校验和 \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload)结构中的校验和卸载信息。

-   大型发送卸载版本 1 (LSOV1) 信息，在 [**NDIS \_ TCP \_ 大规模 \_ 发送 \_ 卸载 \_ V1**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_large_send_offload_v1) 结构中。

-   Internet 协议安全 (IPsec) 信息，在 [**NDIS \_ IPsec \_ 卸载 \_ V1**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v1) 结构中。

-   大型发送卸载版本 2 (LSOV2) 信息，在 [**NDIS \_ TCP \_ 大规模 \_ 发送 \_ 卸载 \_ V2**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_large_send_offload_v2) 结构中。

-   Internet 协议安全 ([**IPsecvOV 的) \_ \_ \_ **](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v2) 信息。

以下主题包含每种类型的卸载服务的特定信息：

-   [报告 NIC 的校验和功能](reporting-a-nic-s-checksum-capabilities.md)
-   [报告 NIC 的 LSOV1 TCP 数据包分段功能](reporting-a-nic-s-lsov1-tcp-packet-segmentation-capabilities.md)
-   [报告 NIC 的 LSOV2 TCP 数据包分段功能](reporting-a-nic-s-lsov2-tcp-packet-segmentation-capabilities.md)
-   [报告 NIC 的 IPsec 功能](reporting-a-nic-s-ipsec-capabilities.md)
    - \[IPsec 任务卸载功能已弃用，不应使用。\]

 

