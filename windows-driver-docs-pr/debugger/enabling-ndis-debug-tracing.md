---
title: 启用 NDIS 调试跟踪
description: 启用 NDIS 调试跟踪
keywords:
- NDIS 调试，调试跟踪
ms.date: 05/12/2020
ms.localizationpriority: medium
ms.openlocfilehash: 5328378c66c5b8f4964d93bc4e645b1f3f5bd078
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813269"
---
# <a name="enabling-ndis-debug-tracing"></a>启用 NDIS 调试跟踪

NDIS 调试跟踪是调试 NDIS 驱动程序的主要方法。 设置 NDIS 调试跟踪时，实际上是要通过 NDIS 启用一个或多个 DbgPrint 语句级别。 生成的信息足以用于调试大多数网络驱动程序问题。

## <a name="enabling-ndis-debug-tracing-by-setting-registry-values"></a>通过设置注册表值启用 NDIS 调试跟踪

可以通过编辑注册表在不同的 NDIS 组件中启用不同级别的调试跟踪。 通常，应将以下项和值添加到 **HKLM \\ SYSTEM \\ CurrentControlSet \\ Services \\ NDIS \\ Parameters** 注册表项：

```text
"DebugLevel"=dword:00000000
"DebugSystems"=dword:000030F3
"DebugBreakPoint"=dword:00000001 
```

对于 **DebugBreakPoint**、 **DebugLevel** 和 **DebugSystems**，以下值是可接受的：

<span id="DebugBreakPoint"></span><span id="debugbreakpoint"></span><span id="DEBUGBREAKPOINT"></span>**DebugBreakPoint**  
控制 NDIS 驱动程序是否会自动中断到调试器。 如果此值设置为1，当驱动程序输入 Ndis.sys 的 **DriverEntry** 函数时，NDIS 将中断到调试器。

<span id="DebugLevel"></span><span id="debuglevel"></span><span id="DEBUGLEVEL"></span>**DebugLevel**  
在选择了 **DebugSystems** 值的 NDIS 组件中选择调试跟踪的级别或量。 下列值指定可以选择的级别：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Level</th>
<th align="left">描述</th>
<th align="left">“值”</th>
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
<td align="left"><p>“错误”。</p></td>
<td align="left"><p>0x00002000</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_LEVEL_FATAL</p></td>
<td align="left"><p>致命错误，这可能会导致操作系统崩溃。 这是最小跟踪级别。</p></td>
<td align="left"><p>0x00003000</p></td>
</tr>
</tbody>
</table>

<span id="DebugSystems"></span><span id="debugsystems"></span><span id="DEBUGSYSTEMS"></span>**DebugSystems**  
为指定的 NDIS 组件启用调试跟踪。 这对应于使用 [**！ ndiskd**](-ndiskd-dbgsystems.md) 扩展名。 以下值指定可以选择的 NDIS 组件：

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
<th align="left">“值”</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DBG_COMP_INIT</p></td>
<td align="left"><p>处理适配器初始化。</p></td>
<td align="left"><p>0x00000001</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_COMP_CONFIG</p></td>
<td align="left"><p>处理适配器配置。</p></td>
<td align="left"><p>0x00000002</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_COMP_SEND</p></td>
<td align="left"><p>处理通过网络发送数据。</p></td>
<td align="left"><p>0x00000004</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_COMP_RECV</p></td>
<td align="left"><p>处理从网络接收数据的句柄。</p></td>
<td align="left"><p>0x00000008</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_COMP_PROTOCOL</p></td>
<td align="left"><p>处理协议操作。</p></td>
<td align="left"><p>0x00000010</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_COMP_BIND</p></td>
<td align="left"><p>处理绑定操作。</p></td>
<td align="left"><p>0x00000020</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_COMP_BUSINFO</p></td>
<td align="left"><p>处理总线查询。</p></td>
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
<td align="left"><p>处理筛选器操作。</p></td>
<td align="left"><p>0x00000200</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_COMP_REQUEST</p></td>
<td align="left"><p>处理请求。</p></td>
<td align="left"><p>0x00000400</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_COMP_WORK_ITEM</p></td>
<td align="left"><p>处理工作项操作。</p></td>
<td align="left"><p>0x00000800</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_COMP_PNP</p></td>
<td align="left"><p>处理即插即用操作。</p></td>
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
<td align="left"><p>处理重置操作。</p></td>
<td align="left"><p>0x00010000</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_COMP_WMI</p></td>
<td align="left"><p>处理 Windows Management Instrumentation 操作。</p></td>
<td align="left"><p>0x00020000</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_COMP_CO</p></td>
<td align="left"><p>处理 Connection-Oriented NDIS。</p></td>
<td align="left"><p>0x00040000</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_COMP_REF</p></td>
<td align="left"><p>处理引用操作。</p></td>
<td align="left"><p>0x00080000</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_COMP_ALL</p></td>
<td align="left"><p>处理所有 NDIS 组件。</p></td>
<td align="left"><p>0xFFFFFFFF</p></td>
</tr>
</tbody>
</table>

你可以选择多个 NDIS 组件。 如果选择了多个组件，请将数据值与 OR 运算符组合。 例如，若要依次选择 "DBG"、"DBG"、"dbg"、"dbg comp" \_ \_ 和 "dbg" \_ \_ \_ \_ \_ \_ ，请将相应的值组合 (0x1000、0x2000、0x1 和 0x2) 以获取0x3003 值，然后在注册表中对其进行设置：

```text
"DebugSystems"=dword:00003003
```

每当更改调试跟踪的注册表值时，都必须重新启动计算机才能使新设置生效。
