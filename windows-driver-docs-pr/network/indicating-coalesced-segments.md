---
title: 指示合并段
description: 本部分介绍如何以指示合并的段
ms.assetid: 79A37DAB-D9B3-4FA2-8258-05E10BD6E3CB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be13f521a54a65da4942868bb7331321993471f8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374827"
---
# <a name="indicating-coalesced-segments"></a>指示合并段


单个合并的单元 (SCU) 是一系列合并到单个 TCP 段根据规则中定义的 TCP 段[规则合并 TCP/IP 段](rules-for-coalescing-tcp-ip-packets.md)。 本部分介绍如何指示生成合并的段。

SCU 必须：

-   通过调用指示[ **NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatereceivenetbufferlists)。

-   如通过网络接收的正常 TCP 段所示。

-   不能大于最大法律 IP 数据报长度，如 3.1 节中定义[RFC 791](http://www.ietf.org/rfc/rfc791.txt)。

    **请注意**  因为不能合并使用 IPv6 扩展标头段 (请参阅[异常条件终止合并](exception-conditions-that-terminate-coalescing.md))，为 IPv6 数据报 SCU 的大小也限制了最大法律数据报长度。

     

NIC 或微型端口驱动程序应重新计算的 TCP 和 IPv4 校验和，如果适用之前，该值指示合并的段。 如果 NIC 或微型端口驱动程序验证 TCP 和 IPv4 校验和，但不会不重新计算这些合并段，它必须设置**TcpChecksumValueInvalid**并**IpChecksumValueInvalid**标记中[ **NDIS\_TCP\_IP\_校验和\_NET\_缓冲区\_列表\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_tcp_ip_checksum_net_buffer_list_info)结构。 此外，在这种情况下该 NIC 或微型端口驱动程序可能根据需要清零的段中的 TCP 和 IPv4 的标头的校验和值。

NIC 和微型端口驱动程序必须始终设置**IpChecksumSucceeded**并**TcpChecksumSucceeded**标记中[ **NDIS\_TCP\_IP\_CHECKSUM\_NET\_缓冲区\_列表\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_tcp_ip_checksum_net_buffer_list_info)结构之前，该值指示合并的段。

有关合并的规则的详细信息，请参阅[规则合并 TCP/IP 段](rules-for-coalescing-tcp-ip-packets.md)。

有关异常的详细信息，请参阅[异常条件终止合并](exception-conditions-that-terminate-coalescing.md)。

合并被应在最大程度上执行。 硬件可能无法再进行合并在某些情况下，例如由于缺乏资源。 要求说明以下主要是以指定何时不 coalesce 和如何合并。

在高级别中，NIC 和微型端口驱动程序必须处理的 TCP 段的接收通过网络，如下所示：

-   检查异常的传入段，如下所示：

    1.  如果未遇到异常，请检查是否可为每个规则的同一 TCP 连接接收的最后一个段与合并段。

    2.  如果段触发异常，或者如果不能与以前接收段合并，然后分别指示段。

-   NIC 和微型端口驱动程序必须指示合并的段，直到协议驱动程序中所述启用 RSC[查询和更改 RSC 状态](querying-and-changing-rsc-state.md)。

-   对于给定的 TCP 连接，从微型端口适配器的主机 TCP/IP 堆栈的数据指示可能会包含一个或多个合并，分隔的段未合并的一个或多个各个段。

-   NIC 和微型端口驱动程序不能在是否合并或不延迟的 TCP 段的指示。 具体而言，NIC 和微型端口驱动程序不能延迟中一个延迟的过程调用 (DPC) 到下一步以便尝试 coalesce 段的段的指示。

-   NIC 和微型端口驱动程序可能使用计时器来确定的合并末尾。 但是，延迟敏感的工作负荷的处理必须是有效地 DPC 边界要求。

 

 





