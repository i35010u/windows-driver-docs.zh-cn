---
title: 指示合并段
description: 本部分介绍如何指示合并段
ms.assetid: 79A37DAB-D9B3-4FA2-8258-05E10BD6E3CB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d363d286cb311ef44a7f783511f2e395518cb6c
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217590"
---
# <a name="indicating-coalesced-segments"></a>指示合并段


 (SCU) 的单个合并单元是一系列 TCP 段，这些段根据用于 [合并 Tcp/ip 段的规则](rules-for-coalescing-tcp-ip-packets.md)中定义的规则合并成单个 tcp 段。 本部分介绍如何指示生成的合并段。

SCU 必须：

-   通过调用 [**NdisMIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)来指示。

-   看起来像是通过线路接收的普通 TCP 段。

-   不能大于在 [RFC 791](http://www.ietf.org/rfc/rfc791.txt)第3.1 节中定义的最大合法 IP 数据报长度。

    **注意**   由于不能合并具有 IPv6 扩展标头的段 (请参阅[终止合并) 的异常情况](exception-conditions-that-terminate-coalescing.md)，IPv6 数据报的 SCU 大小也受最大合法数据报长度的限制。

     

NIC 或微型端口驱动程序应在指示合并段之前重新计算 TCP 和 IPv4 校验和（如果适用）。 如果 NIC 或微型端口驱动程序验证 TCP 和 IPv4 校验和，但不为合并段重新计算，则必须在[**NDIS \_ TCP \_ IP \_ 校验和 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_ip_checksum_net_buffer_list_info)结构中设置**TcpChecksumValueInvalid**和**IpChecksumValueInvalid**标志。 此外，在这种情况下，NIC 或微型端口驱动程序可能会在段中选择性地将 TCP 和 IPv4 标头校验值为零。

NIC 和微型端口驱动程序必须始终在[**NDIS \_ TCP \_ IP \_ 校验和 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_ip_checksum_net_buffer_list_info)结构中设置**IpChecksumSucceeded**和**TcpChecksumSucceeded**标志，然后才能指示合并段。

有关合并规则的详细信息，请参阅 [合并 Tcp/ip 段的规则](rules-for-coalescing-tcp-ip-packets.md)。

有关异常的详细信息，请参阅 [终止合并的异常条件](exception-conditions-that-terminate-coalescing.md)。

预期合并会尽力进行。 在某些情况下（例如由于缺少资源），硬件可能无法合并。 此处所述的要求主要用于指定何时进行合并，以及如何合并。

从较高层次来看，NIC 和微型端口驱动程序必须处理线路上 TCP 段的接收，如下所示：

-   检查传入段是否有异常，如下所示：

    1.  如果没有遇到异常，请检查段是否可以与每个规则的相同 TCP 连接收到的最后一个段相合并。

    2.  如果段触发了异常，或者如果不能将其与先前接收的段合并，则单独指示段。

-   NIC 和微型端口驱动程序不得指示已合并的段，直到协议驱动程序启用 RSC，如 [查询和更改 Rsc 状态](querying-and-changing-rsc-state.md)中所述。

-   对于给定 TCP 连接，从微型端口适配器到主机 TCP/IP 堆栈的数据指示可能包含一个或多个合并段，这些段由一个或多个无法合并的单独段分隔。

-   NIC 和微型端口驱动程序不得延迟 TCP 段（无论是否合并）的指示。 具体而言，NIC 和微型端口驱动程序不得将段的指示从一个延迟的过程调用 (DPC) 到下一个，以便尝试合并段。

-   NIC 和微型端口驱动程序可以使用计时器来确定合并结束。 不过，延迟敏感工作负荷的处理必须与 DPC 边界要求一样有效。

 

