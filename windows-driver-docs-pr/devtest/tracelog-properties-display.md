---
title: Tracelog 属性显示
description: Tracelog 属性显示
ms.assetid: 9adfb4d5-5a0b-4e79-9aa8-ae81e2e1df3e
keywords:
- Tracelog WDK 属性
- 跟踪 WDK，属性
- 属性 WDK 跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de983da6a83b9c80fd4da513ca9b05af06d344d2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369719"
---
# <a name="tracelog-properties-display"></a>Tracelog 属性显示

## <span id="ddk_tracelog_display_tools"></span><span id="DDK_TRACELOG_DISPLAY_TOOLS"></span>

Tracelog 显示跟踪会话时启动、 停止、 更新或查询的会话的属性。

数据来自事件\_跟踪\_日志会话的属性结构。 下表介绍中显示的字段。

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
<td align="left"><p>返回系统的状态。 有关状态消息和系统错误代码的列表，请参阅 Microsoft Windows SDK 文档。</p></td>
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
<td align="left"><p>以 kb 为单位的每个缓冲区的大小。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>最大缓冲区</strong></p></td>
<td align="left"><p>要一次使用的缓冲区最大数目。 使用<strong>-最大</strong>参数来更改此值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>最小缓冲区</strong></p></td>
<td align="left"><p>最小会话分配的缓冲区数。 使用<strong>-最小值</strong>参数，以将此值设置。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>缓冲区数</strong></p></td>
<td align="left"><p>实际分配的会话的缓冲区数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>可用缓冲区</strong></p></td>
<td align="left"><p>缓冲区的分配，但当前未被使用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>写入缓冲区</strong></p></td>
<td align="left"><p>跟踪会话期间写入的缓冲区总数。 这包括缓冲区写入和刷新，然后重新编写，因此它可以超出的值<strong>最大缓冲区</strong>。</p>
<p>若要估计顺序日志文件的大小，乘<strong>缓冲区写入</strong>通过<strong>缓冲区大小</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>丢失事件</strong></p></td>
<td align="left"><p>已生成但不会记录，通常因为所有已分配的缓冲区已满的事件数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>丢失的日志缓冲区</strong></p></td>
<td align="left"><p>其内容无法写入到日志的缓冲区数。 通常，仅当没有足够的磁盘空间来保存日志内容时出现此情况。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>丢失的实时缓冲区</strong></p></td>
<td align="left"><p>其内容，无法传递的缓冲区数。 通常，当系统资源不足时出现此情况。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>AgeLimit</strong></p></td>
<td align="left"><p>释放未使用的缓冲区之前的时间延迟。 若要更改此值，请使用<strong>-年龄</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>模式</em></p>
<p>（已启用的实时模式下，日志文件模式下，缓冲模式下）</p></td>
<td align="left"><p>为此会话启用日志记录模式。 有关日志记录模式常量的完整列表，请参阅 Windows SDK 文档。</p>
<div class="alert">
<strong>注意</strong><br/><p><strong>日志文件模式</strong>甚至不写入日志文件时出现条目。 它将显示日志文件格式。</p>
</div>
<div>

</div></td>
</tr>
<tr class="even">
<td align="left"><p><strong>已启用的跟踪</strong></p></td>
<td align="left"><p>正在跟踪 NT 内核记录器事件。 仅当跟踪 NT 内核记录器会话时，将显示此字段。</p>
<div class="alert">
<strong>注意</strong><br/><p>DPC、 ISR 和上下文切换事件不显示在此字段中，即使它们正在跟踪。</p>
</div>
<div>

</div></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>日志文件名</strong></p></td>
<td align="left"><p>使用会话的日志文件。 对于实时和缓冲跟踪会话，字段值为空白。</p>
<p>若要更改此值，请使用<strong>-f</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>在使用本地/全局序列号。</strong></p></td>
<td align="left"><p>将显示仅当使用本地或全局序列号时。</p>
<p>若要更改此属性，请使用<strong>-ls</strong>或<strong>-gs</strong>。</p></td>
</tr>
</tbody>
</table>
