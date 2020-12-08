---
title: 使用 IPsec 卸载版本 2 发送网络数据
description: 使用 IPsec 卸载版本 2 发送网络数据
keywords:
- IPsecOV2 WDK TCP/IP 传输，发送数据
- 发送数据 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: addee3b221d361304705f9f8ae66b19a8197aa0d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815871"
---
# <a name="sending-network-data-with-ipsec-offload-version-2"></a>使用 IPsec 卸载版本 2 发送网络数据

\[IPsec 任务卸载功能已弃用，不应使用。\]




TCP/IP 传输提供 IPsec 卸载版本 2 (IPsecOV2，其中包含 [OID \_ TCP \_ 任务 \_ ipsec \_ 卸载 \_ V2 \_ 添加 \_ SA](./oid-tcp-task-ipsec-offload-v2-add-sa.md) OID 的一个或多个 SAs 的) 信息。 在微型端口驱动程序为 OID \_ TCP \_ 任务 \_ IPSEC \_ 卸载 V2 添加 SA 返回成功结果之前 \_ \_ \_ ，微型端口驱动程序将初始化卸载句柄。 TCP/IP 传输请求微型端口驱动程序通过在 [**ndis \_ ipsec \_ 卸载 \_ v2 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_net_buffer_list_info)中指定 IPsecOV2 信息，并通过 [**ndis \_ ipsec \_ 卸载 \_ v2 \_ 标头 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_header_net_buffer_list_info)结构（这是 **网络 \_ 缓冲区 \_ 列表** 带外 (OOB) 信息中的一部分）来卸载 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构的处理。

TCP/IP 传输在 [**NDIS \_ IPSEC \_ 卸载 \_ V2 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_net_buffer_list_info)的 **OffloadHandle** 成员中提供了一个卸载句柄，该句柄指定了与发送数据包) 部分传输 (端到端连接 (SA) 的出站安全关联的句柄。

TCP/IP 传输在 [**NDIS \_ IPSEC \_ 卸载 \_ V2 \_ 标头 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_header_net_buffer_list_info) 结构中提供以下标头信息：

-   AH 标头和/或 ESP 标头的标头偏移量。

-   下一个协议值 (与 ESP 尾端) 中包含的相同。

-   用于组合大规模发送卸载 (LSO) 和 IPsec 卸载的填充长度。

此外，如果发送数据包将通过隧道传输，则 TCP/IP 传输提供 [**NDIS \_ IPSEC \_ 卸载 \_ V2 \_ 隧道 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_tunnel_net_buffer_list_info) 结构。 此结构指定发送数据包的隧道部分的出站 SA 的卸载句柄。 有关访问 OOB 信息的详细信息，请参阅 [ \_ \_ IPsec 卸载版本2中的访问网络缓冲区列表信息](accessing-net-buffer-list-information-in-ipsec-offload-version-2.md)。

微型端口驱动程序提供了卸载句柄，以响应 [oid \_ TCP \_ 任务 \_ IPSEC \_ 卸载 \_ V2 \_ 添加 \_ SA](./oid-tcp-task-ipsec-offload-v2-add-sa.md)的 oid 设置请求。 有关 SAs 的详细信息，请参阅 [在 IPsec 卸载版本2中管理安全关联](managing-security-associations-in-ipsec-offload-version-2.md)。

当微型端口驱动程序在 [*MiniportSendNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists) 函数中处理发送请求时，微型端口驱动程序：

-   验证是否已将硬件配置为处理 IPsec 卸载服务。 如果未将硬件配置为处理 IPsec 卸载服务，微型端口驱动程序应处理发送请求，而不提供卸载服务。

-   验证 [**ndis \_ ipsec \_ 卸载 \_ v2 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_net_buffer_list_info) 中的句柄和 [**ndis \_ ipsec \_ 卸载 \_ v2 \_ 隧道 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_tunnel_net_buffer_list_info) 结构，以确定是否需要 IPSEC 加密处理。 如果卸载句柄值为零，则表示不应为 [**NET \_ BUFFER \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)执行 IPsec 任务卸载。 如果微型端口驱动程序找不到与指定的卸载句柄相对应的已卸载 SA，则发送数据包应该会失败，并出现 **NDIS \_ 状态 \_ 失败** 值。

-   验证 [**NDIS \_ TCP \_ 大规模 \_ 发送 \_ 卸载 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info) 结构中的句柄，以确定是否应为 [**NET \_ BUFFER \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)执行分段卸载。

-   完成 [**NET \_ BUFFER \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)中所有发送数据包的所需 AH 和 ESP 处理。 当 NIC 对发送数据包执行 IPsec 处理时，将对数据包数据执行加密操作。 TCP/IP 传输已将数据包括起来，并在必要时对其进行填充 (如有必要) ，并为其分配一个 (SPI) 的序列号和安全参数索引。 对于合并的 LSO 和 IPsec 卸载， [**NET \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer) 可能会有填充，在 NIC 将大数据包分段时，将丢弃这些填充。 填充量是在 [**NDIS \_ IPSEC \_ 卸载 \_ V2 \_ 标头 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_header_net_buffer_list_info)结构的 **PadLength** 成员中指定的。 分段数据包可能需要填充以支持 IPsec 操作。

当协议驱动程序传输同时请求 LSO 和 IPsecOV2 的数据包时，它将不会成为 ESP 尾端的帧。 这是因为 ESP 尾端中的信息（例如填充长度）对于 NIC 生成的最后一段将不准确。

 

