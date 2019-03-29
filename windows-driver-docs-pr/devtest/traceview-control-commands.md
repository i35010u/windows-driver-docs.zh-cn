---
title: TraceView 控制命令
description: Traceview 控制命令用于管理跟踪会话。
ms.assetid: 3ebfb728-7ca7-473d-b4bb-a62d1704aed6
keywords:
- TraceView 管理命令，驱动程序开发工具
topic_type:
- apiref
api_name:
- TraceView Control Commands
api_type:
- NA
ms.date: 12/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: 13aea23c888d1fa5b0802861affe5fe2a07b01ec
ms.sourcegitcommit: 132f0c2d827982b808053ecd3b4d137a2883cca1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2019
ms.locfileid: "56582789"
---
# <a name="traceview-control-commands"></a>TraceView 控制命令

> [!NOTE]
> TraceView 命令行选项已被弃用。 使用 tracepdb.exe 和 tracefmt.exe 分析成 TMF 文件和分析成文本，.etl 文件的 Pdb respectively.content

Traceview 控制命令用于管理跟踪会话，包括启动和停止该会话、 启用和禁用提供程序，更新跟踪会话的属性以及刷新跟踪缓冲区。

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
|**-update**|更新指定的跟踪会话的属性。|
|**-enable**|为指定的跟踪会话启用提供程序。|
|**-disable**|为指定会话禁用提供程序。|
|**-flush**|刷新指定的跟踪会话的活动缓冲区。 强制刷新其中不包括出现当缓冲区已满并且停止跟踪会话时自动刷新。|
|**-q**|查询指定的跟踪会话的状态。|
|**-enumguid**|列出可以在系统上的提供商[注册](registered-provider.md)使用事件跟踪 Windows (ETW)。|
|**-l**|列出计算机上运行的所有跟踪会话。|
|**-x**|停止所有跟踪会话。|

### <a name="span-idparametersspanspan-idparametersspanparameters"></a><span id="parameters"></span><span id="PARAMETERS"></span>参数

<span id="_______SessionName______"></span><span id="_______sessionname______"></span><span id="_______SESSIONNAME______"></span> *SessionName*   
与一起使用时 **-启动**， *SessionName*是选择用于表示跟踪会话的名称。 与所有其他命令， *SessionName*标识跟踪会话。

<span id="_______-f___LogFile_"></span><span id="_______-f___logfile_"></span><span id="_______-F___LOGFILE_"></span> **-f** \[*LogFile*\]  
与一起使用时 **-启动**， **-f**跟踪日志会话启动。 *日志文件*指定的路径 （可选） 和事件跟踪日志 (.etl) 文件的文件名。 默认值为 c:\\LogFile.etl。

与一起使用时 **-更新**， **-f**将所有新的跟踪消息发送到指定[跟踪日志](trace-log.md)。 使用此参数将转换为跟踪日志会话的实时跟踪会话或现有的跟踪日志会话启动新的跟踪日志。 要将跟踪消息发送到实时跟踪使用者和跟踪日志，请同时使用 **-rt**并 **-f**中的参数 **-更新**命令。

<span id="_______-rt______"></span><span id="_______-RT______"></span> **-rt**   
与一起使用时 **-启动**， **-rt**启动实时跟踪会话 (跟踪日志会话 (**-f**) 是默认值。)如果您使用 **-rt**并 **-f**中 **-启动**命令时，跟踪消息发送到跟踪使用者和事件跟踪日志文件。

与一起使用时 **-更新**， **-rt**将添加到跟踪日志会话的实时消息传递。 所有新的跟踪消息直接发送到跟踪使用者 （如实时跟踪会话），除了[跟踪日志](trace-log.md)。

<span id="_______-guid___GUID___GUIDFile_"></span><span id="_______-guid___guid___guidfile_"></span><span id="_______-GUID___GUID___GUIDFILE_"></span> **-guid** {**\#**<em>GUID</em> | *GUIDFile*}  
指定一个或多个跟踪提供程序。 使用具有 **-启动**若要启用用于跟踪会话提供程序。 使用具有 **-启用**启用提供程序或更改其 **-标志**或 **-级别**值。 使用具有 **-禁用**来指定要禁用的提供程序。

*GUID*可以指定其中任意一个[控制 GUID](control-guid.md) (跟在数字符号 (**\#**)) 的路径 （可选） 和文件名称的文本文件，例如控制 GUID (.ctl) 文件，或，包含控件的一个或多个跟踪提供程序的 Guid。

如果省略**guid**中的参数 **-启动**命令，TraceView 启动[NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)。

TraceView 将以下子参数的值传递给指定的提供程序。

<table>
<thead>
<tr>
<th>参数</th>
<th>描述</th>
</tr>
<tbody>
<tr>
<td><em>SessionName</em></td>
<td>与一起使用时<strong>-启动</strong>， <em>SessionName</em>是选择用于表示跟踪会话的名称。 与所有其他命令， <em>SessionName</em>标识跟踪会话。</td>
</tr>
<tr>
<td><strong>-f</strong> \[<em>LogFile</em>\]</td>
<td><p>与一起使用时<strong>-启动</strong>， <strong>-f</strong>跟踪日志会话启动。 <em>日志文件</em>指定的路径 （可选） 和事件跟踪日志 (.etl) 文件的文件名。 默认值为 c:\\LogFile.etl。</p>
<p>与一起使用时<strong>-更新</strong>， <strong>-f</strong>将所有新的跟踪消息发送到指定[跟踪日志](trace-log.md)。 使用此参数将转换为跟踪日志会话的实时跟踪会话或现有的跟踪日志会话启动新的跟踪日志。 要将跟踪消息发送到实时跟踪使用者和跟踪日志，请同时使用<strong>-rt</strong>并<strong>-f</strong>中的参数<strong>-更新</strong>命令。</p>
</td>
</tr>
<tr>
<td><strong>-rt</strong></td>
<td><p>与一起使用时<strong>-启动</strong>， <strong>-rt</strong>启动实时跟踪会话 (跟踪日志会话 (<strong>-f</strong>) 是默认值。)如果您使用<strong>-rt</strong>并<strong>-f</strong>中<strong>-启动</strong>命令时，跟踪消息发送到跟踪使用者和事件跟踪日志文件。</p>
<p>与一起使用时<strong>-更新</strong>， <strong>-rt</strong>将添加到跟踪日志会话的实时消息传递。 所有新的跟踪消息直接发送到跟踪使用者 （如实时跟踪会话），除了[跟踪日志](trace-log.md)。</p>
</td>
</tr>
<tr>
<td><strong>-guid</strong> {<strong>\#</strong><em>GUID</em> | <em>GUIDFile</em>}</td>
<td><p>指定一个或多个跟踪提供程序。 使用具有<strong>-启动</strong>若要启用用于跟踪会话提供程序。 使用具有<strong>-启用</strong>启用提供程序或更改其<strong>-标志</strong>或<strong>-级别</strong>值。 使用具有<strong>-禁用</strong>来指定要禁用的提供程序。</p>
<p><em>GUID</em>可以指定其中任意一个[控制 GUID](control-guid.md) (跟在数字符号 (<strong>\#</strong>)) 的路径 （可选） 和文件名称的文本文件，例如控制 GUID (.ctl) 文件，或，包含控件的一个或多个跟踪提供程序的 Guid。</p>
<p>如果省略<strong>guid</strong>中的参数<strong>-启动</strong>命令，TraceView 启动[NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)。</p>
</td>
</tr>
</tbody>
</table>

TraceView 将以下子参数的值传递给指定的提供程序：

<table>
<thead>
<tr>
<th>子参数的 guid</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr>
<td><p><strong>-flag</strong> <em>Flag</em></p></td>

<span id="_______-b_______BufferSize______"></span><span id="_______-b_______buffersize______"></span><span id="_______-B_______BUFFERSIZE______"></span> **-b** *BufferSize*   
指定大小，以 kb 为单位，每个缓冲区分配的跟踪会话。 只能用于 **-启动**。

默认值取决于数目的处理器、 物理内存量和中使用的操作系统。

<span id="_______-min_______NumberOfBuffers______"></span><span id="_______-min_______numberofbuffers______"></span><span id="_______-MIN_______NUMBEROFBUFFERS______"></span> **-min** *NumberOfBuffers*   
指定用于存储跟踪消息最初分配的缓冲区数。 只能用于 **-启动**。

默认值取决于数目的处理器、 物理内存量和中使用的操作系统。

<span id="_______-max_______NumberOfBuffers______"></span><span id="_______-max_______numberofbuffers______"></span><span id="_______-MAX_______NUMBEROFBUFFERS______"></span> **-max** *NumberOfBuffers*   
与一起使用时 **-启动**，**的最大**指定为跟踪会话的数据流分配的缓冲区的最大数目。 默认值取决于数目的处理器、 物理内存量和中使用的操作系统。

与一起使用时 **-更新**，**的最大**更改分配为跟踪会话缓冲区的最大数目。

<span id="_______-ft_______FlushTime______"></span><span id="_______-ft_______flushtime______"></span><span id="_______-FT_______FLUSHTIME______"></span> **-ft** *FlushTime*   
与一起使用时 **-启动**， **-ft**指定何种频率，以秒为单位，跟踪消息缓冲区被刷新。 与一起使用时 **-更新**， **-ft**到指定的时间更改的刷新时间。

最小的刷新时间为 1 秒。 默认值为 0 （无强制刷新）。

这强制刷新是补充和跟踪消息缓冲区已满时停止跟踪会话时，会发生自动刷新。

另请参阅： **-刷新**。

<span id="_______-paged______"></span><span id="_______-PAGED______"></span> **-paged**   
用于跟踪消息缓冲区的可分页内存。 默认情况下，事件跟踪使用不可分页的内存缓冲区。 只能用于 **-启动**。

当提供程序时可能会产生大于调度的 IRQL 在跟踪消息的驱动程序不使用此参数\_级别。

在 Windows 2000 中不支持此参数。

<span id="_______-seq_______MaxFileSize______"></span><span id="_______-seq_______maxfilesize______"></span><span id="_______-SEQ_______MAXFILESIZE______"></span> **-seq** *MaxFileSize*   
指定向事件跟踪日志 (.etl) 文件顺序 （在文件尾，停止记录事件） 的日志记录。 只能用于 **-启动**。

*MaxFileSize*以 mb 为单位指定文件的最大大小。 无需*MaxFileSize*值，此参数将被忽略。

顺序日志记录是默认值，但可以使用此参数，若要设置最大文件大小，或使用 **-prealloc**。 如果不提供此参数，则文件大小没有限制。

<span id="_______-cir_______MaxFileSize______"></span><span id="_______-cir_______maxfilesize______"></span><span id="_______-CIR_______MAXFILESIZE______"></span> **-cir** *MaxFileSize*   
指定循环日志记录 （位于文件结尾，记录最早的邮件通过新消息） 在事件跟踪日志 (.etl) 文件。 只能用于 **-启动**。

*MaxFileSize*以 mb 为单位指定文件的最大大小。 无需*MaxFileSize*值，此参数将被忽略。

默认值是按顺序与文件大小没有限制日志记录。

<span id="_______-prealloc______"></span><span id="_______-PREALLOC______"></span> **-prealloc**   
分配它之前保留的事件跟踪日志 (.etl) 文件的空间。 只能用于 **-启动**。

此参数需要 **-seq**或 **-cir**与*MaxFileSize*。 它不是有效，且 **-newfile**。

<p><em>标志</em>表示十进制或十六进制格式中的跟踪提供程序中定义的标志值。 默认值为 0。 从通过 0xFF000000 0x01000000 的值被保留供将来使用。</p>

<p>标志的含义是单独定义的每个跟踪提供程序。 通常情况下，标志表示越来越详细的报告级别。</p>

<p>在中<strong>-启动</strong>命令时，该标志值在跟踪会话中适用于所有跟踪提供程序。 若要为每个跟踪提供程序设置不同的标志，请使用单独<strong>-启用</strong>命令为每个跟踪提供程序。</p>
</td>
</tr>

<tr>
<td>
<p><strong>-level</strong> <em>Level</em></p>
</td>
<td>
<p>指定<a href="trace-level.md" data-raw-source="[trace level](trace-level.md)">跟踪级别</a>中跟踪会话提供程序。 级别确定跟踪提供程序生成的事件。</p>

<p><em>级别</em>表示十进制或十六进制格式的级别值。 默认值为 0。</p>

<p>级别值的含义是单独定义的每个跟踪提供程序。 通常情况下，跟踪级别表示 （信息、 警告或错误） 事件的严重性。</p>

<p>在中<strong>-启动</strong>命令时，级别值在跟踪会话中适用于所有跟踪提供程序。 若要为每个跟踪提供程序设置不同级别，使用单独<strong>-启用</strong>命令为每个跟踪提供程序。</p>
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
<td>指定大小，以 kb 为单位，每个缓冲区分配的跟踪会话。 只能用于<strong>-启动</strong>。
<p>默认值取决于数目的处理器、 物理内存量和中使用的操作系统。</p></td>
</tr>
<tr>
<td><strong>-min</strong> <em>NumberOfBuffers</em></td>
<td>指定用于存储跟踪消息最初分配的缓冲区数。 只能用于<strong>-启动</strong>。
<p>默认值取决于数目的处理器、 物理内存量和中使用的操作系统。</p></td>
</tr>
<tr>
<td><strong>-max</strong> <em>NumberOfBuffers</em></td>
<td>与一起使用时<strong>-启动</strong>，<strong>的最大</strong>指定为跟踪会话的数据流分配的缓冲区的最大数目。 默认值取决于数目的处理器、 物理内存量和中使用的操作系统。
<p>与一起使用时<strong>-更新</strong>，<strong>的最大</strong>更改分配为跟踪会话缓冲区的最大数目。</p></td>
</tr>
<tr>
<td><strong>-ft</strong> <em>FlushTime</em></td>
<td>与一起使用时<strong>-启动</strong>， <strong>-ft</strong>指定何种频率，以秒为单位，跟踪消息缓冲区被刷新。 与一起使用时<strong>-更新</strong>， <strong>-ft</strong>到指定的时间更改的刷新时间。
<p>最小的刷新时间为 1 秒。 默认值为 0 （无强制刷新）。</p>
<p>这强制刷新是补充和跟踪消息缓冲区已满时停止跟踪会话时，会发生自动刷新。</p>
<p>另请参阅： <strong>-刷新</strong>。</p></td>
</tr>
<tr>
<td><strong>-age</strong> <em>AgeLimit</em></td>
<td>与一起使用时<strong>-启动</strong>， <strong>-年龄<strong>指定之前则释放未使用的跟踪缓冲区保留的时间长度 （以分钟为单位）。 与一起使用时<strong>-更新<strong>， <strong>-年龄<strong>更改年龄限制为指定的值。
<p><em>年龄限制</em>指定之前则释放未使用的跟踪缓冲区保留的时间长度 （以分钟为单位）。 默认值为 15 分钟。</p>
<p>此参数是仅在 Windows 2000 中有效。</p></td>
</tr>
<tr>
<td><strong>-paged</strong></td>
<td>用于跟踪消息缓冲区的可分页内存。 默认情况下，事件跟踪使用不可分页的内存缓冲区。 只能用于<strong>-启动</strong>。
<p>当提供程序时可能会产生大于调度的 IRQL 在跟踪消息的驱动程序不使用此参数\_级别。</p>
<p>在 Windows 2000 中不支持此参数。</p></td>
</tr>
<tr>
<td><strong>-seq</strong> <em>MaxFileSize</em></td>
<td>指定向事件跟踪日志 (.etl) 文件顺序 （在文件尾，停止记录事件） 的日志记录。 只能用于<strong>-启动</strong>。
<p><em>MaxFileSize</em>以 mb 为单位指定文件的最大大小。 无需<em>MaxFileSize</em>值，此参数将被忽略。</p>
<p>顺序日志记录是默认值，但可以使用此参数，若要设置最大文件大小，或使用<strong>-prealloc</strong>。 如果不提供此参数，则文件大小没有限制。</p></td>
</tr>
<tr>
<td><strong>-cir</strong> <em>MaxFileSize</em></td>
<td>指定循环日志记录 （位于文件结尾，记录最早的邮件通过新消息） 在事件跟踪日志 (.etl) 文件。 只能用于<strong>-启动</strong>。
<p><em>MaxFileSize</em>以 mb 为单位指定文件的最大大小。 无需<em>MaxFileSize</em>值，此参数将被忽略。</p>
<p>默认值是按顺序与文件大小没有限制日志记录。</p></td>
</tr>
<tr>
<td><strong>-prealloc</strong></td>
<td>分配它之前保留的事件跟踪日志 (.etl) 文件的空间。 只能用于<strong>-启动</strong>。
<p>此参数需要<strong>-seq</strong>或<strong>-cir</strong>与<em>MaxFileSize</em>。 它不是有效，且<strong>-newfile</strong>。</p>
<p>在 Windows XP 和更高版本的系统中，系统会创建事件跟踪日志 (.etl) 文件的大小等于<em>MaxFileSize</em>通过使用指定值<strong>-seq</strong>或<strong>-cir</strong>参数。 在您停止会话后，它可以日志文件减少到其内容的大小。</p></td>
</tr>
<tr>
<td><strong>-newfile</strong> <em>MaxFileSize</em></td>
<td>创建一个新的事件跟踪日志 (.etl) 文件，只要现有文件达到<em>MaxFileSize</em>。 只能用于<strong>-启动</strong>。
<p><em>MaxFileSize</em>以 mb 为单位指定每个日志文件的最大大小。 无需<em>MaxFileSize</em>值，此参数将被忽略。</p>
<p>使用时<strong>-newfile</strong>，则还必须使用<strong>-f</strong> <em>日志文件</em>参数和的值<em>日志文件</em>必须包含一个名称字符<strong>%d</strong>指示十进制模式-例如，trace%d.etl。 否则，该命令将失败，错误\_无效\_名称。 Windows 会创建一个新文件每次递增的十进制值中的文件的名称。</p>
<p>此参数不是有效，且预先分配 (<strong>-prealloc</strong>日志记录 (<strong>-cir</strong>)、 与 NT 内核记录器会话或专用跟踪会话。 在 Windows 2000 中不支持它。</p></td>
</tr>
<tr>
<td><strong>-append</strong></td>
<td>将跟踪消息追加到现有的事件跟踪日志 (.etl) 文件。 默认值是创建一个新的文件。 只能用于<strong>-启动</strong>。
<p>仅在顺序文件和仅当此参数才有效<strong>-f</strong>使用并<strong>-rt</strong>不使用。 在 Windows 2000 中不支持它。</p></td>
</tr>
<tr>
<td><strong>-kd</strong></td>
<td>将跟踪消息重定向到 KD 或的 Windbg 中，附加者为准。 此参数还将跟踪缓冲区大小设置为 3 KB，在调试器中，最大缓冲区大小，并忽略任何<strong>-b</strong>命令中的参数。 只能用于<strong>-启动</strong>。</td>
</tr>
</tbody>
</table>

### <a name="comments"></a>备注

一个**traceview**不带任何参数的命令会打开 TraceView 窗口。

可以使用 TraceView-启动命令来启动[全局记录器跟踪会话](global-logger-trace-session.md)。 为此，请使用以下命令格式。 与其他命令，此命令格式中的"GlobalLogger"一词是区分大小写。

```command
traceview -start GlobalLogger [parameters]
```
