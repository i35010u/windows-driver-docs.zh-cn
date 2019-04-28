---
title: 将数据包处理驱动程序和应用移植到 WFP
description: Windows 筛选平台 (WFP) 启用 TCP/IP 数据包筛选、 检查和修改、 连接监视或授权，IPsec 规则和处理和 RPC 筛选。
ms.assetid: 9BB77BB8-1382-4F65-A4E8-80E229F43425
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 457f1a5bfbfb09344ff7996d10f3b68c43402b41
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342976"
---
# <a name="porting-packet-processing-drivers-and-apps-to-wfp"></a>将数据包处理驱动程序和应用移植到 WFP


Windows 筛选平台 (WFP) 启用 TCP/IP 数据包筛选、 检查和修改、 连接监视或授权，IPsec 规则和处理和 RPC 筛选。 通常情况下，您必须将 TCP/IP 筛选或转换的连接监视组件在 Windows XP 和 Windows Server 2003 使用 WFP 用户模式应用程序或服务、 WFP 内核模式标注驱动程序，或同时适用于 Windows Vista 和 Windows Server 2008 及更高版本。 下表列出了用于处理在 Windows XP 和 Windows Server 2003 以及如何必须更改其在 Windows Vista 和 Windows Server 2008 和更高版本使用 WFP 的数据包的现有方法。

**请注意**  截至 Windows 8，传输驱动程序接口 (TDI) 功能和分层服务提供商 (Lsp) 功能已弃用。

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Windows XPand Windows Server 2003 中的现有方法</th>
<th align="left">在 Windows Vista 和 Windows Server 2008 和更高版本中的新方法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">防火墙钩或筛选器将挂钩适用于简单的数据包筛选驱动程序。</td>
<td align="left">用户模式应用程序或服务，它使用<a href="https://msdn.microsoft.com/library/windows/desktop/aa366510" data-raw-source="[WFP Win32 API](https://msdn.microsoft.com/library/windows/desktop/aa366510)">WFP Win32 API</a>。</td>
</tr>
<tr class="even">
<td align="left">防火墙钩或筛选器将挂钩深度数据包检查或修改驱动程序。</td>
<td align="left">IP 层、 传输层或应用程序层强制 (ALE) 层标注驱动程序和可选的用户模式应用程序或服务，它使用<a href="https://msdn.microsoft.com/library/windows/desktop/aa366510" data-raw-source="[WFP Win32 API](https://msdn.microsoft.com/library/windows/desktop/aa366510)">WFP Win32 API</a>。</td>
</tr>
<tr class="odd">
<td align="left">传输驱动程序接口 (TDI) 筛选器驱动程序进行简单的数据包筛选。</td>
<td align="left">用户模式应用程序或服务，它使用<a href="https://msdn.microsoft.com/library/windows/desktop/aa366510" data-raw-source="[WFP Win32 API](https://msdn.microsoft.com/library/windows/desktop/aa366510)">WFP Win32 API</a>。</td>
</tr>
<tr class="even">
<td align="left">有关深入的数据包或流检查或修改 TDI 筛选器驱动程序。</td>
<td align="left"><p>传输层、 Stream 层和/或 ALE 标注驱动程序和可选的用户模式应用程序或服务，它使用<a href="https://msdn.microsoft.com/library/windows/desktop/aa366510" data-raw-source="[WFP Win32 API](https://msdn.microsoft.com/library/windows/desktop/aa366510)">WFP Win32 API</a></p></td>
</tr>
<tr class="odd">
<td align="left">为 TCP 连接或用户数据报协议 (UDP) 流量管理 TDI 筛选器驱动程序。</td>
<td align="left"><p>用于 TCP 连接管理：ALE 标注驱动程序和可选的用户模式应用程序或服务，它使用<a href="https://msdn.microsoft.com/library/windows/desktop/aa366510" data-raw-source="[WFP Win32 API](https://msdn.microsoft.com/library/windows/desktop/aa366510)">WFP Win32 API</a>。</p>
<p>对于 TCP 代理：</p>
<ul>
<li>在 Windows Vista 中：数据包修改标注驱动程序。</li>
<li>在 Windows 7 及更高版本：ALE_REDIRECT 层标注驱动程序。</li>
</ul>
<p>为 MAC 级别的筛选：</p>
<ul>
<li>在 Windows 8 和更高版本：MAC_FRAME 层标注驱动程序。</li>
<li>在 Windows Vista 和 Windows 7:NDIS 轻型筛选器驱动程序。</li>
</ul>
<p>对于 UDP 流量管理：Stream 或数据报数据层标注驱动程序和可选的用户模式应用程序或服务，它使用<a href="https://msdn.microsoft.com/library/windows/desktop/aa366510" data-raw-source="[WFP Win32 API](https://msdn.microsoft.com/library/windows/desktop/aa366510)">WFP Win32 API</a>。</p></td>
</tr>
<tr class="even">
<td align="left">Windows 套接字 LSP 进行简单的数据包筛选。</td>
<td align="left">用户模式应用程序或服务，它使用<a href="https://msdn.microsoft.com/library/windows/desktop/aa366510" data-raw-source="[WFP Win32 API](https://msdn.microsoft.com/library/windows/desktop/aa366510)">WFP Win32 API</a>。</td>
</tr>
<tr class="odd">
<td align="left">Windows 套接字 LSP 深度数据包检查或修改。</td>
<td align="left"><p>IP 层，ALE、 传输协议 （如数据报数据），或 Stream 层标注驱动程序和可选的用户模式应用程序或服务，它使用<a href="https://msdn.microsoft.com/library/windows/desktop/aa366510" data-raw-source="[WFP Win32 API](https://msdn.microsoft.com/library/windows/desktop/aa366510)">WFP Win32 API</a>。</p></td>
</tr>
<tr class="even">
<td align="left">网络设备接口规范 (NDIS) 中间层进行简单的数据包筛选驱动程序。</td>
<td align="left"><p>为基于 IP 的筛选：用户模式应用程序或服务，它使用<a href="https://msdn.microsoft.com/library/windows/desktop/aa366510" data-raw-source="[WFP Win32 API](https://msdn.microsoft.com/library/windows/desktop/aa366510)">WFP Win32 API</a>。</p>
<p>为基于 MAC 的筛选：</p>
<ul>
<li>在 Windows 8 和更高版本：MAC_FRAME 层标注驱动程序。</li>
<li>在 Windows Vista 和 Windows 7:NDIS 轻型筛选器驱动程序。</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left">为 TCP 连接或 UDP 流量管理的 NDIS 中间驱动程序。</td>
<td align="left"><p>TCP 连接管理：ALE 标注驱动程序和可选的用户模式应用程序或服务，它使用<a href="https://msdn.microsoft.com/library/windows/desktop/aa366510" data-raw-source="[WFP Win32 API](https://msdn.microsoft.com/library/windows/desktop/aa366510)">WFP Win32 API</a>。</p>
<p>UDP 流量管理：ALE 或传输层标注驱动程序和可选的用户模式应用程序或服务，它使用<a href="https://msdn.microsoft.com/library/windows/desktop/aa366510" data-raw-source="[WFP Win32 API](https://msdn.microsoft.com/library/windows/desktop/aa366510)">WFP Win32 API</a>。</p></td>
</tr>
<tr class="even">
<td align="left">NDIS 轻型筛选器驱动程序来执行媒体访问控制 (MAC) 的级别筛选。</td>
<td align="left"><p>在 Windows 8 和更高版本：MAC_FRAME 层标注驱动程序。</p>
<p>在 Windows Vista 和 Windows 7:NDIS 轻型筛选器驱动程序。</p></td>
</tr>
</tbody>
</table>

 

 

 





