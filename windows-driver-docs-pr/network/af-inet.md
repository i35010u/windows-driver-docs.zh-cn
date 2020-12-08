---
title: AF_INET
description: AF_INET
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 AF_INET 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d8bbb9dc22f8553feda1f1e576689655a25ddc3c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794731"
---
# <a name="af_inet"></a>AF \_ INET


AF \_ INET address 系列是 IPv4 地址族。

### <a name="socket-address-structure"></a>套接字地址结构

使用结构 [**\_ 中的 SOCKADDR**](/windows/win32/api/ws2def/ns-ws2def-sockaddr_in) 指定 IPv4 传输地址。

### <a name="socket-types"></a>套接字类型

IPv4 支持以下套接字类型：

<a href="" id="sock-stream"></a>SOCK \_ 流  
支持可靠的面向连接的字节流通信。

<a href="" id="sock-dgram"></a>SOCK \_ DGRAM  
支持不可靠的无连接数据报通信。

<a href="" id="sock-raw"></a>SOCK \_ RAW  
支持对传输协议的原始访问。

当 WSK 应用程序调用 [**WskSocket**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket) 函数或 [**WskSocketConnect**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket_connect) 函数来创建新的套接字时，它指定套接字类型。

### <a name="protocols"></a>协议

\_WSK 头文件中定义了 IPPROTO 枚举的以下 IPV4 IPPROTO *XXX* 协议值：

<a href="" id="ipproto-ip"></a>IPPROTO \_ IP  
Internet 协议选项

<a href="" id="ipproto-icmp"></a>IPPROTO \_ ICMP  
Internet 控制消息协议

<a href="" id="ipproto-igmp"></a>IPPROTO \_ IGMP  
Internet 组管理协议

<a href="" id="ipproto-ggp"></a>IPPROTO \_ GGP  
网关到网关协议

<a href="" id="ipproto-ipv4"></a>IPPROTO \_ IPV4  
IPv4 封装

<a href="" id="ipproto-st"></a>IPPROTO \_ ST  
流协议

<a href="" id="ipproto-tcp"></a>IPPROTO \_ TCP  
传输控制协议

<a href="" id="ipproto-cbt"></a>IPPROTO \_ CBT  
基于内核的树协议

<a href="" id="ipproto-egp"></a>IPPROTO \_ EGP  
外部网关协议

<a href="" id="ipproto-igp"></a>IPPROTO \_ IGP  
专用内部网关协议

<a href="" id="ipproto-pup"></a>IPPROTO \_ PUP  
PARC 通用数据包协议

<a href="" id="ipproto-udp"></a>IPPROTO \_ UDP  
用户数据报协议

<a href="" id="ipproto-idp"></a>IPPROTO \_ IDP  
Internet 数据报协议

<a href="" id="ipproto-rdp"></a>IPPROTO \_ RDP  
可靠的数据协议

<a href="" id="ipproto-nd"></a>IPPROTO \_ ND  
网络磁盘协议

<a href="" id="ipproto-iclfxbm"></a>IPPROTO \_ ICLFXBM  
宽带监视

<a href="" id="ipproto-pim"></a>IPPROTO \_ PIM  
独立于协议的多播

<a href="" id="ipproto-pgm"></a>IPPROTO \_ PGM  
实用常规多播

<a href="" id="ipproto-l2tp"></a>IPPROTO \_ L2TP  
2级隧道协议

<a href="" id="ipproto-sctp"></a>IPPROTO \_ SCTP  
流控制传输协议

<a href="" id="ipproto-raw"></a>IPPROTO \_ RAW  
原始 IP 数据包

使用原始套接字支持其他协议。

WSK 应用程序在调用 [**WskSocket**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket) 函数或 [**WskSocketConnect**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket_connect) 函数来创建新的套接字时指定协议。

当 WSK 应用程序调用 [**WskControlSocket**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)函数来设置或检索传输协议级别或网络协议级别套接字选项时，它还将协议 (指定为 *Level* 参数) 。

### <a name="combinations"></a>各种

对于每个 WSK [套接字类别](./winsock-kernel-socket-categories.md)，IPv4 支持以下套接字类型和协议组合：

基本套接 SOCK \_ STREAM + IPPROTO \_ TCP SOCK \_ DGRAM + IPPROTO \_ UDP SOCK \_ RAW + IPPROTO \_ *XXX* 侦听套接字 SOCK \_ STREAM + IPPROTO \_ TCP

数据报套接字 SOCK \_ DGRAM + IPPROTO \_ UDP SOCK \_ RAW + IPPROTO \_ *Xxx* Connection-Oriented 套接字 SOCK \_ STREAM + IPPROTO \_ TCP

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
<td>Ws2def (包含 Wsk) </td>
</tr>
</tbody>
</table>

 

