---
title: 将数据包处理驱动程序和应用移植到 WFP
description: Windows 筛选平台 (WFP) 启用 TCP/IP 数据包筛选、检查和修改、连接监视或授权、IPsec 规则和处理以及 RPC 筛选。
ms.assetid: 9BB77BB8-1382-4F65-A4E8-80E229F43425
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: feb4f909da0ec94da20640fea7f5ee0bdb1c3221
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90103908"
---
# <a name="porting-packet-processing-drivers-and-apps-to-wfp"></a>将数据包处理驱动程序和应用移植到 WFP


Windows 筛选平台 (WFP) 启用 TCP/IP 数据包筛选、检查和修改、连接监视或授权、IPsec 规则和处理以及 RPC 筛选。 通常，你必须将 Windows XP 和 Windows Server 2003 中的 TCP/IP 筛选或连接监视组件转换为对 Windows Vista 和 Windows Server 2008 及更高版本使用 WFP 用户模式应用程序或服务、WFP 内核模式标注驱动程序或同时使用这两者。 下表列出了 Windows XP 和 Windows Server 2003 中的包处理的现有方法，以及如何在 Windows Vista 和 Windows Server 2008 及更高版本中将其更改为使用 WFP。

**注意**   在 Windows 8 中，传输驱动程序接口 (TDI) 功能和分层服务提供程序 (Lsp) 功能已弃用。

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Windows X) Windows Server 2003 中的现有方法</th>
<th align="left">Windows Vista 和 Windows Server 2008 及更高版本中的新方法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">用于简单数据包筛选的防火墙挂钩或筛选器挂钩驱动程序。</td>
<td align="left">使用 <a href="/windows/desktop/FWP/windows-filtering-platform-start-page" data-raw-source="[WFP Win32 API](/windows/desktop/FWP/windows-filtering-platform-start-page)">WFP Win32 API</a>的用户模式应用程序或服务。</td>
</tr>
<tr class="even">
<td align="left">用于进行深层数据包检查或修改的防火墙挂钩或筛选器挂钩驱动程序。</td>
<td align="left">IP 层、传输层或应用程序层强制 (ALE) 层标注驱动程序和使用 <a href="/windows/desktop/FWP/windows-filtering-platform-start-page" data-raw-source="[WFP Win32 API](/windows/desktop/FWP/windows-filtering-platform-start-page)">WFP Win32 API</a>的可选用户模式应用程序或服务。</td>
</tr>
<tr class="odd">
<td align="left">传输驱动程序接口 (TDI) 筛选器驱动程序用于简单数据包筛选。</td>
<td align="left">使用 <a href="/windows/desktop/FWP/windows-filtering-platform-start-page" data-raw-source="[WFP Win32 API](/windows/desktop/FWP/windows-filtering-platform-start-page)">WFP Win32 API</a>的用户模式应用程序或服务。</td>
</tr>
<tr class="even">
<td align="left">用于深层数据包或流检查或修改的 TDI 筛选器驱动程序。</td>
<td align="left"><p>传输层、流层和/或 ALE 标注驱动程序以及使用 WFP 的可选用户模式应用程序或服务 <a href="/windows/desktop/FWP/windows-filtering-platform-start-page" data-raw-source="[WFP Win32 API](/windows/desktop/FWP/windows-filtering-platform-start-page)">Win32 API</a></p></td>
</tr>
<tr class="odd">
<td align="left">用于 TCP 连接或用户数据报协议 (UDP) 流量管理的 TDI 筛选器驱动程序。</td>
<td align="left"><p>对于 TCP 连接管理： ALE 标注驱动程序和使用 <a href="/windows/desktop/FWP/windows-filtering-platform-start-page" data-raw-source="[WFP Win32 API](/windows/desktop/FWP/windows-filtering-platform-start-page)">WFP Win32 API</a>的可选用户模式应用程序或服务。</p>
<p>对于 TCP 代理：</p>
<ul>
<li>在 Windows Vista 中：数据包修改标注驱动程序。</li>
<li>在 Windows 7 和更高版本中： ALE_REDIRECT 层标注驱动程序。</li>
</ul>
<p>对于 MAC 级别的筛选：</p>
<ul>
<li>在 Windows 8 和更高版本中： MAC_FRAME 层标注驱动程序。</li>
<li>在 Windows Vista 和 Windows 7 中： NDIS 轻型筛选器驱动程序。</li>
</ul>
<p>对于 UDP 流量管理：流或数据报数据层标注驱动程序以及使用 <a href="/windows/desktop/FWP/windows-filtering-platform-start-page" data-raw-source="[WFP Win32 API](/windows/desktop/FWP/windows-filtering-platform-start-page)">WFP Win32 API</a>的可选用户模式应用程序或服务。</p></td>
</tr>
<tr class="even">
<td align="left">用于简单数据包筛选的 Windows 套接字 LSP。</td>
<td align="left">使用 <a href="/windows/desktop/FWP/windows-filtering-platform-start-page" data-raw-source="[WFP Win32 API](/windows/desktop/FWP/windows-filtering-platform-start-page)">WFP Win32 API</a>的用户模式应用程序或服务。</td>
</tr>
<tr class="odd">
<td align="left">用于进行深层数据包检查或修改的 Windows 套接字 LSP。</td>
<td align="left"><p>IP 层、ALE、传输 (（例如数据报数据) ）或流层标注驱动程序和使用 <a href="/windows/desktop/FWP/windows-filtering-platform-start-page" data-raw-source="[WFP Win32 API](/windows/desktop/FWP/windows-filtering-platform-start-page)">WFP Win32 API</a>的可选用户模式应用程序或服务。</p></td>
</tr>
<tr class="even">
<td align="left">网络设备接口规范 (NDIS) 用于简单数据包筛选的中间驱动程序。</td>
<td align="left"><p>对于基于 IP 的筛选：使用 <a href="/windows/desktop/FWP/windows-filtering-platform-start-page" data-raw-source="[WFP Win32 API](/windows/desktop/FWP/windows-filtering-platform-start-page)">WFP Win32 API</a>的用户模式应用程序或服务。</p>
<p>对于基于 MAC 的筛选：</p>
<ul>
<li>在 Windows 8 和更高版本中： MAC_FRAME 层标注驱动程序。</li>
<li>在 Windows Vista 和 Windows 7 中： NDIS 轻型筛选器驱动程序。</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left">用于 TCP 连接或 UDP 流量管理的 NDIS 中间驱动程序。</td>
<td align="left"><p>TCP 连接管理： ALE 标注驱动程序和使用 <a href="/windows/desktop/FWP/windows-filtering-platform-start-page" data-raw-source="[WFP Win32 API](/windows/desktop/FWP/windows-filtering-platform-start-page)">WFP Win32 API</a>的可选用户模式应用程序或服务。</p>
<p>UDP 流量管理： ALE 或传输层标注驱动程序以及使用 <a href="/windows/desktop/FWP/windows-filtering-platform-start-page" data-raw-source="[WFP Win32 API](/windows/desktop/FWP/windows-filtering-platform-start-page)">WFP Win32 API</a>的可选用户模式应用程序或服务。</p></td>
</tr>
<tr class="even">
<td align="left">用于执行 (MAC) 级筛选的媒体访问控制的 NDIS 轻型筛选器驱动程序。</td>
<td align="left"><p>在 Windows 8 和更高版本中： MAC_FRAME 层标注驱动程序。</p>
<p>在 Windows Vista 和 Windows 7 中： NDIS 轻型筛选器驱动程序。</p></td>
</tr>
</tbody>
</table>

 

