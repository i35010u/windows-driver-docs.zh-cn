---
title: AF_INET6
description: AF_INET6
ms.assetid: 58d36a1e-cda2-42aa-9563-96df2f7319b2
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 AF_INET6 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 142902974f1210337bfb57df62206c1aff404e24
ms.sourcegitcommit: 57b649e59a2be2055413982035d89bc85e3e425d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/22/2020
ms.locfileid: "85133281"
---
# <a name="af_inet6"></a>AF \_ INET6


AF \_ INET6 address 系列是 IPv6 的地址族。

### <a name="socket-address-structure"></a>套接字地址结构

IPv6 传输地址是使用[**SOCKADDR \_ IN6**](https://docs.microsoft.com/windows/win32/api/ws2ipdef/ns-ws2ipdef-sockaddr_in6_lh)结构指定的。

### <a name="socket-types"></a>套接字类型

IPv6 支持以下套接字类型：

<a href="" id="sock-stream"></a>SOCK \_ 流  
支持可靠的面向连接的字节流通信。

<a href="" id="sock-dgram"></a>SOCK \_ DGRAM  
支持不可靠的无连接数据报通信。

<a href="" id="sock-raw"></a>SOCK \_ RAW  
支持对传输协议的原始访问。

当 WSK 应用程序调用[**WskSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket)函数或[**WskSocketConnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket_connect)函数来创建新的套接字时，它指定套接字类型。

### <a name="protocols"></a>协议

IPPROTO 枚举的以下 IPv6 IPPROTO \_ *XXX*协议值在 WSK 标头文件中定义：

<a href="" id="ipproto-hopopts"></a>IPPROTO \_ HOPOPTS  
IPv6 逐跃点选项

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

<a href="" id="ipproto-ipv6"></a>IPPROTO \_ IPV6  
IPv6 标头

<a href="" id="ipproto-routing"></a>IPPROTO \_ 路由  
IPv6 路由标头

<a href="" id="ipproto-fragment"></a>IPPROTO \_ 片段  
IPv6 碎片标头

<a href="" id="ipproto-esp"></a>IPPROTO \_ ESP  
封装安全有效负载

<a href="" id="ipproto-ah"></a>IPPROTO \_ AH  
身份验证标头

<a href="" id="ipproto-icmpv6"></a>IPPROTO \_ ICMPV6  
IPv6 Internet 控制消息协议

<a href="" id="ipproto-none"></a>\_无 IPPROTO  
IPv6 无下一个标头

<a href="" id="ipproto-dstopts"></a>IPPROTO \_ DSTOPTS  
IPv6 目标选项

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

WSK 应用程序在调用[**WskSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket)函数或[**WskSocketConnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket_connect)函数来创建新的套接字时指定协议。

当 WSK 应用程序调用[**WskControlSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)函数设置或检索传输协议级别或网络协议级别套接字选项时，它还指定协议（作为*Level*参数）。

### <a name="combinations"></a>各种

对于每个 WSK[套接字类别](https://docs.microsoft.com/windows-hardware/drivers/network/winsock-kernel-socket-categories)，IPv6 支持以下套接字类型和协议的组合：

基本套接 SOCK \_ STREAM + IPPROTO \_ TCP SOCK \_ DGRAM + IPPROTO \_ UDP SOCK \_ RAW + IPPROTO \_ *XXX*侦听套接字 SOCK \_ STREAM + IPPROTO \_ TCP

数据报套接字 SOCK \_ DGRAM + IPPROTO \_ UDP SOCK \_ RAW + IPPROTO \_ *Xxx*面向连接的套接字 SOCK \_ STREAM + IPPROTO \_ TCP

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

 

 




