---
title: AF_INET6
description: AF_INET6
ms.assetid: 58d36a1e-cda2-42aa-9563-96df2f7319b2
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 AF_INET6 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 2a5279716f63da4ff24edc1f5e34cd0cac23fde8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382930"
---
# <a name="afinet6"></a>AF\_INET6


AF\_INET6 地址系列是 IPv6 的地址族。

### <a name="socket-address-structure"></a>套接字地址结构

使用指定的 IPv6 传输地址[ **SOCKADDR\_IN6** ](https://docs.microsoft.com/windows/desktop/api/ws2ipdef/ns-ws2ipdef-sockaddr_in6)结构。

### <a name="socket-types"></a>套接字类型

IPv6 支持以下的套接字类型：

<a href="" id="sock-stream"></a>热歌劲\_流  
支持可靠的面向连接的字节流进行通信。

<a href="" id="sock-dgram"></a>热歌劲\_DGRAM  
支持不可靠的无连接数据报进行通信。

<a href="" id="sock-raw"></a>热歌劲\_RAW  
支持的传输协议对原始访问。

WSK 应用程序指定套接字类型时，它调用[ **WskSocket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_socket)函数或[ **WskSocketConnect** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_socket_connect)函数来创建新的套接字。

### <a name="protocols"></a>协议

以下 IPv6 IPPROTO\_*XXX* WSK 标头文件中定义协议 IPPROTO 枚举值：

<a href="" id="ipproto-hopopts"></a>IPPROTO\_HOPOPTS  
IPv6 逐跳选项

<a href="" id="ipproto-icmp"></a>IPPROTO\_ICMP  
Internet 控制消息协议

<a href="" id="ipproto-igmp"></a>IPPROTO\_IGMP  
Internet 组管理协议

<a href="" id="ipproto-ggp"></a>IPPROTO\_GGP  
网关到网关协议

<a href="" id="ipproto-ipv4"></a>IPPROTO\_IPV4  
IPv4 封装

<a href="" id="ipproto-st"></a>IPPROTO\_ST  
Stream 协议

<a href="" id="ipproto-tcp"></a>IPPROTO\_TCP  
传输控制协议

<a href="" id="ipproto-cbt"></a>IPPROTO\_CBT  
基于内核树协议

<a href="" id="ipproto-egp"></a>IPPROTO\_EGP  
外部网关协议

<a href="" id="ipproto-igp"></a>IPPROTO\_IGP  
专用的内部网关协议

<a href="" id="ipproto-pup"></a>IPPROTO\_PUP  
PARC 通用数据包协议

<a href="" id="ipproto-udp"></a>IPPROTO\_UDP  
用户数据报协议

<a href="" id="ipproto-idp"></a>IPPROTO\_IDP  
Internet 数据报协议

<a href="" id="ipproto-rdp"></a>IPPROTO\_RDP  
可靠的数据协议

<a href="" id="ipproto-ipv6"></a>IPPROTO\_IPV6  
IPv6 标头

<a href="" id="ipproto-routing"></a>IPPROTO\_路由  
IPv6 路由标头

<a href="" id="ipproto-fragment"></a>IPPROTO\_片段  
IPv6 碎片标头

<a href="" id="ipproto-esp"></a>IPPROTO\_ESP  
封装安全负载

<a href="" id="ipproto-ah"></a>IPPROTO\_AH  
身份验证标头

<a href="" id="ipproto-icmpv6"></a>IPPROTO\_ICMPV6  
IPv6 Internet 控制消息协议

<a href="" id="ipproto-none"></a>IPPROTO\_NONE  
IPv6 无下一步的标头

<a href="" id="ipproto-dstopts"></a>IPPROTO\_DSTOPTS  
IPv6 目标选项

<a href="" id="ipproto-nd"></a>IPPROTO\_ND  
网络磁盘协议

<a href="" id="ipproto-iclfxbm"></a>IPPROTO\_ICLFXBM  
宽带监视

<a href="" id="ipproto-pim"></a>IPPROTO\_PIM  
协议无关多播

<a href="" id="ipproto-pgm"></a>IPPROTO\_PGM  
实用的常规多播

<a href="" id="ipproto-l2tp"></a>IPPROTO\_L2TP  
级别 2 的隧道协议

<a href="" id="ipproto-sctp"></a>IPPROTO\_SCTP  
Stream 控制传输协议

<a href="" id="ipproto-raw"></a>IPPROTO\_RAW  
原始 IP 数据包

通过使用原始套接字支持其他协议。

WSK 应用程序指定一种协议时，它调用[ **WskSocket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_socket)函数或[ **WskSocketConnect** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_socket_connect)函数来创建新的套接字。

WSK 应用程序还指定了一种协议 (作为*级别*参数) 时调用[ **WskControlSocket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_control_socket)函数来设置或检索传输协议级别或网络协议级别的套接字选项。

### <a name="combinations"></a>组合

IPv6 支持以下的套接字类型和协议组合的每个 WSK[套接字类别](https://docs.microsoft.com/windows-hardware/drivers/network/winsock-kernel-socket-categories):

基本套接字热歌劲\_流 + IPPROTO\_TCP 热歌劲\_DGRAM + IPPROTO\_UDP 热歌劲\_RAW + IPPROTO\_*Xxx*侦听套接字热歌劲\_流 + IPPROTO\_TCP

数据报套接字热歌劲\_DGRAM + IPPROTO\_UDP 热歌劲\_RAW + IPPROTO\_*Xxx*面向连接的套接字热歌劲\_流 + IPPROTO\_TCP

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>在 Windows Vista 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ws2def.h （包括 Wsk.h）</td>
</tr>
</tbody>
</table>

 

 




