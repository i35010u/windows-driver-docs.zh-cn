---
title: 在校验和卸载中支持 NVGRE
description: 本部分介绍了校验和卸载中的支持 NVGRE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 706e9cab48f30d49056fe778c465f83a004538d9
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102247822"
---
# <a name="supporting-nvgre-in-checksum-offload"></a>在校验和卸载中支持 NVGRE


 (Windows Server 2012) NDIS 6.30 介绍了 [使用通用路由封装的网络虚拟化 (NVGRE) ](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)。 卸载校验和任务的 NDIS 微型端口、协议和筛选器驱动程序和 Nic 应该以支持 NVGRE 的方式进行。

**注意**  本页假设你熟悉 [卸载校验和任务](offloading-checksum-tasks.md)中的信息。

 

如果 [**NDIS \_ TCP \_ 发送将 \_ 卸载 \_ 补充的 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_send_offloads_supplemental_net_buffer_list_info)。**IsEncapsulatedPacket** 为 **TRUE** ，并且 **TCPIPCHECKSUMNETBUFFERLISTINFO** 带外 (OOB) 信息有效，这表示需要 NVGRE 支持，NIC 必须为隧道 (外部) ip 标头、传输 (内部) ip 标头以及 TCP 或 UDP 标头进行计算。

[**NDIS \_ TCP \_ IP \_ 校验和 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/nblchecksum/ns-nblchecksum-ndis_tcp_ip_checksum_net_buffer_list_info)结构中的 **IsIPv4** 和 **ISIPV6** 标志表明隧道的 ip 标头版本 (外部) ip 标头。 NIC 必须分析传输 (内部) IP 标头以确定标头的 IP 版本。 由于允许混合模式数据包 (请参阅 [**NDIS \_ 封装的 \_ 数据包 \_ 任务 \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_encapsulated_packet_task_offload)) ，NIC 不得假设内部和外部 IP 标头具有相同的 ip 标头版本。

Nic 和微型端口驱动程序可以使用 [**NDIS \_ TCP \_ 发送 \_ \_ \_ \_ \_ \_**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_send_offloads_supplemental_net_buffer_list_info)中提供的 **InnerFrameOffset**、 **TransportIpHeaderRelativeOffset** 和 **TcpHeaderRelativeOffset** 值。 NIC 或微型端口驱动程序可以在隧道上执行任何所需的标头检查 (外部) IP 标头或后续标头来验证这些偏移量。

请注意，在 [**NDIS TCP 发送时，会 \_ \_ \_ 卸载补充的 \_ \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_send_offloads_supplemental_net_buffer_list_info)。**IsEncapsulatedPacket** 为 TRUE，现有的标头偏移量字段， [**NDIS \_ TCP \_ 大规模 \_ 发送 \_ 卸载 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/nbllso/ns-nbllso-ndis_tcp_large_send_offload_net_buffer_list_info)。**LsoV2Transmit**。**TcpHeaderOffset** 和 [**NDIS \_ TCP \_ IP \_ 校验和 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/nblchecksum/ns-nblchecksum-ndis_tcp_ip_checksum_net_buffer_list_info)。**传输**。**TcpHeaderOffset** 的值不正确，NIC 或驱动程序不得使用这些值。

微型端口驱动程序必须处理 [**NDIS \_ TCP \_ 发送 \_ 卸载补充的 \_ \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_send_offloads_supplemental_net_buffer_list_info)的情况。**InnerFrameOffset** 可能在不同于数据包开头的分散列表列表中。 协议驱动程序将保证所有预置的封装标头 (ETH、IP、GRE) 在物理上是连续的，并将位于数据包的第一 MDL。

## <a name="checksum-validation"></a>校验和验证


NVGRE 的校验和验证在很大程度上与否则相同。

如果某个微型端口接收到 [oid \_ TCP \_ 卸载 \_ 参数](./oid-tcp-offload-parameters.md) OID 请求并成功为 **ndis \_ 封装 \_ 类型 \_ GRE \_ MAC** (参阅 [**ndis \_ 卸载 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters)) ，则 NIC 必须对隧道 (外部) ip 标头、传输 (内部) ip 标头以及 TCP 或 UDP 标头执行校验和验证。

对于具有 IPv4 隧道 (外部) 标头和 IPv4 传输 (内部) 标头的封装的数据包，只有在 IP 标头校验和验证成功的情况下，微型端口驱动程序才应在 [**NDIS \_ TCP \_ IP \_ 校验和 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/nblchecksum/ns-nblchecksum-ndis_tcp_ip_checksum_net_buffer_list_info)结构中设置 **IpChecksumSucceeded** 标志。 对于同时具有隧道 (外部) IPv4 标头和传输 (内部) IPv4 标头的封装的数据包，如果 IP 标头校验和验证失败之一，微型端口驱动程序应设置 **IpChecksumFailed** 标志。

 

