---
title: 指定绑定接口
description: 指定绑定接口
ms.assetid: 49ef3eae-88e6-4424-8c3b-19e8c3bb734f
keywords:
- 添加注册表部分 WDK 网络绑定接口
- 绑定接口 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b91c63325aaa4d929b277ef2871fa4f6c9d2085
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342582"
---
# <a name="specifying-binding-interfaces"></a>指定绑定接口





对于每个网络组件的安装，网络 INF 文件必须通过添加指定组件的上限和下限绑定接口**接口**关键**Ndi**密钥。

**接口**键具有至少两个值：

<a href="" id="upperrange"></a>**UpperRange**  
REG\_SZ 值，用于定义该组件可以将绑定到在其上边缘的接口。

<a href="" id="lowerrange"></a>**LowerRange**  
REG\_SZ 值，用于定义该组件可以将绑定到在其下边缘的接口。 对于物理适配器，此接口应始终为网络媒体，如以太网适配器连接。

**请注意**   **DefUpper**并**DefLower**值在 Windows 95/98/我网络 INF 文件，但是，不支持将 Windows 2000 及更高版本使用的 INF 文件操作系统的版本。

 

下表列出了 Microsoft 提供**UpperRange**值：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ReplTest1</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>netbios</p></td>
<td align="left"><p>NetBIOS</p></td>
</tr>
<tr class="even">
<td align="left"><p>ipx</p></td>
<td align="left"><p>IPX</p></td>
</tr>
<tr class="odd">
<td align="left"><p>tdi</p></td>
<td align="left"><p>为 TCP/IP TDI 接口</p></td>
</tr>
<tr class="even">
<td align="left"><p>ndis5</p></td>
<td align="left"><p>NDIS 5.x （应不再使用 ndis2、 ndis3 和 ndis4）。 应为任何非 ATM 网络组件，请使用 NDIS 接口在其上边缘的非 ATM 适配器，如指定此值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Ndisatm</p></td>
<td align="left"><p>NDIS 5.x ATM 支持。 任何 ATM 网络组件，如 ATM 适配器，使用 NDIS 其上边缘接口的指定的值</p></td>
</tr>
<tr class="even">
<td align="left"><p>ndiswan</p></td>
<td align="left"><p>WAN 适配器的上边缘。 如果指定，此值会导致操作系统来自动启用与 RAS 一起使用的 WAN 适配器</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Ndiscowan</p></td>
<td align="left"><p>对于面向连接的 NDIS 运行通过 WAN 适配器的上边缘</p></td>
</tr>
<tr class="even">
<td align="left"><p>noupper</p></td>
<td align="left"><p>对于任何组件都不会公开绑定; 的上边缘的上边缘此类组件通常具有在其上边缘的专用接口</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Winsock</p></td>
<td align="left"><p>Windows 套接字接口</p></td>
</tr>
<tr class="even">
<td align="left"><p>ndis5_atalk</p></td>
<td align="left"><p>上边缘为 NDIS 5.x Net 组件 （适配器），它将仅向在其上边缘 AppleTalk 接口绑定</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ndis5_dlc</p></td>
<td align="left"><p>为 NDIS 5.x Net 组件 （适配器） 将绑定到在其上边缘的 DLC 接口仅的上边缘</p></td>
</tr>
<tr class="even">
<td align="left"><p>ndis5_ip</p></td>
<td align="left"><p>为 NDIS 5.x Net 组件 （适配器） 将绑定到在其上边缘的 TCP/IP 接口仅的上边缘</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ndis5_ipx</p></td>
<td align="left"><p>为 NDIS 5.x Net 组件 （适配器） 将绑定到在其上边缘的 IPX 接口仅的上边缘</p></td>
</tr>
<tr class="even">
<td align="left"><p>ndis5_nbf</p></td>
<td align="left"><p>为 NDIS 5.x Net 组件 （适配器） 将绑定到在其上边缘的 NetBEUI 接口仅的上边缘</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ndis5_streams</p></td>
<td align="left"><p>为 NDIS 5.x Net 组件 （适配器） 将绑定到在其上边缘的流接口仅的上边缘。 此值是适用于 Windows XP 和更高版本的操作系统已过时。</p></td>
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

 

下表列出了 Microsoft 提供**LowerRange**值：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ReplTest1</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>以太网</p></td>
<td align="left"><p>下边缘的以太网适配器</p></td>
</tr>
<tr class="even">
<td align="left"><p>atm</p></td>
<td align="left"><p>下边缘的 ATM 适配器</p></td>
</tr>
<tr class="odd">
<td align="left"><p>令牌环</p></td>
<td align="left"><p>令牌环适配器的下边缘</p></td>
</tr>
<tr class="even">
<td align="left"><p>串行</p></td>
<td align="left"><p>串行适配器的下边缘</p></td>
</tr>
<tr class="odd">
<td align="left"><p>fddi</p></td>
<td align="left"><p>FDDI 适配器的下边缘</p></td>
</tr>
<tr class="even">
<td align="left"><p>基带</p></td>
<td align="left"><p>基带适配器的下边缘</p></td>
</tr>
<tr class="odd">
<td align="left"><p>宽带</p></td>
<td align="left"><p>宽带适配器的下边缘</p></td>
</tr>
<tr class="even">
<td align="left"><p>蓝牙</p></td>
<td align="left"><p>Bluetooth 适配器的下边缘</p></td>
</tr>
<tr class="odd">
<td align="left"><p>arcnet</p></td>
<td align="left"><p>下边缘的 Arcnet 适配器</p></td>
</tr>
<tr class="even">
<td align="left"><p>isdn</p></td>
<td align="left"><p>ISDN 适配器的下边缘</p></td>
</tr>
<tr class="odd">
<td align="left"><p>localtalk</p></td>
<td align="left"><p>LocalTalk 适配器的下边缘</p></td>
</tr>
<tr class="even">
<td align="left"><p>wan</p></td>
<td align="left"><p>下边缘的 WAN 适配器</p></td>
</tr>
<tr class="odd">
<td align="left"><p>nolower</p></td>
<td align="left"><p>对于任何组件都不会公开绑定下边缘的下边缘</p></td>
</tr>
<tr class="even">
<td align="left"><p>ndis5</p></td>
<td align="left"><p>NDIS 5.x。 （ndis2、 ndis3 和 ndis4 应不再使用。）对于其下边缘与非 ATM 组件接口 NDIS 通过任何网络组件</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Ndisatm</p></td>
<td align="left"><p>Ndis 5.x ATM 支持。 对于其下边缘与 ATM 组件接口 NDIS 通过任何网络组件</p></td>
</tr>
<tr class="even">
<td align="left"><p>wlan</p></td>
<td align="left"><p>本机 802.11 无线 LAN 适配器的下边缘。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ppip</p></td>
<td align="left"><p>移动宽带 (MB) 适配器的下边缘</p></td>
</tr>
<tr class="even">
<td align="left"><p>vwifi</p></td>
<td align="left"><p>虚拟 wifi 接口的的下边缘</p></td>
</tr>
</tbody>
</table>

 

**UpperRange**并**LowerRange**值组件可以绑定到指定类型的接口-不包含实际组件。 绑定引擎将网络组件绑定到提供适当的 （上限或下限） 边缘处的指定的接口的所有组件。 例如，一个协议**LowerRange** ndis5 的将绑定到具有的所有组件**UpperRange**的 ndis5，例如物理或虚拟适配器。

如果一个 NDIS 5.x Net 组件 （适配器） 仅适用于一个或多个特定的协议，则其**UpperRange**应分配一个或多个特定于协议的值，如 ndis5\_atalk，ndis5\_dlc，ndis5\_ip，ndis5\_ipx，ndis5\_nbf、 或 ndis5\_流。 此类 net 类组件不应将分配**UpperRange**值的 ndis5，因为这将导致该组件将绑定到所有的协议提供 ndis5 降低边缘。

有 INF 文件作者可以定义并使用特定于供应商**UpperRange**并**LowerRange**专用绑定接口的值。 例如，如果供应商想要其适配器只能绑定到其自己的专有协议驱动程序，可以指定 INF 文件 writer **XXX**有关**UpperRange**的适配器和**XXX**有关**LowerRange**的专有协议。 Windows 2000 绑定引擎会将绑定具有的所有组件**UpperRange**的**XXX** （在此情况下，适配器） 具有的所有组件**LowerRange**的**XXX** （在本例中为专有协议）。

以下是一种*添加注册表部分*，它将**UpperRange**并**LowerRange** ATM 适配器的值：

```INF
[addreg-section]
HKR, Ndi\Interfaces, UpperRange, 0, "ndisATM"
HKR, Ndi\Interfaces, LowerRange, 0, "atm"
```

 

 





