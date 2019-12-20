---
title: 正在为接收的封装的数据包定位传输标头
description: 在接收路径中查找已封装数据包的传输标头
ms.assetid: D3BDE575-C9EB-49E3-9B61-FDB99B68ED8E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0232f08a5b0a90990a94f60d79ba9b47ce49ecef
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210253"
---
# <a name="locating-the-transport-header-for-encapsulated-packets-in-the-receive-path"></a>在接收路径中查找已封装数据包的传输标头

接收数据包时，支持[使用通用路由封装的网络虚拟化（NVGRE）](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)的 NIC 必须首先确定是否封装数据包，如果是，则为封装类型。

**请注意**，在发送路径  ，如果[**NDIS\_TCP\_发送\_卸载\_补充\_**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_tcp_send_offloads_supplemental_net_buffer_list_info)\_\_\_**IsEncapsulatedPacket**为**TRUE**。
 

在接收路径中，NIC 必须通过检查 IPv4 隧道（外部）标头的 "**协议**" 字段中的协议号或 IPv6 隧道（外部）标头的**NextHeader**字段，来确定数据包是否已封装。 可在 <https://www.iana.org/assignments/protocol-numbers/protocol-numbers.xml>找到分配的协议编号的列表。

一旦将数据包确定为封装的数据包，NIC 就必须通过分析封装的数据包协议来确定传输（内部） IP 标头的偏移量。

对于 NDIS 6.30 （Windows Server 2012）和更高版本，仅支持 GRE IP 封装。 因此 NIC 应该能够分析以下内容，具体取决于广告功能：

-   GRE （[RFC 2784：通用路由封装（GRE）](https://tools.ietf.org/html/rfc2784)）标头
-   [RFC 2890： GRE 的密钥和序列号扩展](https://tools.ietf.org/html/rfc2890)
-   IPv4 （[RFC 791： Internet 协议](https://tools.ietf.org/html/rfc791)）标头
-   IPv6 （[RFC 2460： Internet 协议，版本6（IPv6）](https://tools.ietf.org/html/rfc2460)）标头

如果 NIC 发现未知或不受支持的封装协议，则必须将数据包原样传递到主机堆栈。

因此，在接收路径上，微型端口必须分析传输（内部） IP 标头，以确定 IP 版本以及访问 TCP 或 UDP 标头。 这是对 NDIS 6.30 （Windows Server 2012）和更高版本的新要求。

 

 





