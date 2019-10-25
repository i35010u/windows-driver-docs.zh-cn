---
title: IPsec 卸载版本 2 简介
description: IPsec 卸载版本 2 简介
ms.assetid: d8fd0bf8-f7b6-44ad-a3dc-f10bb20ce651
keywords:
- IPsecOV2 WDK TCP/IP 传输，关于 IPsecOV2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9565942f7a7bf983626702d4ac8982ad3c1d75e9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844174"
---
# <a name="introduction-to-ipsec-offload-version-2"></a>IPsec 卸载版本 2 简介

\[IPsec 任务卸载功能已弃用，不应使用。\]




IPsec 卸载版本2（IPsecOV2）扩展了 IPsec 卸载版本1（IPsecOV1）中提供的服务。 有关 IPsecOV1 卸载和 IPsec 的详细信息，请参阅[Ipsec 卸载版本 1](ipsec-offload-version-1.md)。

NDIS 6.1 和更高版本的微型端口驱动程序报告将微型端口适配器的 IPsecOV2 卸载功能到 NDIS。 报告 IPsec 功能：

-   在初始化期间，微型端口驱动程序会在[**NDIS\_微型端口\_适配器\_卸载\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_offload_attributes)结构中，报告任务卸载默认配置以及微型端口适配器的硬件功能。

-   如果配置的功能发生更改，微型端口驱动程序将报告具有[**NDIS\_状态\_任务的当前配置，\_卸载\_当前\_配置**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-task-offload-current-config)状态指示。 如果[oid\_TCP\_卸载\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-parameters)oid 设置微型端口适配器的当前任务卸载配置，则该配置可能会更改。 此外，如果[mux 中间驱动程序](ndis-mux-intermediate-drivers.md)的硬件配置发生更改，则 mux 中间驱动程序必须使用 NDIS\_状态报告硬件配置更改[ **\_任务\_卸载\_硬件\_功能**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-task-offload-hardware-capabilities)状态指示。

NDIS 将小型端口适配器的卸载功能的默认配置报告到[**NDIS\_绑定\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)结构中的过量协议驱动程序。 过量协议驱动程序可以从当前配置支持的服务中选择 IPsecOV2 任务卸载服务。 [**NDIS\_状态\_任务\_卸载\_当前\_配置**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-task-offload-current-config)状态指示可确保所有的过量协议驱动程序都已通过新功能信息进行更新。

在初始化期间报告硬件功能时，微型端口驱动程序必须从注册表读取标准化关键字。 有关 IPsecOV2 卸载功能的详细信息，请参阅[报告 NIC 的 IPsec 卸载第2版功能](reporting-a-nic-s-ipsec-offload-version-2-capabilities.md)。

**请注意**  NDIS 为 ndis 6.1 和更高版本的驱动程序提供直接 OID 请求接口。 [直接 OID 请求路径](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)支持经常查询或设置的 OID 请求。

 

IPsecOV2 提供[\_TCP\_任务\_IPSEC\_卸载\_v2\_\_\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-add-sa)\_\_\_[\_IPSEC\_UPDATE\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-update-sa)和[OID\_TCP\_任务\_IPSEC\_卸载\_V2\_删除\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-delete-sa)直接 OID 请求以使协议驱动程序能够添加、更新和删除安全关联（SAs）。 有关 SAs 的详细信息，请参阅[在 IPsec 卸载版本2中管理安全关联](managing-security-associations-in-ipsec-offload-version-2.md)。

NIC 可以在发送和接收路径上执行 IPsec 卸载任务。 NDIS 驱动程序使用[**ndis\_IPSEC\_卸载\_V2\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_net_buffer_list_info)， [**NDIS\_IPSEC\_卸载\_V2\_\_@no__ 网络t_16_ BUFFER\_列出\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_header_net_buffer_list_info)， [**NDIS\_IPSEC\_卸载\_V2\_隧道\_NET\_BUFFER\_列出\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_tunnel_net_buffer_list_info)结构以访问 IPSEC 带外（OOB）信息.

在发送路径上，过量驱动程序将句柄设置为[**NET\_BUFFER\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构中的 OOB 信息中的出站 SA 和 IPsec 标头信息，以指定 NIC 应该执行 IPsecOV2 卸载任务。

在接收路径上，卸载 SA 后，NIC 必须对所有接收到的数据包执行 IPsec 处理，这些数据包与微型端口驱动程序报告给 NDIS 的功能相匹配。 微型端口驱动程序在[**NET\_BUFFER\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构中设置 OOB 信息中的适当标志，以指定 NIC 执行的特定卸载任务以及这些操作的结果。

有关 IPsecOV2 中的发送和接收处理的详细信息，请参阅[通过 Ipsec 卸载版本2发送网络数据](sending-network-data-with-ipsec-offload-version-2.md)和[接收包含 ipsec 卸载版本2的网络数据](receiving-network-data-with-ipsec-offload-version-2.md)。

 

 





