---
title: 指定绑定接口
description: 指定绑定接口
keywords:
- 添加-注册表-WDK 网络，绑定接口
- 绑定接口 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7aa08e4324d8f3c186eedc9c7a33356aaea36322
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790443"
---
# <a name="specifying-binding-interfaces"></a>指定绑定接口





对于它安装的每个网络组件，网络 INF 文件都必须通过将 **接口** 键添加到 **Ndi** 项来指定组件的上限和下限接口。

**接口** 键至少有两个值：

<a href="" id="upperrange"></a>**UpperRange**  
一个 REG \_ SZ 值，它定义组件可在其上边缘绑定到的接口。

<a href="" id="lowerrange"></a>**LowerRange**  
一个 REG \_ SZ 值，它定义组件可在其下边缘绑定到的接口。 对于物理适配器，此接口应始终是适配器连接到的网络媒体（如以太网）。

**注意**  但是，在 windows 2000 和更高版本的操作系统上将使用 Windows 95/98/Me 网络 INF 文件中的 **DefUpper** 和 **DefLower** 值。

 

下表列出了 Microsoft 提供的 **UpperRange** 值：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">“值”</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>netbios</p></td>
<td align="left"><p>NetBIOS</p></td>
</tr>
<tr class="even">
<td align="left"><p>路由器</p></td>
<td align="left"><p>路由器</p></td>
</tr>
<tr class="odd">
<td align="left"><p>tdi</p></td>
<td align="left"><p>TCP/IP 的 TDI 接口</p></td>
</tr>
<tr class="even">
<td align="left"><p>ndis5</p></td>
<td align="left"><p>不应再) 使用 NDIS 1.x (ndis2、ndis3 和 ndis4。 应为任何非 atm 网络组件（例如非 ATM 适配器）指定此值，其上边缘都具有 NDIS 接口。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Ndisatm</p></td>
<td align="left"><p>支持 ATM 的 NDIS 1.x。 为任意 ATM 网络组件指定的值（例如 ATM 适配器），其上边缘接口与 NDIS</p></td>
</tr>
<tr class="even">
<td align="left"><p>ndiswan</p></td>
<td align="left"><p>WAN 适配器的上边缘。 如果指定此值，则会导致操作系统自动启用 WAN 适配器以便与 RAS 一起使用</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Ndiscowan</p></td>
<td align="left"><p>面向连接的 NDIS 在其上运行的 WAN 适配器的上部边缘</p></td>
</tr>
<tr class="even">
<td align="left"><p>noupper</p></td>
<td align="left"><p>没有公开用于绑定的上部边缘的任何组件的上边缘;此类组件的上部边缘通常有一个专用接口</p></td>
</tr>
<tr class="odd">
<td align="left"><p>winsock</p></td>
<td align="left"><p>Windows 套接字接口</p></td>
</tr>
<tr class="even">
<td align="left"><p>ndis5_atalk</p></td>
<td align="left"><p>NDIS 1.x 网络组件的上部边缘 (仅绑定到其上边缘的 AppleTalk 接口的适配器) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>ndis5_dlc</p></td>
<td align="left"><p>NDIS 1.x 网络组件的上部边缘 (适配器) 仅绑定到其上边缘的 DLC 接口</p></td>
</tr>
<tr class="even">
<td align="left"><p>ndis5_ip</p></td>
<td align="left"><p>NDIS 1.x 网络组件的上部边缘 (仅绑定到其上边缘 TCP/IP 接口的适配器) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>ndis5_ipx</p></td>
<td align="left"><p>NDIS 1.x 网络组件的上部边缘 (适配器) 仅绑定到其上边缘的 IPX 接口</p></td>
</tr>
<tr class="even">
<td align="left"><p>ndis5_nbf</p></td>
<td align="left"><p>NDIS 1.x 网络组件的上部边缘 (适配器) 仅绑定到其上边缘的 NetBEUI 接口</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ndis5_streams</p></td>
<td align="left"><p>NDIS 1.x 网络组件的上部边缘 (适配器) 仅绑定到其上边缘的流接口。 对于 Windows XP 和更高版本的操作系统，此值已过时。</p></td>
</tr>
<tr class="even">
<td align="left"><p>flpp4</p></td>
<td align="left"><p>支持 IPv4 的移动宽带 (MB) 设备。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>flpp6</p></td>
<td align="left"><p>支持 IPv6 的移动宽带 (MB) 设备。</p></td>
</tr>
</tbody>
</table>

 

下表列出了 Microsoft 提供的 **LowerRange** 值：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">“值”</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>网</p></td>
<td align="left"><p>以太网适配器的下边缘</p></td>
</tr>
<tr class="even">
<td align="left"><p>atm</p></td>
<td align="left"><p>ATM 适配器的下边缘</p></td>
</tr>
<tr class="odd">
<td align="left"><p>tokenring</p></td>
<td align="left"><p>令牌环适配器的下边缘</p></td>
</tr>
<tr class="even">
<td align="left"><p>serial</p></td>
<td align="left"><p>串行适配器的下边缘</p></td>
</tr>
<tr class="odd">
<td align="left"><p>fddi</p></td>
<td align="left"><p>FDDI 适配器的下边缘</p></td>
</tr>
<tr class="even">
<td align="left"><p>局域网</p></td>
<td align="left"><p>基带适配器的下边缘</p></td>
</tr>
<tr class="odd">
<td align="left"><p>宽带</p></td>
<td align="left"><p>宽带适配器的下边缘</p></td>
</tr>
<tr class="even">
<td align="left"><p>蓝牙</p></td>
<td align="left"><p>蓝牙适配器的下边缘</p></td>
</tr>
<tr class="odd">
<td align="left"><p>arcnet</p></td>
<td align="left"><p>Arcnet 适配器的下边缘</p></td>
</tr>
<tr class="even">
<td align="left"><p>专线</p></td>
<td align="left"><p>ISDN 适配器的下边缘</p></td>
</tr>
<tr class="odd">
<td align="left"><p>localtalk</p></td>
<td align="left"><p>LocalTalk 适配器的下边缘</p></td>
</tr>
<tr class="even">
<td align="left"><p>wan</p></td>
<td align="left"><p>WAN 适配器的下边缘</p></td>
</tr>
<tr class="odd">
<td align="left"><p>nolower</p></td>
<td align="left"><p>未公开绑定的下边缘的任何组件的下边缘</p></td>
</tr>
<tr class="even">
<td align="left"><p>ndis5</p></td>
<td align="left"><p>NDIS 1.x。 不应再使用 (ndis2、ndis3 和 ndis4。对于其下边缘接口通过使用非 ATM 组件的 NDIS 的任何网络组件 ) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>Ndisatm</p></td>
<td align="left"><p>支持 ATM 的 Ndis 1.x。 对于其下边缘接口通过具有 ATM 组件的 NDIS 的任何网络组件</p></td>
</tr>
<tr class="even">
<td align="left"><p>局域网</p></td>
<td align="left"><p>本机802.11 无线 LAN 适配器的下边缘。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ppip</p></td>
<td align="left"><p>移动宽带 (MB) 适配器的下边缘</p></td>
</tr>
<tr class="even">
<td align="left"><p>vwifi</p></td>
<td align="left"><p>虚拟 wifi 接口的下边缘</p></td>
</tr>
</tbody>
</table>

 

**UpperRange** 和 **LowerRange** 值指定组件的类型（而不是组件可以绑定到的实际组件）。 绑定引擎将网络组件绑定到所有组件，这些组件在适当的 (大写或小写) 边缘提供指定接口。 例如， **LowerRange** 为 ndis5 的协议将绑定到具有 **UpperRange** of ndis5 的所有组件，如物理或虚拟适配器。

如果 (适配器) 的 NDIS 1.x 网络组件仅适用于一个或多个特定协议，则应为其 **UpperRange** 分配一个或多个特定于协议的值，例如 ndis5 \_ atalk、ndis5 \_ dlc、ndis5 \_ ip、ndis5 \_ ipx、ndis5 \_ nbf 或 ndis5 \_ 流。 不应为这种 net class 组件分配 **UpperRange** 值 ndis5，因为这会导致该组件绑定到提供 ndis5 下边缘的所有协议。

INF-文件编写器可以为专用绑定接口定义和使用特定于供应商的 **UpperRange** 和 **LowerRange** 值。 例如，如果某个供应商想要将其适配器仅绑定到其自己的专用协议驱动程序，则 INF-文件编写器可以为该适配器的 **UpperRange** 指定 **xxx** ，并为专用协议的 **LowerRange** 指定 **xxx** 。 Windows 2000 绑定引擎将绑定 **UpperRange** 为 **xxx** (的所有组件，在这种情况下，适配器) 包含 **LowerRange** 为 **xxx** (的所有组件（在这种情况下为专有协议) ）。

以下是添加 **UpperRange** 和 **LowerRange** 值的 "*添加注册表" 部分* 的示例：

```INF
[addreg-section]
HKR, Ndi\Interfaces, UpperRange, 0, "ndisATM"
HKR, Ndi\Interfaces, LowerRange, 0, "atm"
```

 

 





