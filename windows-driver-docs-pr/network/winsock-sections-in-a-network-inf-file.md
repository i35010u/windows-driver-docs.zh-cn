---
title: 网络 INF 文件中的 Winsock 节
description: 网络 INF 文件中的 Winsock 节
ms.assetid: 179a8570-287b-446e-8b56-a9f23071e84d
keywords:
- INF 文件 WDK 网络，Winsock 部分
- 网络 INF 文件 WDK，Winsock 部分
- Winsock 部分 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ed7d375c9f1d58e8c123242765ca855291812a8
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90107092"
---
# <a name="winsock-sections-in-a-network-inf-file"></a>网络 INF 文件中的 Winsock 节




提供 Winsock 接口的 **NetTrans** 组件的 INF 文件必须指定此 winsock 依赖项。 此类 INF 文件必须包含 *Winsock 安装* 部分。 若要创建 Winsockinstall 节，请添加。对协议的 *DDInstall* 节名称的 Winsock 扩展。 例如，如果某个协议的 *DDInstall* 部分命名为 **ipx**，则该协议的 *Winsock 安装* 部分必须命名为 "ipx"。

> [!NOTE] 
> Windows 8 及更高版本中已弃用 Winsock 依赖项。


*Winsock 安装*节必须包含**AddSock**指令。 **AddSock**指令指定了一个名为的供应商名称部分，其中包含要添加到组件的**HKEY \_ 本地 \_ 计算机 \\ 系统 \\ CurrentControlSet \\ Services \\ *TransportDriverName* \\ Params \\ Winsock**键的值。

**AddSock**指令引用的由供应商命名的部分必须包含以下必需值：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">值名称</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>TransportService</p></td>
<td align="left"><p>一个 REG_SZ 值，该值指定协议的服务名称。 此值必须与协议的 <strong>Ndi\Service</strong> 值相同。 有关详细信息，请参阅 <a href="adding-service-related-values-to-the-ndi-key.md" data-raw-source="[Adding Service-Related Values to the Ndi Key](adding-service-related-values-to-the-ndi-key.md)">将与服务相关的值添加到 Ndi 项</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HelperDllName</p></td>
<td align="left"><p>一个 REG_EXPAND_SZ 值，该值指定 Windows 套接 helper 的路径 (WSH) DLL 协议。 有关详细信息，请参阅 <a href="/previous-versions/windows/hardware/network/ff566260(v=vs.85)" data-raw-source="[WSH DLL Function Summary](/previous-versions/windows/hardware/network/ff566260(v=vs.85))">WSH DLL 函数摘要</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MaxSockAddrLength</p></td>
<td align="left"><p>一个 REG_DWORD 值，该值指定 WSH DLL 的最大有效 SOCKADDR 大小（以字节为单位）</p></td>
</tr>
<tr class="even">
<td align="left"><p>MinSockAddrLength</p></td>
<td align="left"><p>一个 REG_DWORD 值，该值指定 WSH DLL 的最小有效 SOCKADDR 大小（以字节为单位）</p></td>
</tr>
</tbody>
</table>

 

如果指定了命名空间提供程序的可选 **ProviderId** ，还必须指定以下值：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">值名称</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ProviderId</p></td>
<td align="left"><p>一个 REG_SZ 值，该值指定标识命名空间提供程序 (GUID) 的全局唯一标识符。 GUID 用作对命名空间提供程序的所有后续引用的键。 通过运行 uuidgen.exe 实用程序获取 GUID。 有关此实用工具的详细信息，请参阅 Microsoft Windows SDK。</p></td>
</tr>
<tr class="even">
<td align="left"><p>LibraryPath</p></td>
<td align="left"><p>一个 REG_EXPAND_SZ 值，该值指定指向命名空间提供程序 DLL 的完整路径。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DisplayString</p></td>
<td align="left"><p>一个可本地化的字符串，它指定在用户界面中为命名空间提供程序显示的名称。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SupportedNameSpace</p></td>
<td align="left"><p>一个 REG_DWORD 值，该值指定命名空间提供程序支持的命名空间。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>一个可选 REG_DWORD 值，该值指定命名空间提供程序的版本号。 如果未指定此值，则将默认值 (1) 用于版本号。</p></td>
</tr>
</tbody>
</table>

 

以下命名空间值可以分配给 SupportedNameSpace，并在 Winsock2. h 中定义：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">命名空间</th>
<th align="left">值</th>
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

以下示例显示了 IPX 协议的 Winsock 部分：

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

INF 文件可以通过包含 *winsock-remove* 部分来删除协议的 winsock 依赖关系。 若要创建 *Winsock 删除* 节，请添加。用于协议的 *删除* 节名称的 Winsock 扩展。 例如，如果协议的 " *删除* " 部分命名为 "ipx"，则协议的 " *Winsock 删除* " 部分必须命名为 "Ipx"。删除 winsock。

*Winsock-remove*部分包含指定 INF 写入器命名部分的**DelSock**指令。 INF 写入方命名部分必须指定要删除的传输服务。 如果先前已为协议注册了 **providerid** ，则供应商命名部分还必须指定要删除的 **providerid** 。

下面的示例演示了删除 IPX 协议的 Winsock 依赖项的两个部分：

```INF
[Ipx.Remove.Winsock]
DelSock = Remove.IpxWinsock
 
[Remove.IpxWinsock]
TransportService = nwlinkipx
ProviderId = "GUID"
```

