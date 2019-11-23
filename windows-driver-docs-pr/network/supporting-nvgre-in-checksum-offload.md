---
title: 在校验和卸载中支持 NVGRE
description: 本部分介绍了校验和卸载中的支持 NVGRE
ms.assetid: 933EE18B-917A-40BC-87AA-0F463615A082
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9b698da69fcc65bf31aea0c91bb79f9b330d869
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841797"
---
# <a name="supporting-nvgre-in-checksum-offload"></a>在校验和卸载中支持 NVGRE


NDIS 6.30 （Windows Server 2012）[使用通用路由封装（NVGRE）引入网络虚拟化](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)。 卸载校验和任务的 NDIS 微型端口、协议和筛选器驱动程序和 Nic 应该以支持 NVGRE 的方式进行。

**请注意**  本页假设你熟悉[卸载校验和任务](offloading-checksum-tasks.md)中的信息。

 

如果[**NDIS\_TCP\_发送\_卸载\_补充\_NET\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_send_offloads_supplemental_net_buffer_list_info)\_\_的信息。**IsEncapsulatedPacket**为**TRUE** ，并且**TcpIpChecksumNetBufferListInfo**带外（OOB）信息有效，这表示需要 NVGRE 支持，NIC 必须计算隧道（外部） ip 标头、传输（内部） IP 标头和 TCP 或 UDP 标头的校验和。

NDIS 中的**IsIPv4**和**ISIPV6**标志[ **\_TCP\_IP\_校验和\_NET\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_ip_checksum_net_buffer_list_info)结构指示隧道（外部） ip 标头的 ip 标头版本。 NIC 必须分析传输（内部） IP 标头以确定标头的 IP 版本。 由于允许混合模式数据包（请参阅[**NDIS\_封装\_数据包\_任务\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_encapsulated_packet_task_offload)），NIC 不得假设内部和外部 IP 标头具有相同的 ip 标头版本。

Nic 和微型端口驱动程序可以使用 NDIS\_TCP\_中提供的**InnerFrameOffset**、 **TransportIpHeaderRelativeOffset**和**TcpHeaderRelativeOffset**值[**发送\_卸载\_补充\_网络\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_send_offloads_supplemental_net_buffer_list_info)\_\_信息结构。 NIC 或微型端口驱动程序可以对隧道（外部） IP 标头或后续标头执行任何所需的标头检查来验证这些偏移量。

请注意，在[**NDIS\_TCP\_发送\_卸载\_补充\_NET\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_send_offloads_supplemental_net_buffer_list_info)\_\_的信息。**IsEncapsulatedPacket**为 TRUE，现有的标头偏移字段， [**NDIS\_TCP\_大型\_发送\_卸载\_NET\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_large_send_offload_net_buffer_list_info)\_\_的信息。**LsoV2Transmit**。**TcpHeaderOffset**和[**NDIS\_TCP\_IP\_校验和\_NET\_BUFFER\_列出\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_ip_checksum_net_buffer_list_info)。**传输**。**TcpHeaderOffset**的值不正确，NIC 或驱动程序不得使用这些值。

微型端口驱动程序必须处理[**NDIS\_TCP\_发送\_卸载\_补充\_NET\_\_\_列表信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_send_offloads_supplemental_net_buffer_list_info)的情况。**InnerFrameOffset**可能在不同于数据包开头的分散列表列表中。 协议驱动程序将保证所有预置的封装标头（ETH、IP、GRE）在物理上是连续的，并将位于数据包的第一 MDL。

## <a name="checksum-validation"></a>校验和验证


NVGRE 的校验和验证在很大程度上与否则相同。

如果某个微型端口接收到[oid\_TCP\_卸载\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-parameters)OID 请求并成功为**NDIS\_封装\_类型\_GRE\_MAC** （请参阅[**ndis\_卸载\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters)），则 NIC 必须对隧道（外部） ip 标头、传输（内部） IP 标头以及 TCP 或 UDP 标头执行校验和验证。

对于具有 IPv4 隧道（外部）标头和 IPv4 传输（内部）标头的封装的数据包，微型端口驱动程序应仅在两个 IP 标头校验和验证成功的情况下，在[**NDIS\_TCP\_IP\_\_\_CHECKSUM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_ip_checksum_net_buffer_list_info)中设置**IpChecksumSucceeded**标志。\_\_ 对于同时具有隧道（外部） IPv4 标头和传输（内部） IPv4 标头的封装的数据包，如果 IP 标头校验和验证中的任何一个验证失败，微型端口驱动程序应设置**IpChecksumFailed**标志。

 

 





