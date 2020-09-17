---
title: IPsec 卸载版本 2 简介
description: IPsec 卸载版本 2 简介
ms.assetid: d8fd0bf8-f7b6-44ad-a3dc-f10bb20ce651
keywords:
- IPsecOV2 WDK TCP/IP 传输，关于 IPsecOV2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7c5e2963969d7877ca046389f63260c2e771ee3
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715044"
---
# <a name="introduction-to-ipsec-offload-version-2"></a>IPsec 卸载版本 2 简介

\[IPsec 任务卸载功能已弃用，不应使用。\]




IPsec 卸载版本 2 (IPsecOV2) 扩展 IPsec 卸载版本 1 (IPsecOV1) 中提供的服务。 有关 IPsecOV1 卸载和 IPsec 的详细信息，请参阅 [Ipsec 卸载版本 1](background-reading-on-ipsec.md)。

NDIS 6.1 和更高版本的微型端口驱动程序报告将微型端口适配器的 IPsecOV2 卸载功能到 NDIS。 报告 IPsec 功能：

-   在初始化期间，微型端口驱动程序在 [**NDIS \_ 微型端口 \_ 适配器 \_ 卸载 \_ 特性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_offload_attributes) 结构中报告任务卸载默认配置以及微型端口适配器的硬件功能。

-   如果配置的功能发生更改，微型端口驱动程序将报告当前配置，并提供 [**NDIS \_ 状态 \_ 任务 " \_ 卸载 \_ 当前 \_ 配置**](./ndis-status-task-offload-current-config.md) 状态指示"。 如果 [oid \_ TCP \_ 卸载 \_ 参数](./oid-tcp-offload-parameters.md) oid 设置微型端口适配器的当前任务卸载配置，则该配置可能会更改。 此外，如果 [mux 中间驱动程序](ndis-mux-intermediate-drivers.md) 的硬件配置发生更改，则 mux 中间驱动程序必须使用 [**NDIS \_ 状态 \_ 任务 " \_ 卸载 \_ 硬件 \_ 功能**](./ndis-status-task-offload-hardware-capabilities.md) " 状态指示来报告硬件配置更改。

NDIS 在 [**ndis \_ 绑定 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters) 结构中报告微型协议驱动程序的卸载功能的默认配置。 过量协议驱动程序可以从当前配置支持的服务中选择 IPsecOV2 任务卸载服务。 [**NDIS \_ 状态任务 \_ " \_ 卸载 \_ 当前 \_ 配置**](./ndis-status-task-offload-current-config.md)状态" 指示可确保所有的过量协议驱动程序都已用新功能信息更新。

在初始化期间报告硬件功能时，微型端口驱动程序必须从注册表读取标准化关键字。 有关 IPsecOV2 卸载功能的详细信息，请参阅 [报告 NIC 的 IPsec 卸载第2版功能](reporting-a-nic-s-ipsec-offload-version-2-capabilities.md)。

**注意**   NDIS 为 NDIS 6.1 和更高版本的驱动程序提供直接 OID 请求接口。 [直接 OID 请求路径](/windows-hardware/drivers/ddi/_netvista/)支持经常查询或设置的 OID 请求。

 

IPsecOV2 提供 [OID \_ tcp \_ 任务 \_ ipsec \_ 卸载 \_ v2 \_ 添加 \_ SA](./oid-tcp-task-ipsec-offload-v2-add-sa.md)、 [oid \_ tcp \_ 任务 ipsec 卸载 \_ \_ \_ v2 \_ 更新 \_ sa](./oid-tcp-task-ipsec-offload-v2-update-sa.md)和 [oid \_ tcp \_ 任务 \_ ipsec \_ 卸载 \_ v2 \_ 删除 \_ SA](./oid-tcp-task-ipsec-offload-v2-delete-sa.md) 直接 OID 请求，以启用协议驱动程序以添加、更新和删除 (SAs) 的安全关联。 有关 SAs 的详细信息，请参阅 [在 IPsec 卸载版本2中管理安全关联](managing-security-associations-in-ipsec-offload-version-2.md)。

NIC 可以在发送和接收路径上执行 IPsec 卸载任务。 NDIS 驱动程序使用 [**ndis \_ ipsec \_ 卸载 \_ v2 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_net_buffer_list_info)， [**ndis \_ ipsec 卸载 v2 \_ \_ \_ 标头 \_ 网络 \_ 缓冲区 \_ \_ **](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_header_net_buffer_list_info)列表信息， [**ndis \_ ipsec \_ 卸载 \_ v2 \_ 隧道 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_tunnel_net_buffer_list_info) 结构，用于访问 IPSEC 带外 (OOB) 信息。

在发送路径上，过量驱动程序将句柄设置为 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构中 OOB 信息中的出站 SA 和 IPsec 标头信息，以指定 NIC 应该执行 IPsecOV2 卸载任务。

在接收路径上，卸载 SA 后，NIC 必须对所有接收到的数据包执行 IPsec 处理，这些数据包与微型端口驱动程序报告给 NDIS 的功能相匹配。 微型端口驱动程序在 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构中设置 OOB 信息中的适当标志，以指定 NIC 执行的特定卸载任务以及这些操作的结果。

有关 IPsecOV2 中的发送和接收处理的详细信息，请参阅 [通过 Ipsec 卸载版本2发送网络数据](sending-network-data-with-ipsec-offload-version-2.md) 和 [接收包含 ipsec 卸载版本2的网络数据](receiving-network-data-with-ipsec-offload-version-2.md)。

 

