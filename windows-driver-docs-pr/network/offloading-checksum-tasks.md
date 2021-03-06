---
title: 卸载校验和任务
description: 卸载校验和任务
keywords:
- 任务卸载 WDK TCP/IP 传输，校验和任务
- 校验和任务 WDK 网络
ms.date: 09/19/2018
ms.localizationpriority: medium
ms.openlocfilehash: 27995371e2c3a347d6a6d26b1b9f0bb9e2dad6a5
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248477"
---
# <a name="offloading-checksum-tasks"></a>卸载校验和任务

NDIS 支持在运行时卸载 TCP/IP 校验和任务。

> [!NOTE]
> 校验和卸载带外 (OOB) 数据存储在 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list) 信息数组中。 有关 OOB 数据的详细信息，请参阅 [访问 Tcp/ip 卸载网络 \_ 缓冲区 \_ 列表信息](accessing-tcp-ip-offload-net-buffer-list-information.md)。

在将 \_ \_ 小型端口驱动程序用于执行校验和任务的数据包的网络缓冲区列表结构传递到微型端口驱动程序之前，tcp/ip 传输会指定与网络 \_ 缓冲区列表结构关联的校验和信息 \_ 。 此信息由 [**NDIS \_ TCP \_ IP \_ 校验和 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/nblchecksum/ns-nblchecksum-ndis_tcp_ip_checksum_net_buffer_list_info) 结构指定，该结构是网络 \_ 缓冲区 \_ 列表信息 (带外数据) 的一部分，与网络 \_ 缓冲区 \_ 列表结构关联。

在为 TCP 数据包卸载校验和计算之前，TCP/IP 传输会计算 TCP pseudoheader 的补码和。 TCP/IP 传输在 pseudoheader 中的所有字段之间计算一次补码之和，包括源 IP 地址、目标 IP 地址、协议和 TCP 数据包的 TCP 长度。 TCP/IP 传输在 TCP 标头的校验和字段中输入 pseudoheader 的补码总和。

TCP/IP 传输提供的 pseudoheader 的补码 sum 使 NIC 在计算发送数据包的实际 TCP 校验和时提前开始。 若要计算实际 TCP 校验和，NIC 将计算 TCP 标头和负载) 的 TCP 校验和 (的可变部分，将此校验和添加到 TCP/IP 传输所计算的 pseudoheader 的补码总和，并为校验和计算16位的补码。 有关计算此类校验和的详细信息，请参阅 RFC 793 和 RFC 1122。

> [!NOTE]
> TCP/IP 传输使用与 TCP 数据包相同的步骤来计算 UDP 数据包的 pseudoheader 的补码和，并将该值存储在 UDP 标头的校验和字段中。

请注意，TCP/IP 传输总是确保数据包的 IP 标头中的校验和字段设置为零，然后将数据包传递到基础微型端口驱动程序。 微型端口驱动程序应忽略 IP 标头中的校验和字段。 微型端口驱动程序无需验证校验和字段是否设置为零，且不需要将此字段设置为零。

在收到网络 \_ 缓冲区 \_ 列表结构的 [*MiniportSendNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists) 或 [**MiniportCoSendNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_send_net_buffer_lists) 函数后，微型端口驱动程序通常会执行以下校验和处理：

1.  微型端口驱动程序调用 *\_ Id* 为 **TcpIpChecksumNetBufferListInfo** 的 [**网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/nblaccessors/nf-nblaccessors-net_buffer_list_info)宏，以获取 [**NDIS \_ TCP \_ IP \_ 校验和 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/nblchecksum/ns-nblchecksum-ndis_tcp_ip_checksum_net_buffer_list_info)结构。

2.  微型端口驱动程序会测试 NDIS  \_ TCP \_ IP \_ 校验和 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息结构中的 IsIPv4 和 IsIPv6 标志。 如果未设置 **IsIPv4** 和 **IsIPv6** 标志，则 NIC 不应对包执行任何校验和操作。

3.  如果设置了 **IsIPv4** 或 **IsIPv6** 标志，微型端口驱动程序会测试 **TcpChecksum**、 **UDPCHECKSUM** 和 **IpHeaderChecksum** 标志，以确定 NIC 应该为数据包计算哪些校验和。

4.  微型端口驱动程序将数据包传递到 NIC，这将计算数据包的相应校验和。 如果数据包具有隧道 IP 标头和传输 IP 标头，则支持 IP 校验和卸载的 NIC 将仅对隧道标头执行 IP 校验和任务。 TCP/IP 传输对传输 IP 标头执行 IP 校验和任务。

在为接收数据包指示用于执行校验和任务的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list)结构之前，微型端口驱动程序将验证相应的校验和，并在 NDIS TCP IP   \_ \_ \_ 校验和 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息结构中设置相应的 xxx * * * ChecksumFailed * 或 xxx * * * 标记。

如果启用了大规模发送卸载 (LSO) ，则关闭地址校验和卸载不会阻止微型端口驱动程序计算和插入由 LSO 功能生成的数据包中的校验和。 若要禁用地址校验和卸载，在这种情况下，用户还必须禁用 LSO。

 

