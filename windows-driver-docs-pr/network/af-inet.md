---
title: AF_INET
description: AF_INET
ms.assetid: 59e12f8d-02eb-413c-bc04-6b9b6e4adde6
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 AF_INET 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d4d1293dde037e87d2c5f5c010f7fd911c199314
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835395"
---
# <a name="af_inet"></a>AF\_INET


AF\_INET address 系列是 IPv4 的地址族。

### <a name="socket-address-structure"></a>套接字地址结构

使用结构[**中的 SOCKADDR\_** ](https://docs.microsoft.com/windows/desktop/api/ws2def/ns-ws2def-sockaddr_in)指定 IPv4 传输地址。

### <a name="socket-types"></a>套接字类型

IPv4 支持以下套接字类型：

<a href="" id="sock-stream"></a>SOCK\_流  
支持可靠的面向连接的字节流通信。

<a href="" id="sock-dgram"></a>SOCK\_DGRAM  
支持不可靠的无连接数据报通信。

<a href="" id="sock-raw"></a>SOCK\_RAW  
支持对传输协议的原始访问。

当 WSK 应用程序调用[**WskSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket)函数或[**WskSocketConnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket_connect)函数来创建新的套接字时，它指定套接字类型。

### <a name="protocols"></a>协议

WSK 头文件中定义了 IPPROTO 枚举的以下 IPv4 IPPROTO\_*XXX*协议值：

<a href="" id="ipproto-ip"></a>IPPROTO\_IP  
Internet 协议选项

<a href="" id="ipproto-icmp"></a>IPPROTO\_ICMP  
Internet 控制消息协议

<a href="" id="ipproto-igmp"></a>IPPROTO\_IGMP  
Internet 组管理协议

<a href="" id="ipproto-ggp"></a>IPPROTO\_GGP  
网关到网关协议

<a href="" id="ipproto-ipv4"></a>IPPROTO\_IPV4  
IPv4 封装

<a href="" id="ipproto-st"></a>IPPROTO\_ST  
流协议

<a href="" id="ipproto-tcp"></a>IPPROTO\_TCP  
传输控制协议

<a href="" id="ipproto-cbt"></a>IPPROTO\_CBT  
基于内核的树协议

<a href="" id="ipproto-egp"></a>IPPROTO\_EGP  
外部网关协议

<a href="" id="ipproto-igp"></a>IPPROTO\_IGP  
专用内部网关协议

<a href="" id="ipproto-pup"></a>IPPROTO\_PUP  
PARC 通用数据包协议

<a href="" id="ipproto-udp"></a>IPPROTO\_UDP  
用户数据报协议

<a href="" id="ipproto-idp"></a>IPPROTO\_IDP  
Internet 数据报协议

<a href="" id="ipproto-rdp"></a>IPPROTO\_RDP  
可靠的数据协议

<a href="" id="ipproto-nd"></a>IPPROTO\_ND  
网络磁盘协议

<a href="" id="ipproto-iclfxbm"></a>IPPROTO\_ICLFXBM  
宽带监视

<a href="" id="ipproto-pim"></a>IPPROTO\_PIM  
独立于协议的多播

<a href="" id="ipproto-pgm"></a>IPPROTO\_PGM  
实用常规多播

<a href="" id="ipproto-l2tp"></a>IPPROTO\_L2TP  
2级隧道协议

<a href="" id="ipproto-sctp"></a>IPPROTO\_SCTP  
流控制传输协议

<a href="" id="ipproto-raw"></a>IPPROTO\_RAW  
原始 IP 数据包

使用原始套接字支持其他协议。

WSK 应用程序在调用[**WskSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket)函数或[**WskSocketConnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket_connect)函数来创建新的套接字时指定协议。

当 WSK 应用程序调用[**WskControlSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)函数设置或检索传输协议级别或网络协议级别套接字选项时，它还指定协议（作为*Level*参数）。

### <a name="combinations"></a>各种

对于每个 WSK[套接字类别](https://docs.microsoft.com/windows-hardware/drivers/network/winsock-kernel-socket-categories)，IPv4 支持以下套接字类型和协议组合：

基本套接字 SOCK\_STREAM + IPPROTO\_TCP SOCK\_DGRAM + IPPROTO\_UDP SOCK\_RAW + IPPROTO\_*Xxx*侦听套接字 SOCK\_STREAM + IPPROTO\_TCP

数据报套接字 SOCK\_DGRAM + IPPROTO\_UDP SOCK\_RAW + IPPROTO\_*Xxx*面向连接的套接字 SOCK\_STREAM + IPPROTO\_TCP

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>在 Windows Vista 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ws2def （包括 Wsk）</td>
</tr>
</tbody>
</table>

 

 




