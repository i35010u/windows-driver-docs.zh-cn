---
title: TraceView 控制命令
description: 使用 Traceview 控件命令管理跟踪会话。
keywords:
- TraceView 控件命令驱动程序开发工具
topic_type:
- apiref
api_name:
- TraceView Control Commands
api_type:
- NA
ms.date: 12/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: 119241c84b6139b290575c67ef257859804ec54e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838101"
---
# <a name="traceview-control-commands"></a>TraceView 控制命令

> [!NOTE]
> 不推荐使用 TraceView 命令行选项。 使用 tracepdb.exe 和 tracefmt.exe 将 Pdb 分析为 TMF 文件，并将 .etl 文件分别分析为文本。内容

使用 Traceview 控制命令来管理跟踪会话，包括启动和停止会话、启用和禁用提供程序、更新跟踪会话的属性以及刷新跟踪缓冲区。

```command
    traceview {-start | -stop | -update | -enable | -disable | -flush | -q} SessionName [Parameters]
```

```command
    traceview {-enumguid | -l | -h | -x}
```

## <a name="command-parameters"></a>命令参数

### <a name="actions"></a>操作

|操作|描述|
|----|----|
|**-start**|启动指定的跟踪会话。|
|**-stop**|停止指定的跟踪会话。|
|**-更新**|更新指定跟踪会话的属性。|
|**-enable**|为指定的跟踪会话启用提供程序。|
|**-disable**|禁用指定会话的提供程序。|
|**-flush**|刷新指定跟踪会话的活动缓冲区。 此强制刷新是除了当缓冲区已满时和跟踪会话停止时发生的自动刷新之外。|
|-q|查询指定跟踪会话的状态。|
|**-enumguid**|列出系统上的提供程序，这些提供程序 [已注册](registered-provider.md) 到 WINDOWS (ETW) 的事件跟踪。|
|**-l**|列出计算机上运行的所有跟踪会话。|
|**-x**|停止所有跟踪会话。|

### <a name="span-idparametersspanspan-idparametersspanparameters"></a><span id="parameters"></span><span id="PARAMETERS"></span>参数

<span id="_______SessionName______"></span><span id="_______sessionname______"></span><span id="_______SESSIONNAME______"></span>*SessionName*   
与 **-start** 一起使用时， *SessionName* 是您选择用来表示跟踪会话的名称。 对于其他所有命令， *SessionName* 标识跟踪会话。

<span id="_______-f___LogFile_"></span><span id="_______-f___logfile_"></span><span id="_______-F___LOGFILE_"></span>**-f** \[*日志文件*\]  
与 **-start** 一起使用时， **-f** 启动跟踪日志会话。 *LogFile* 指定 ( ( .etl) 文件的事件跟踪日志的可选) 和文件名。 默认值为 C： \\ LogFile。

与 **-update** 一起使用时， **-f** 仅向指定的 [跟踪日志](trace-log.md)发送所有新跟踪消息。 使用此参数可将实时跟踪会话转换为跟踪日志会话，或启动现有跟踪日志会话的新跟踪日志。 若要将跟踪消息发送到实时跟踪使用者和跟踪日志，请在 **-update** 命令中同时使用 **-rt** 和 **-f** 参数。

<span id="_______-rt______"></span><span id="_______-RT______"></span>**-rt**   
与 **-start** 一起使用时， **-rt** 启动实时跟踪会话 (跟踪日志会话 (**-f**) 是默认值。 ) 如果在 **-start** 命令中使用 **-rt** 和 **-f** ，则跟踪消息将发送到跟踪使用者和事件跟踪日志文件。

与 **-update** 一起使用时， **-rt** 会将实时消息传递添加到跟踪日志会话中。 除了 [跟踪日志](trace-log.md)以外，所有新跟踪消息都将直接发送到跟踪使用者 (如) 的实时跟踪会话中。

<span id="_______-guid___GUID___GUIDFile_"></span><span id="_______-guid___guid___guidfile_"></span><span id="_______-GUID___GUID___GUIDFILE_"></span>**-guid** { **\#** <em>guid</em>  |  *GUIDFile*}  
指定一个或多个跟踪提供程序。 使用 with **-start** 启用跟踪会话的提供程序。 使用 with **-enable** 启用提供程序或更改其 **标志** 或 **级别** 值。 使用 with **-disable** 指定要禁用的提供程序。

*GUID* 可以指定一个 (前面带有数字符号 (的 [控件 guid](control-guid.md) **\#** ，) # A3 或文本文件 (可选) 和文件名（例如控件 guid ( 文件），该文件包含一个或多个跟踪提供程序的控件 guid。

如果从 **-start** 命令中省略 **-Guid** 参数，TraceView 将启动 [NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)。

TraceView 将以下子参数的值传递到指定的提供程序。

<table>
<thead>
<tr>
<th>参数</th>
<th>描述</th>
</tr>
<tbody>
<tr>
<td><em>SessionName</em></td>
<td>与 <strong>-start</strong>一起使用时， <em>SessionName</em> 是您选择用来表示跟踪会话的名称。 对于其他所有命令， <em>SessionName</em> 标识跟踪会话。</td>
</tr>
<tr>
<td><strong>-f</strong> \[<em>日志文件</em>\]</td>
<td><p>与 <strong>-start</strong>一起使用时， <strong>-f</strong> 启动跟踪日志会话。 <em>LogFile</em> 指定 ( ( .etl) 文件的事件跟踪日志的可选) 和文件名。 默认值为 C： \\ LogFile。</p>
<p>与 <strong>-update</strong>一起使用时， <strong>-f</strong> 仅向指定的 [跟踪日志](trace-log.md)发送所有新跟踪消息。 使用此参数可将实时跟踪会话转换为跟踪日志会话，或启动现有跟踪日志会话的新跟踪日志。 若要将跟踪消息发送到实时跟踪使用者和跟踪日志，请在<strong>-update</strong>命令中同时使用<strong>-rt</strong>和<strong>-f</strong>参数。</p>
</td>
</tr>
<tr>
<td><strong>-rt</strong></td>
<td><p>与<strong>-start</strong>一起使用时， <strong>-rt</strong>启动实时跟踪会话 (跟踪日志会话 (<strong>-f</strong>) 是默认值。 ) 如果在<strong>-start</strong>命令中使用<strong>-rt</strong>和<strong>-f</strong> ，则跟踪消息将发送到跟踪使用者和事件跟踪日志文件。</p>
<p>与 <strong>-update</strong>一起使用时， <strong>-rt</strong> 会将实时消息传递添加到跟踪日志会话中。 除了 [跟踪日志](trace-log.md)以外，所有新跟踪消息都将直接发送到跟踪使用者 (如) 的实时跟踪会话中。</p>
</td>
</tr>
<tr>
<td><strong>-guid</strong> { <strong>\#</strong> <em>guid</em>  |  <em>GUIDFile</em>}</td>
<td><p>指定一个或多个跟踪提供程序。 使用 with <strong>-start</strong> 启用跟踪会话的提供程序。 使用 with <strong>-enable</strong> 启用提供程序或更改其 <strong>标志</strong> 或 <strong>级别</strong> 值。 使用 with <strong>-disable</strong> 指定要禁用的提供程序。</p>
<p><em>GUID</em> 可以指定一个 (前面带有数字符号 (的 [控件 guid](control-guid.md) <strong>\#</strong> ，) # A3 或文本文件 (可选) 和文件名（例如控件 guid ( 文件），该文件包含一个或多个跟踪提供程序的控件 guid。</p>
<p>如果从<strong>-start</strong>命令中省略<strong>-Guid</strong>参数，TraceView 将启动[NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)。</p>
</td>
</tr>
</tbody>
</table>

TraceView 将以下子参数的值传递到指定的提供程序：

<table>
<thead>
<tr>
<th>子参数 guid</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr>
<td><p><strong>-标志</strong><em>标志</em></p></td>

<span id="_______-b_______BufferSize______"></span><span id="_______-b_______buffersize______"></span><span id="_______-B_______BUFFERSIZE______"></span>**-b** *BufferSize*   
指定为跟踪会话分配的每个缓冲区的大小（以 KB 为单位）。 仅使用 **-start**。

默认值由处理器数量、物理内存量和使用中的操作系统决定。

<span id="_______-min_______NumberOfBuffers______"></span><span id="_______-min_______numberofbuffers______"></span><span id="_______-MIN_______NUMBEROFBUFFERS______"></span>**-最小** *NumberOfBuffers*   
指定最初为存储跟踪消息分配的缓冲区数。 仅使用 **-start**。

默认值由处理器数量、物理内存量和使用中的操作系统决定。

<span id="_______-max_______NumberOfBuffers______"></span><span id="_______-max_______numberofbuffers______"></span><span id="_______-MAX_______NUMBEROFBUFFERS______"></span>**-最大** *NumberOfBuffers*   
与 **-start** 一起使用时， **-max** 指定为跟踪会话分配的最大缓冲区数。 默认值由处理器数量、物理内存量和使用中的操作系统决定。

与 **-update** 一起使用时， **-max** 更改为跟踪会话分配的最大缓冲区数。

<span id="_______-ft_______FlushTime______"></span><span id="_______-ft_______flushtime______"></span><span id="_______-FT_______FLUSHTIME______"></span>**-ft** *FlushTime*   
与 **-start** 一起使用时， **-ft** 指定刷新跟踪消息缓冲区的频率（以秒为单位）。 与 **-update** 一起使用时， **-ft** 会将刷新时间更改为指定的时间。

最小刷新时间为1秒。 默认值为0， (没有强制刷新) 。

此强制刷新除了跟踪消息缓冲区已满和跟踪会话停止时自动发生的刷新之外。

另请参阅： **-flush**。

<span id="_______-paged______"></span><span id="_______-PAGED______"></span>**-分页**   
为跟踪消息缓冲区使用可分页内存。 默认情况下，事件跟踪使用不可分页 memory 作为缓冲区。 仅使用 **-start**。

当提供程序是可能生成比调度级别更多的 IRQL 的跟踪消息的驱动程序时，请勿使用此参数 \_ 。

Windows 2000 不支持此参数。

<span id="_______-seq_______MaxFileSize______"></span><span id="_______-seq_______maxfilesize______"></span><span id="_______-SEQ_______MAXFILESIZE______"></span>**-seq** *MaxFileSize*   
指定顺序日志记录 (在文件末尾，停止记录事件) 到事件跟踪日志 ( .etl) 文件中。 仅使用 **-start**。

*MaxFileSize* 指定文件的最大大小（MB）。 如果没有 *MaxFileSize* 值，则忽略此参数。

顺序日志记录是默认值，但你可以使用此参数设置最大文件大小或使用 **-prealloc**。 如果没有此参数，则没有文件大小限制。

<span id="_______-cir_______MaxFileSize______"></span><span id="_______-cir_______maxfilesize______"></span><span id="_______-CIR_______MAXFILESIZE______"></span>**-cir** *MaxFileSize*   
指定文件结尾处的循环日志记录 (，并在事件跟踪日志 ( .etl) 文件中记录最早消息) 的新消息。 仅使用 **-start**。

*MaxFileSize* 指定文件的最大大小（MB）。 如果没有 *MaxFileSize* 值，则忽略此参数。

默认值为顺序日志记录，没有文件大小限制。

<span id="_______-prealloc______"></span><span id="_______-PREALLOC______"></span>**-prealloc**   
在分配事件跟踪日志 ( .etl) 文件之前，为其预留空间。 仅使用 **-start**。

此参数需要 **-seq** 或 **-cir** with *MaxFileSize*。 它对于 **-newfile** 无效。

<p><em>标志</em> 表示在跟踪提供程序中定义的标志值（采用十进制或十六进制格式）。 默认值为 0。 0x01000000 到0xFF000000 的值保留供将来使用。</p>

<p>标志的含义由每个跟踪提供程序单独定义。 通常，标志表示越来越详细的报表级别。</p>

<p>在 <strong>-start</strong> 命令中，标志值适用于跟踪会话中的所有跟踪提供程序。 若要为每个跟踪提供程序设置不同的标志，请对每个跟踪提供程序使用单独的 <strong>启用</strong> 命令。</p>
</td>
</tr>

<tr>
<td>
<p><strong>级别</strong><em>级别</em></p>
</td>
<td>
<p>指定跟踪会话中提供程序的 <a href="trace-level.md" data-raw-source="[trace level](trace-level.md)">跟踪级别</a> 。 级别确定跟踪提供程序生成的事件。</p>

<p><em>Level</em> 表示以十进制或十六进制格式表示的级别值。 默认值为 0。</p>

<p>级别值的含义由每个跟踪提供程序单独定义。 通常，跟踪级别表示事件的严重性 (信息、警告或错误) 。</p>

<p>在 <strong>-start</strong> 命令中，level 值适用于跟踪会话中的所有跟踪提供程序。 若要为每个跟踪提供程序设置不同的级别，请对每个跟踪提供程序使用单独的 <strong>启用</strong> 命令。</p>
</td>
</tr>
</tbody>
</table>

<table>
<thead>
<tr>参数</tr>
<tr>描述</tr>
</thead>
<tbody>
<tr>
<td><strong>-b</strong> <em>BufferSize</em></td>
<td>指定为跟踪会话分配的每个缓冲区的大小（以 KB 为单位）。 仅使用 <strong>-start</strong>。
<p>默认值由处理器数量、物理内存量和使用中的操作系统决定。</p></td>
</tr>
<tr>
<td><strong>-最小</strong> <em>NumberOfBuffers</em></td>
<td>指定最初为存储跟踪消息分配的缓冲区数。 仅使用 <strong>-start</strong>。
<p>默认值由处理器数量、物理内存量和使用中的操作系统决定。</p></td>
</tr>
<tr>
<td><strong>-最大</strong> <em>NumberOfBuffers</em></td>
<td>与 <strong>-start</strong>一起使用时， <strong>-max</strong> 指定为跟踪会话分配的最大缓冲区数。 默认值由处理器数量、物理内存量和使用中的操作系统决定。
<p>与 <strong>-update</strong>一起使用时， <strong>-max</strong> 更改为跟踪会话分配的最大缓冲区数。</p></td>
</tr>
<tr>
<td><strong>-ft</strong> <em>FlushTime</em></td>
<td>与 <strong>-start</strong>一起使用时， <strong>-ft</strong> 指定刷新跟踪消息缓冲区的频率（以秒为单位）。 与 <strong>-update</strong>一起使用时， <strong>-ft</strong> 会将刷新时间更改为指定的时间。
<p>最小刷新时间为1秒。 默认值为0， (没有强制刷新) 。</p>
<p>此强制刷新除了跟踪消息缓冲区已满和跟踪会话停止时自动发生的刷新之外。</p>
<p>另请参阅： <strong>-flush</strong>。</p></td>
</tr>
<tr>
<td><strong>-age</strong> <em>AgeLimit</em></td>
<td>当与 <strong>-start</strong>一起使用时， <strong> age <strong> 指定在释放 (多长时间后) 未使用的跟踪缓冲区。 与-update 一起使用时 <strong> <strong> ，age 会将 <strong> <strong> 期限更改为指定值。
<p><em>Age 限制</em> 指定在释放) 未使用的跟踪缓冲区之前，该时间段内 (的时间长度。 默认值为 15 分钟。</p>
<p>此参数仅在 Windows 2000 中有效。</p></td>
</tr>
<tr>
<td><strong>-分页</strong></td>
<td>为跟踪消息缓冲区使用可分页内存。 默认情况下，事件跟踪使用不可分页 memory 作为缓冲区。 仅使用 <strong>-start</strong>。
<p>当提供程序是可能生成比调度级别更多的 IRQL 的跟踪消息的驱动程序时，请勿使用此参数 \_ 。</p>
<p>Windows 2000 不支持此参数。</p></td>
</tr>
<tr>
<td><strong>-seq</strong> <em>MaxFileSize</em></td>
<td>指定顺序日志记录 (在文件末尾，停止记录事件) 到事件跟踪日志 ( .etl) 文件中。 仅使用 <strong>-start</strong>。
<p><em>MaxFileSize</em> 指定文件的最大大小（MB）。 如果没有 <em>MaxFileSize</em> 值，则忽略此参数。</p>
<p>顺序日志记录是默认值，但你可以使用此参数设置最大文件大小或使用 <strong>-prealloc</strong>。 如果没有此参数，则没有文件大小限制。</p></td>
</tr>
<tr>
<td><strong>-cir</strong> <em>MaxFileSize</em></td>
<td>指定文件结尾处的循环日志记录 (，并在事件跟踪日志 ( .etl) 文件中记录最早消息) 的新消息。 仅使用 <strong>-start</strong>。
<p><em>MaxFileSize</em> 指定文件的最大大小（MB）。 如果没有 <em>MaxFileSize</em> 值，则忽略此参数。</p>
<p>默认值为顺序日志记录，没有文件大小限制。</p></td>
</tr>
<tr>
<td><strong>-prealloc</strong></td>
<td>在分配事件跟踪日志 ( .etl) 文件之前，为其预留空间。 仅使用 <strong>-start</strong>。
<p>此参数需要 <strong>-seq</strong> 或 <strong>-cir</strong> with <em>MaxFileSize</em>。 它对于 <strong>-newfile</strong>无效。</p>
<p>在 Windows XP 和更高版本的系统中，系统创建事件跟踪日志 ( .etl) 文件，其大小等于使用<strong>-seq</strong>或<strong>-cir</strong>参数指定的<em>MaxFileSize</em>值。 停止会话时，它会将日志文件减少到其内容大小。</p></td>
</tr>
<tr>
<td><strong>-newfile</strong> <em>MaxFileSize</em></td>
<td>每当现有文件 <em>MaxFileSize</em>时，都将创建一个新的事件跟踪日志 ( .etl) 文件。 仅使用 <strong>-start</strong>。
<p><em>MaxFileSize</em> 指定每个日志文件的最大大小（MB）。 如果没有 <em>MaxFileSize</em> 值，则忽略此参数。</p>
<p>使用 <strong>-newfile</strong>时，还必须使用 <strong>-f</strong> <em>logfile</em> 参数，而 <em>LogFile</em> 的值必须是包含字符 <strong>% d</strong> 的名称，以指示小数模式-例如，trace% d. .etl。 否则，该命令将失败并返回 \_ 无效 \_ 名称。 每次创建新文件时，Windows 都会递增文件名中的十进制值。</p>
<p>此参数对预先分配 (<strong>-prealloc</strong> 日志记录 (<strong>-CIR</strong>) 、NT 内核记录器会话或专用跟踪会话无效。 Windows 2000 不支持此方法。</p></td>
</tr>
<tr>
<td><strong>-append</strong></td>
<td>将跟踪消息追加到现有的事件跟踪日志 ( .etl) 文件中。 默认为创建新文件。 仅使用 <strong>-start</strong>。
<p>此参数仅对顺序文件有效，并且仅当使用 <strong>-f</strong> 并且未使用 <strong>-rt</strong> 时才有效。 Windows 2000 不支持此方法。</p></td>
</tr>
<tr>
<td><strong>-kd</strong></td>
<td>将跟踪消息重定向到 KD 或 Windbg，无论附加哪个。 此参数还将跟踪缓冲区大小设置为 3 KB，为调试器设置最大缓冲区大小，并忽略命令中的任何 <strong>-b</strong> 参数。 仅使用 <strong>-start</strong>。</td>
</tr>
</tbody>
</table>

### <a name="comments"></a>注释

不带参数的 **traceview** 命令会打开 "traceview" 窗口。

可以使用 TraceView 命令启动 [全局记录器跟踪会话](global-logger-trace-session.md)。 为此，请使用以下命令格式。 与其他命令不同，此命令格式的 "GlobalLogger" 一词区分大小写。

```command
traceview -start GlobalLogger [parameters]
```
