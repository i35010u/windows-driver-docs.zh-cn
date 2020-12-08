---
title: Tracelog 属性显示
description: Tracelog 属性显示
keywords:
- Tracelog WDK，属性
- 跟踪 WDK，属性
- 属性 WDK 跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0dc0f844398ca700d99cfce80dbd6985718e4ce9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838125"
---
# <a name="tracelog-properties-display"></a>Tracelog 属性显示

## <span id="ddk_tracelog_display_tools"></span><span id="DDK_TRACELOG_DISPLAY_TOOLS"></span>

Tracelog 显示启动、停止、更新或查询会话时跟踪会话的属性。

数据来自日志会话的事件 \_ 跟踪 \_ 属性结构。 下表对显示中的字段进行了说明。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">字段</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>操作状态</strong></p></td>
<td align="left"><p>系统返回的状态。 有关状态消息和系统错误代码的列表，请参阅 Microsoft Windows SDK 文档。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>记录器名称</strong></p></td>
<td align="left"><p>跟踪会话的名称。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>记录器 ID</strong></p></td>
<td align="left"><p>标识跟踪会话。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>记录器线程 ID</strong></p></td>
<td align="left"><p>标识运行跟踪会话的线程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>缓冲区大小</strong></p></td>
<td align="left"><p>每个缓冲区的大小（KB）。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>最大缓冲区</strong></p></td>
<td align="left"><p>一次使用的最大缓冲区数。 使用 <strong>-max</strong> 参数更改此值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>最小缓冲区</strong></p></td>
<td align="left"><p>为会话分配的最小缓冲区数。 使用 <strong>-min</strong> 参数设置此值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>缓冲区数</strong></p></td>
<td align="left"><p>为会话分配的实际缓冲区数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>可用缓冲区</strong></p></td>
<td align="left"><p>已分配但当前未使用的缓冲区。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>写入的缓冲区</strong></p></td>
<td align="left"><p>跟踪会话期间写入的缓冲区总数。 这包括写入、刷新和重写的缓冲区，因此它可以超出 <strong>最大缓冲区</strong>的值。</p>
<p>若要估计顺序日志文件的大小，请将<strong>缓冲区大小</strong>的<strong>缓冲区</strong>相乘。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>丢失的事件</strong></p></td>
<td align="left"><p>生成但未记录的事件数，通常是因为所有已分配的缓冲区已满。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>日志缓冲区丢失</strong></p></td>
<td align="left"><p>其内容无法写入日志的缓冲区数。 通常，仅当磁盘空间不足以容纳日志内容时才会发生这种情况。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>实时缓冲丢失</strong></p></td>
<td align="left"><p>无法传递其内容的缓冲区数。 通常情况下，当系统资源不足时，会发生这种情况。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>AgeLimit</strong></p></td>
<td align="left"><p>释放未使用的缓冲区之前的时间延迟。 若要更改此值，请使用 <strong>-age</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>模式</em></p>
<p> (实时模式已启用，日志文件模式，仅缓冲模式) </p></td>
<td align="left"><p>为此会话启用的日志记录模式。 有关日志记录模式常量的完整列表，请参阅 Windows SDK 文档。</p>
<div class="alert">
<strong>注意</strong><br/><p>即使未写入日志文件，也会显示 " <strong>日志文件模式</strong> " 条目。 它将显示日志文件格式。</p>
</div>
<div>

</div></td>
</tr>
<tr class="even">
<td align="left"><p><strong>启用跟踪</strong></p></td>
<td align="left"><p>正在跟踪的 NT 内核记录器事件。 只有在跟踪 NT 内核记录器会话时才会显示此字段。</p>
<div class="alert">
<strong>注意</strong><br/><p>即使正在跟踪 DPC、ISR 和上下文切换事件，也不会在该字段中显示。</p>
</div>
<div>

</div></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>日志文件名</strong></p></td>
<td align="left"><p>用于会话的日志文件。 对于实时和缓冲跟踪会话，字段值为空。</p>
<p>若要更改此值，请使用 <strong>-f</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>使用中的本地/全局序列号。</strong></p></td>
<td align="left"><p>仅当使用本地序列号或全局序列号时才显示。</p>
<p>若要更改此属性，请使用 <strong>-ls</strong> 或 <strong>-gs</strong>。</p></td>
</tr>
</tbody>
</table>
