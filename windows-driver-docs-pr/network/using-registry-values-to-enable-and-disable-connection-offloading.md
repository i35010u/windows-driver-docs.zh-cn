---
title: 使用注册表值启用和禁用连接卸载
description: 使用注册表值启用和禁用连接卸载
keywords:
- 连接卸载 WDK TCP/IP 传输，注册表值
- 注册表 WDK TCP/IP 卸载
- 连接卸载 WDK TCP/IP 传输，启用服务
- 连接卸载 WDK TCP/IP 传输，禁用服务
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec73d3a7059117886a48c3b9165ad6058b09c374
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806123"
---
# <a name="using-registry-values-to-enable-and-disable-connection-offloading"></a>使用注册表值启用和禁用连接卸载





调试驱动程序的连接卸载功能时，您可能会发现使用注册表项设置启用或禁用连接卸载服务很有用。 你可以在 INF 文件和注册表中定义标准化关键字。 有关标准化关键字的详细信息，请参阅 [网络设备的标准化 INF 关键字](standardized-inf-keywords-for-network-devices.md)。

连接卸载关键字定义如下：

<a href="" id="-tcpconnectionoffloadipv4"></a>**\*TCPConnectionOffloadIPv4**  
描述设备是启用还是禁用了通过 IPv4 卸载 TCP 连接。

<a href="" id="-tcpconnectionoffloadipv6"></a>**\*TCPConnectionOffloadIPv6**  
描述设备是启用还是禁用了通过 IPv6 卸载 TCP 连接。

下表描述了可用于配置卸载服务的分组关键字。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">SubkeyName</th>
<th align="left">ParamDesc</th>
<th align="left">“值”</th>
<th align="left">EnumDesc</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em>TCPConnectionOffloadIPv4</strong></p></td>
<td align="left"><p>TCP 连接卸载 (IPv4) </p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>已禁用</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (默认值) </p></td>
<td align="left"><p>已启用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>TCPConnectionOffloadIPv6</strong></p></td>
<td align="left"><p> (IPv6) 的 TCP 连接卸载</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>已禁用</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (默认值) </p></td>
<td align="left"><p>已启用</p></td>
</tr>
</tbody>
</table>

 

 

 





