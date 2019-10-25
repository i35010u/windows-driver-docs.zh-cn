---
title: 使用 IPsec 卸载版本 2 发送网络数据
description: 使用 IPsec 卸载版本 2 发送网络数据
ms.assetid: d3580313-a98b-4150-b344-e3e395ce68e9
keywords:
- IPsecOV2 WDK TCP/IP 传输，发送数据
- 发送数据 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6fe7ef224f6ccc3e99b00f0a48e91cc164ed86c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841965"
---
# <a name="sending-network-data-with-ipsec-offload-version-2"></a>使用 IPsec 卸载版本 2 发送网络数据

\[IPsec 任务卸载功能已弃用，不应使用。\]




TCP/IP 传输为一个或多个 SAs\_TCP\_任务提供 IPsec 卸载版本2（IPsecOV2）信息[\_ipsec\_卸载\_V2\_添加\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-add-sa) OID。 在微型端口驱动程序返回\_TCP\_任务的成功结果\_IPSEC\_卸载\_V2\_添加\_SA 之前，微型端口驱动程序将初始化卸载句柄。 TCP/IP 传输请求微型端口驱动程序通过在 NDIS 中指定 IPsecOV2 信息，将[**网络\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)的处理卸载\_列表结构，方法是在[**NDIS\_IPSEC\_卸载\_V2\_NET\_缓冲区\_列出\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_net_buffer_list_info)和[**NDIS\_IPSEC\_卸载\_V2\_\_NET\_BUFFER\_列表\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_header_net_buffer_list_info)结构，这是网络的一部分\_**BUFFER\_列出**带外（OOB）信息。

TCP/IP 传输在 NDIS\_IPSEC\_卸载\_V2 的**OffloadHandle**成员中提供了卸载句柄[ **\_NET\_BUFFER\_LIST\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_net_buffer_list_info)发送数据包的传输（端到端连接）部分的安全关联（SA）。

TCP/IP 传输在 NDIS 中提供以下标头信息[ **\_IPSEC\_卸载\_V2\_标头\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_header_net_buffer_list_info)结构：

-   AH 标头和/或 ESP 标头的标头偏移量。

-   下一个协议值（与 ESP 尾端中包含的值相同）。

-   用于组合大规模发送卸载（LSO）和 IPsec 卸载的填充长度。

此外，如果发送数据包将通过隧道传输，则 TCP/IP 传输会提供一个[**NDIS\_IPSEC\_卸载\_V2\_隧道\_网络\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_tunnel_net_buffer_list_info)\_\_的信息结构。 此结构指定发送数据包的隧道部分的出站 SA 的卸载句柄。 有关访问 OOB 信息的详细信息，请参阅[IPsec 卸载版本2中的访问 NET\_BUFFER\_列表信息](accessing-net-buffer-list-information-in-ipsec-offload-version-2.md)。

微型端口驱动程序提供了卸载句柄，以响应 oid [\_TCP\_任务\_IPSEC\_卸载\_V2\_添加\_SA](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-task-ipsec-offload-v2-add-sa)。 有关 SAs 的详细信息，请参阅[在 IPsec 卸载版本2中管理安全关联](managing-security-associations-in-ipsec-offload-version-2.md)。

当微型端口驱动程序在[*MiniportSendNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists)函数中处理发送请求时，微型端口驱动程序：

-   验证是否已将硬件配置为处理 IPsec 卸载服务。 如果未将硬件配置为处理 IPsec 卸载服务，微型端口驱动程序应处理发送请求，而不提供卸载服务。

-   验证 NDIS 中的句柄[ **\_ipsec\_卸载\_V2\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_net_buffer_list_info) and [**NDIS\_IPSEC\_\_\_隧道\_NET\_BUFFER\_列出\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_tunnel_net_buffer_list_info)结构，以确定是否需要 IPsec 加密处理。 如果卸载句柄值为零，则表示不应为[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)中执行 IPsec 任务卸载。 如果微型端口驱动程序找不到与指定的卸载句柄相对应的已卸载 SA，则发送数据包应该会失败，并且**NDIS\_状态\_失败**值。

-   验证 NDIS 中的句柄[ **\_TCP\_大型\_发送\_卸载\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info)结构，以确定是否应为 NET 执行分段卸载[ **\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)。

-   完成[**NET\_BUFFER\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)中的所有发送数据包的所需 AH 和 ESP 处理。 当 NIC 对发送数据包执行 IPsec 处理时，将对数据包数据执行加密操作。 TCP/IP 传输已经将数据包括起来，对其进行了填充（如有必要），并为其分配了序列号和安全参数索引（SPI）。 对于合并的 LSO 和 IPsec 卸载， [**NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)可能会有填充，在 NIC 将大数据包分段时，将丢弃此填充。 在 NDIS 的**PadLength**成员中指定填充量[ **\_IPSEC\_卸载\_V2\_标头\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v2_header_net_buffer_list_info)结构。 分段数据包可能需要填充以支持 IPsec 操作。

当协议驱动程序传输同时请求 LSO 和 IPsecOV2 的数据包时，它将不会成为 ESP 尾端的帧。 这是因为 ESP 尾端中的信息（例如填充长度）对于 NIC 生成的最后一段将不准确。

 

 





