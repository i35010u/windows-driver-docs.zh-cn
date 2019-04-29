---
title: AF_INET
description: AF_INET
ms.assetid: 59e12f8d-02eb-413c-bc04-6b9b6e4adde6
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 AF_INET 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5319fe56d72f314708725bc16952a78e11ada74d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367752"
---
# <a name="afinet"></a>AF\_INET


AF\_INET 地址系列是 IPv4 地址族。

### <a name="socket-address-structure"></a>套接字地址结构

使用指定的 IPv4 传输地址[ **SOCKADDR\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff570823)结构。

### <a name="socket-types"></a>套接字类型

IPv4 支持以下的套接字类型：

<a href="" id="sock-stream"></a>热歌劲\_流  
支持可靠的面向连接的字节流进行通信。

<a href="" id="sock-dgram"></a>热歌劲\_DGRAM  
支持不可靠的无连接数据报进行通信。

<a href="" id="sock-raw"></a>热歌劲\_RAW  
支持的传输协议对原始访问。

WSK 应用程序指定套接字类型时，它调用[ **WskSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571149)函数或[ **WskSocketConnect** ](https://msdn.microsoft.com/library/windows/hardware/ff571150)函数来创建新的套接字。

### <a name="protocols"></a>协议

以下 IPv4 IPPROTO\_*XXX* WSK 标头文件中定义协议 IPPROTO 枚举值：

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

WSK 应用程序指定一种协议时，它调用[ **WskSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571149)函数或[ **WskSocketConnect** ](https://msdn.microsoft.com/library/windows/hardware/ff571150)函数来创建新的套接字。

WSK 应用程序还指定了一种协议 (作为*级别*参数) 时调用[ **WskControlSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571127)函数来设置或检索传输协议级别或网络协议级别的套接字选项。

### <a name="combinations"></a>组合

IPv4 支持以下的套接字类型和协议组合的每个 WSK[套接字类别](https://msdn.microsoft.com/library/windows/hardware/ff571093):

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

 

 




