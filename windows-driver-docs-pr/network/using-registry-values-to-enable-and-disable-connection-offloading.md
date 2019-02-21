---
title: 使用注册表值来启用和禁用连接卸载
description: 使用注册表值来启用和禁用连接卸载
ms.assetid: dd5d1e8a-0c6f-40d2-8a33-4d6fc70c17d5
keywords:
- 连接将卸载 WDK TCP/IP 传输，注册表值
- 注册表 WDK TCP/IP 卸载
- 连接将卸载 WDK TCP/IP 传输，启用服务
- 连接将卸载 WDK TCP/IP 传输，禁用服务
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e825b74a670a3931ffbfc11f37b8d8c5367ffe3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526323"
---
# <a name="using-registry-values-to-enable-and-disable-connection-offloading"></a>使用注册表值来启用和禁用连接卸载





在调试时驱动程序的连接将卸载功能，你可能会发现可以启用或禁用连接卸载服务使用注册表项设置。 没有你可以定义在 INF 文件和注册表中的标准化的关键字。 有关标准化关键字的详细信息，请参阅[为网络设备的标准化 INF 关键字](standardized-inf-keywords-for-network-devices.md)。

连接卸载关键字定义，如下所示：

<a href="" id="-tcpconnectionoffloadipv4"></a>**\*TCPConnectionOffloadIPv4**  
介绍设备是启用还是禁用 IPv4 上的 TCP 连接的卸载。

<a href="" id="-tcpconnectionoffloadipv6"></a>**\*TCPConnectionOffloadIPv6**  
介绍设备是启用还是禁用 IPv6 上的 TCP 连接的卸载。

下表介绍可用于配置卸载服务分组的关键字。

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
<th align="left">值</th>
<th align="left">EnumDesc</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em>TCPConnectionOffloadIPv4</strong></p></td>
<td align="left"><p>TCP 连接卸载 (IPv4)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 （默认值）</p></td>
<td align="left"><p>已启用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>TCPConnectionOffloadIPv6</strong></p></td>
<td align="left"><p>TCP 连接卸载 (IPv6)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 （默认值）</p></td>
<td align="left"><p>已启用</p></td>
</tr>
</tbody>
</table>

 

 

 





