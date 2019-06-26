---
title: 网络 INF 文件中的 Winsock 节
description: 网络 INF 文件中的 Winsock 节
ms.assetid: 179a8570-287b-446e-8b56-a9f23071e84d
keywords:
- INF 文件 WDK 网络，Winsock 部分
- 可使用网络 INF 文件 WDK、 Winsock 部分
- Winsock 部分 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ee02e73cca6844a1204d1c4f8d2cc271a666047
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368435"
---
# <a name="winsock-sections-in-a-network-inf-file"></a>网络 INF 文件中的 Winsock 节




用于的 INF 文件**NetTrans**提供 Winsock 接口的组件必须指定此 Winsock 依赖项。 此类的 INF 文件必须包含*Winsock 安装*部分。 若要创建 Winsockinstall 部分，添加。Winsock 扩展*DDInstall*协议的节名称。 例如，如果*DDInstall*部分的名为一种协议**Ipx**，则*Winsock 安装*部分为该协议必须命名为 Ipx.Winsock。

> [!NOTE] 
> 在 Windows 8 和更高版本已弃用 Winsock 依赖关系。


一个*Winsock 安装*部分必须包含**AddSock**指令。 **AddSock**指令指定了一个包含要添加到组件的值的供应商名为节**HKEY\_本地\_机\\系统\\CurrentControlSet\\Services\\*TransportDriverName*\\Params\\Winsock**密钥。

引用的供应商名为部分**AddSock**指令必须包含所需的以下值：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">值名称</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>TransportService</p></td>
<td align="left"><p>REG_SZ 值，该值指定协议的服务名称。 这必须是与相同<strong>Ndi\Service</strong>协议的值。 有关详细信息，请参阅<a href="adding-service-related-values-to-the-ndi-key.md" data-raw-source="[Adding Service-Related Values to the Ndi Key](adding-service-related-values-to-the-ndi-key.md)">Adding Service-Related 值到 Ndi 密钥</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HelperDllName</p></td>
<td align="left"><p>REG_EXPAND_SZ 值，该值指定 Windows 套接字帮助程序 (WSH) 协议的 DLL 的路径。 有关详细信息，请参阅<a href="https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566260(v=vs.85)" data-raw-source="[WSH DLL Function Summary](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566260(v=vs.85))">WSH DLL 函数摘要</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MaxSockAddrLength</p></td>
<td align="left"><p>REG_DWORD 值，该值指定有效 SOCKADDR 的最大大小，以字节为单位，WSH DLL</p></td>
</tr>
<tr class="even">
<td align="left"><p>MinSockAddrLength</p></td>
<td align="left"><p>指定的最小有效 SOCKADDR 大小，以字节为单位，WSH DLL 的 REG_DWORD 值</p></td>
</tr>
</tbody>
</table>

 

如果一个可选**ProviderId**为指定的命名空间提供程序，还必须指定以下值：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">值名称</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ProviderId</p></td>
<td align="left"><p>REG_SZ 值，指定全局唯一标识符 (GUID) 标识命名空间提供程序。 GUID 用作命名空间提供程序的所有后续引用的键。 通过运行 uuidgen.exe 实用程序获取 GUID。 有关此实用工具的详细信息，请参阅 Microsoft Windows SDK。</p></td>
</tr>
<tr class="even">
<td align="left"><p>LibraryPath</p></td>
<td align="left"><p>REG_EXPAND_SZ 值，该值指定命名空间提供程序 DLL 的完整路径。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DisplayString</p></td>
<td align="left"><p>可本地化的字符串，指定命名空间提供程序用户界面中显示的名称。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SupportedNameSpace</p></td>
<td align="left"><p>REG_DWORD 值，该值指定命名空间提供程序支持的命名空间。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>一个可选的 REG_DWORD 值，指定命名空间提供程序的版本号。 如果未指定此值，默认值 (1) 用于的版本号。</p></td>
</tr>
</tbody>
</table>

 

以下命名空间值可以分配给 SupportedNameSpace 和 Winsock2.h 中定义：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">命名空间</th>
<th align="left">ReplTest1</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>NS_ALL</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>NS_SAP</p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>NS_NDS</p></td>
<td align="left"><p>2</p></td>
</tr>
<tr class="even">
<td align="left"><p>NS_PEER_BROWSE</p></td>
<td align="left"><p>3</p></td>
</tr>
<tr class="odd">
<td align="left"><p>NS_TCPIP_LOCAL</p></td>
<td align="left"><p>10</p></td>
</tr>
<tr class="even">
<td align="left"><p>NS_TCPIP_HOSTS</p></td>
<td align="left"><p>11</p></td>
</tr>
<tr class="odd">
<td align="left"><p>NS_DNS</p></td>
<td align="left"><p>12</p></td>
</tr>
<tr class="even">
<td align="left"><p>NS_NETBT</p></td>
<td align="left"><p>13</p></td>
</tr>
<tr class="odd">
<td align="left"><p>NS_WINS</p></td>
<td align="left"><p>14</p></td>
</tr>
<tr class="even">
<td align="left"><p>NS_NBP</p></td>
<td align="left"><p>20</p></td>
</tr>
<tr class="odd">
<td align="left"><p>NS_MS</p></td>
<td align="left"><p>30</p></td>
</tr>
<tr class="even">
<td align="left"><p>NS_STDA</p></td>
<td align="left"><p>31</p></td>
</tr>
<tr class="odd">
<td align="left"><p>NS_CAIRO</p></td>
<td align="left"><p>32</p></td>
</tr>
<tr class="even">
<td align="left"><p>NS_X500</p></td>
<td align="left"><p>40</p></td>
</tr>
<tr class="odd">
<td align="left"><p>NS_NIS</p></td>
<td align="left"><p>41</p></td>
</tr>
<tr class="even">
<td align="left"><p>NS_WRQ</p></td>
<td align="left"><p>50</p></td>
</tr>
</tbody>
</table>

 

有关命名空间提供程序的详细信息，请参阅 Windows SDK 文档。

下面的示例演示 IPX 协议的 Winsock 部分：

```INF
[Ipx.Winsock]
AddSock = Install.IpxWinsock
 
[Install.IpxWinsock]
TransportService = nwlinkipx
HelperDllName = "%%SystemRoot%%\System32\wshisn.dll"
MaxSockAddrLength = 0x10
MinSockAddrLength = 0xe
ProviderId = "GUID"
LibraryPath = "%SystemRoot%\\System32\\nwprovau.dll"
DisplayString = %NwlnkIpx_Desc%
SupportedNameSpace = 1
Version = 2
```

INF 文件可以通过包括删除的一种协议的 Winsock 依赖项*Winsock 删除*部分。 若要创建*Winsock 删除*部分中，添加。Winsock 扩展*删除*协议的节名称。 例如，如果*删除*部分 Ipx.Remove，名为一种协议*Winsock 删除*协议必须命名为 Ipx.Remove.Winsock 部分。

*Winsock 删除*部分包含**DelSock**指令指定 INF 编写器名为的部分。 INF 编写器名为部分必须指定要删除的传输服务。 如果**ProviderId**以前注册的协议，还必须指定供应商名称部分**ProviderId**删除。

下面的示例显示了删除 IPX 协议的 Winsock 依赖关系的两个部分：

```INF
[Ipx.Remove.Winsock]
DelSock = Remove.IpxWinsock
 
[Remove.IpxWinsock]
TransportService = nwlinkipx
ProviderId = "GUID"
```

 

 





