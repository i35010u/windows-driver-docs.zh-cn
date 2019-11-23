---
title: 卸载校验和任务
description: 卸载校验和任务
ms.assetid: 5fb2f379-c357-4ec3-b103-bdbe23fcc033
keywords:
- 任务卸载 WDK TCP/IP 传输，校验和任务
- 校验和任务 WDK 网络
ms.date: 09/19/2018
ms.localizationpriority: medium
ms.openlocfilehash: b8f5f83914519db0a820c1d234018b20f930df1a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844330"
---
# <a name="offloading-checksum-tasks"></a>卸载校验和任务

NDIS 支持在运行时卸载 TCP/IP 校验和任务。

> [!NOTE]
> 校验和卸载带外（OOB）数据将存储在[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)信息数组中。 有关 OOB 数据的详细信息，请参阅[访问 Tcp/ip 卸载 NET\_BUFFER\_列表信息](accessing-tcp-ip-offload-net-buffer-list-information.md)。

在向微型端口驱动程序传递一个网络\_缓冲区\_列表结构（其中，微型端口驱动程序将在其上执行校验和任务）之前，TCP/IP 传输会指定与 NET\_缓冲区\_列表结构关联的校验和信息。 此信息由[**NDIS\_TCP\_IP\_校验和\_NET\_buffer\_list\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_ip_checksum_net_buffer_list_info)结构，这是与 NET\_BUFFER\_list 结构关联的 net\_BUFFER\_列表信息（带外数据）的一部分。

在为 TCP 数据包卸载校验和计算之前，TCP/IP 传输会计算 TCP pseudoheader 的补码和。 TCP/IP 传输在 pseudoheader 中的所有字段之间计算一次补码之和，包括源 IP 地址、目标 IP 地址、协议和 TCP 数据包的 TCP 长度。 TCP/IP 传输在 TCP 标头的校验和字段中输入 pseudoheader 的补码总和。

TCP/IP 传输提供的 pseudoheader 的补码 sum 使 NIC 在计算发送数据包的实际 TCP 校验和时提前开始。 若要计算实际 TCP 校验和，NIC 将计算 TCP 校验和的可变部分（对于 TCP 标头和负载），将此校验和添加到由 TCP/IP 传输计算的 pseudoheader 的补码总和，并计算16位一校验和的补充。 有关计算此类校验和的详细信息，请参阅 RFC 793 和 RFC 1122。

> [!NOTE]
> TCP/IP 传输使用与 TCP 数据包相同的步骤来计算 UDP 数据包的 pseudoheader 的补码和，并将该值存储在 UDP 标头的校验和字段中。

请注意，TCP/IP 传输总是确保数据包的 IP 标头中的校验和字段设置为零，然后将数据包传递到基础微型端口驱动程序。 微型端口驱动程序应忽略 IP 标头中的校验和字段。 微型端口驱动程序无需验证校验和字段是否设置为零，且不需要将此字段设置为零。

在它的[*MiniportSendNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists)或[**MiniportCoSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_send_net_buffer_lists)函数中收到 NET\_BUFFER\_列表结构后，微型端口驱动程序通常会执行以下校验和处理：

1.  微型端口驱动程序使用 *\_Id* **TcpIpChecksumNetBufferListInfo**调用[**net\_BUFFER\_LIST\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-info)宏，以获取[**NDIS\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_ip_checksum_net_buffer_list_info)\_\_\_\_\_\_

2.  微型端口驱动程序会测试 NDIS 中的**IsIPv4**和**ISIPV6**标志\_TCP\_IP\_校验和\_NET\_BUFFER\_LIST\_INFO 结构。 如果未设置**IsIPv4**和**IsIPv6**标志，则 NIC 不应对包执行任何校验和操作。

3.  如果设置了**IsIPv4**或**IsIPv6**标志，微型端口驱动程序会测试**TcpChecksum**、 **UDPCHECKSUM**和**IpHeaderChecksum**标志，以确定 NIC 应该为数据包计算哪些校验和。

4.  微型端口驱动程序将数据包传递到 NIC，这将计算数据包的相应校验和。 如果数据包具有隧道 IP 标头和传输 IP 标头，则支持 IP 校验和卸载的 NIC 将仅对隧道标头执行 IP 校验和任务。 TCP/IP 传输对传输 IP 标头执行 IP 校验和任务。

在为用于执行校验和任务的接收数据包指示[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构之前，微型端口驱动程序将验证相应的校验和，并在 NDIS\_TCP\_IP\_校验和中设置相应的*Xxx * * ChecksumFailed** 或*xxx * ** * 标记\_\_\_\_

如果启用了大规模发送卸载（LSO），则关闭地址校验和卸载不会阻止微型端口驱动程序计算和插入由 LSO 功能生成的数据包中的校验和。 若要禁用地址校验和卸载，在这种情况下，用户还必须禁用 LSO。

 

 





