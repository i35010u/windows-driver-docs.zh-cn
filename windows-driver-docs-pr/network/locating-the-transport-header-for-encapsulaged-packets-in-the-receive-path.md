---
title: 收到查找传输标头封装的数据包
description: 在接收路径中查找已封装数据包的传输标头
ms.assetid: D3BDE575-C9EB-49E3-9B61-FDB99B68ED8E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 657ad67c7c7721ac8313d190dc4868555020947d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356205"
---
# <a name="locating-the-transport-header-for-encapsulated-packets-in-the-receive-path"></a>在接收路径中查找已封装数据包的传输标头

在上接收数据包，NIC 的支持[网络虚拟化使用通用路由封装 (NVGRE)](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)封装数据包; 如果是，必须首先确定封装的类型。

**请注意**  在发送路径封装数据包，如果[ **NDIS\_TCP\_发送\_将卸载\_补充\_NET\_缓冲区\_列表\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_tcp_send_offloads_supplemental_net_buffer_list_info)。**IsEncapsulatedPacket**是**TRUE**。
 

在接收路径中，NIC 必须确定是否通过签入协议号来封装数据包**协议**IPv4 隧道 （外部） 标头的字段或**NextHeader** IPv6 字段隧道 （外部） 标头。 可以在找到的已分配的协议号列表<http://www.iana.org/assignments/protocol-numbers/protocol-numbers.xml>。

一旦确定数据包进行封装的数据包，NIC 必须通过分析封装的数据包协议确定到传输 （内部） IP 标头的偏移量。

NDIS 6.30 (Windows Server 2012) 和更高版本，支持仅 GRE IP 封装。 因此 NIC 应该是可以解析以下内容，具体取决于播发功能：

-   GRE ([RFC 2784:通用路由封装 (GRE)](https://tools.ietf.org/html/rfc2784)) 标头
-   [RFC 2890:键和序列号 GRE 扩展](https://tools.ietf.org/html/rfc2890)
-   IPv4 ([RFC 791:Internet 协议](https://tools.ietf.org/html/rfc791)) 标头
-   IPv6 ([RFC 2460:Internet 协议版本 6 (IPv6)](https://tools.ietf.org/html/rfc2460)) 标头

如果 NIC 发现未知或不受支持的封装协议，它必须将传递到主机堆栈保持不变的数据包。

因此，在接收路径上的微型端口必须传输 （内部） IP 标头以确定 IP 版本以及有关访问 TCP 或 UDP 标头分析。 这是新的要求 (Windows Server 2012) 的 NDIS 6.30 和更高版本。

 

 





