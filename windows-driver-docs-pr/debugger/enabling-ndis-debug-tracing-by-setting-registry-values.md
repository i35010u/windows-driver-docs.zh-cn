---
title: 通过设置注册表值启用 NDIS 调试跟踪
description: 通过设置注册表值启用 NDIS 调试跟踪
ms.assetid: ae01f546-0636-4e67-bfc7-229c3cc24b27
keywords:
- NDIS 调试，调试跟踪，设置注册表值
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d06839b09b7af4aa5c290e9d5628e7ce30a91c7e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340596"
---
# <a name="enabling-ndis-debug-tracing-by-setting-registry-values"></a>通过设置注册表值启用 NDIS 调试跟踪


通过编辑注册表，可以启用不同级别的各种 NDIS 组件中的调试跟踪。 通常情况下，应添加以下条目和值与**HKLM\\系统\\CurrentControlSet\\Services\\NDIS\\参数**注册表项：

```text
"DebugLevel"=dword:00000000
"DebugSystems"=dword:000030F3
"DebugBreakPoint"=dword:00000001 
```

以下值是否符合**DebugBreakPoint**， **DebugLevel**并**DebugSystems**:

<span id="DebugBreakPoint"></span><span id="debugbreakpoint"></span><span id="DEBUGBREAKPOINT"></span>**DebugBreakPoint**  
控制是否 NDIS 驱动程序会自动进入调试器。 当驱动程序进入 Ndis.sys 的此值设置为 1，如果 NDIS 将中断调试器**DriverEntry**函数。

<span id="DebugLevel"></span><span id="debuglevel"></span><span id="DEBUGLEVEL"></span>**DebugLevel**  
选择与的 NDIS 组件中选择的级别或调试跟踪的量**DebugSystems**值。 以下值指定可以选择的级别：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">级别</th>
<th align="left">描述</th>
<th align="left">值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DBG_LEVEL_INFO</p></td>
<td align="left"><p>所有可用的调试信息。 这是最高级别的跟踪。</p></td>
<td align="left"><p>0x00000000</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_LEVEL_LOG</p></td>
<td align="left"><p>日志信息。</p></td>
<td align="left"><p>0x00000800</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_LEVEL_WARN</p></td>
<td align="left"><p>警告。</p></td>
<td align="left"><p>0x00001000</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_LEVEL_ERR</p></td>
<td align="left"><p>错误。</p></td>
<td align="left"><p>0x00002000</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_LEVEL_FATAL</p></td>
<td align="left"><p>致命错误，可能会导致操作系统崩溃。 这是跟踪的最低级别。</p></td>
<td align="left"><p>0x00003000</p></td>
</tr>
</tbody>
</table>

 

<span id="DebugSystems"></span><span id="debugsystems"></span><span id="DEBUGSYSTEMS"></span>**DebugSystems**  
启用调试对指定 NDIS 组件的跟踪。 这对应于使用[ **！ ndiskd.dbgsystems** ](-ndiskd-dbgsystems.md)扩展。 以下值指定可以选择的 NDIS 组件：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">组件</th>
<th align="left">描述</th>
<th align="left">ReplTest1</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DBG_COMP_INIT</p></td>
<td align="left"><p>处理适配器的初始化。</p></td>
<td align="left"><p>0x00000001</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_COMP_CONFIG</p></td>
<td align="left"><p>处理适配器配置。</p></td>
<td align="left"><p>0x00000002</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_COMP_SEND</p></td>
<td align="left"><p>通过网络发送数据的句柄。</p></td>
<td align="left"><p>0x00000004</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_COMP_RECV</p></td>
<td align="left"><p>从网络接收数据的句柄。</p></td>
<td align="left"><p>0x00000008</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_COMP_PROTOCOL</p></td>
<td align="left"><p>处理的协议操作。</p></td>
<td align="left"><p>0x00000010</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_COMP_BIND</p></td>
<td align="left"><p>绑定操作的句柄。</p></td>
<td align="left"><p>0x00000020</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_COMP_BUSINFO</p></td>
<td align="left"><p>处理总线的查询。</p></td>
<td align="left"><p>0x00000040</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_COMP_REG</p></td>
<td align="left"><p>处理注册表操作。</p></td>
<td align="left"><p>0x00000080</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_COMP_MEMORY</p></td>
<td align="left"><p>处理内存管理。</p></td>
<td align="left"><p>0x00000100</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_COMP_FILTER</p></td>
<td align="left"><p>句柄的筛选器操作。</p></td>
<td align="left"><p>0x00000200</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_COMP_REQUEST</p></td>
<td align="left"><p>处理请求。</p></td>
<td align="left"><p>0x00000400</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_COMP_WORK_ITEM</p></td>
<td align="left"><p>句柄工作项操作。</p></td>
<td align="left"><p>0x00000800</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_COMP_PNP</p></td>
<td align="left"><p>处理操作，即插即用和播放。</p></td>
<td align="left"><p>0x00001000</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_COMP_PM</p></td>
<td align="left"><p>处理电源管理操作。</p></td>
<td align="left"><p>0x00002000</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_COMP_OPENREF</p></td>
<td align="left"><p>处理打开引用对象的操作。</p></td>
<td align="left"><p>0x00004000</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_COMP_LOCKS</p></td>
<td align="left"><p>处理锁定操作。</p></td>
<td align="left"><p>0x00008000</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_COMP_RESET</p></td>
<td align="left"><p>重置操作的句柄。</p></td>
<td align="left"><p>0x00010000</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_COMP_WMI</p></td>
<td align="left"><p>处理 Windows Management Instrumentation 的操作。</p></td>
<td align="left"><p>0x00020000</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_COMP_CO</p></td>
<td align="left"><p>处理面向连接的 NDIS。</p></td>
<td align="left"><p>0x00040000</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_COMP_REF</p></td>
<td align="left"><p>句柄引用的操作。</p></td>
<td align="left"><p>0x00080000</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_COMP_ALL</p></td>
<td align="left"><p>处理所有 NDIS 组件。</p></td>
<td align="left"><p>0xFFFFFFFF</p></td>
</tr>
</tbody>
</table>

 

您可以选择多个 NDIS 组件。 如果选择多个组件，则将与 OR 运算符组合的数据值。 例如，若要选择 DBG\_COMP\_PNP、 DBG\_COMP\_PM，DBG\_COMP\_INIT 和 DBG\_COMP\_的配置来说，会结合相应值 （0x1000、 0x2000、 0x1 和 0x2） 来获取值 0x3003，并因此然后将其设置在注册表中：

```text
"DebugSystems"=dword:00003003
```

只要您更改调试跟踪的注册表值，必须重新启动计算机中的新设置才能生效。

 

 





