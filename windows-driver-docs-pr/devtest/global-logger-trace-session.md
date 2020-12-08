---
title: 全局记录器跟踪会话
description: 全局记录器跟踪会话
keywords:
- 跟踪会话 WDK，全局记录器
- 全局记录器跟踪会话 WDK，关于全局记录器会话
- 全局记录器跟踪会话 WDK，注册表项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6366d541d14dd8c377c652811a84c05667dd88b7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831571"
---
# <a name="global-logger-trace-session"></a>全局记录器跟踪会话

*全局记录器跟踪会话* 记录在系统完全操作之前在启动过程中发生的事件，例如设备驱动程序生成的事件。 它是内置于 Windows 中的保留跟踪会话。

全局记录器跟踪会话始终将消息写入跟踪日志。 全局记录器不支持实时跟踪会话或缓冲跟踪会话。

因为在操作系统启动过程中，全局记录器必须在早期可用，所以它是通过使用 **HKLM \\ system \\ CurrentControlSet \\ Control \\ WMI \\ GlobalLogger**) 子项中 (的注册表项（而不是函数调用）来启动和配置的。 启动后，全局记录器的行为类似于常规事件跟踪会话。

全局记录器跟踪会话使用保留的会话名称 "GlobalLogger"。 [控件 GUID](control-guid.md)由常量 **GlobalLoggerGuid** 表示。 您将创建一个全局记录器跟踪会话，然后重新启动计算机以启动跟踪会话。 一次只能在计算机上运行一个全局记录器跟踪会话。

若要创建全局记录器跟踪会话，请使用 [Tracelog](tracelog.md)。 它会自动创建用于存储跟踪会话选项的注册表子项和项。 重新启动计算机时，将启动全局记录器跟踪会话。 有关详细信息，请参阅 [**Tracelog 命令语法**](tracelog-command-syntax.md)。

若要从全局记录器跟踪会话设置跟踪消息的格式，请将 [Tracefmt](tracefmt.md) 与 tmf （一种 [跟踪消息格式文件](trace-message-format-file.md) ）结合使用。

由于注册表项会触发全局记录器会话，因此它会在每次项出现在注册表中时运行。 若要防止全局记录器会话在系统每次启动时都启动，请将 **开始** 项的值设置为0或删除所有注册表项。

可以将全局记录器跟踪会话转换为 NT 内核记录器跟踪会话，从而在启动过程中跟踪内核。 有关信息，请参阅 [启动时全局记录器会话](boot-time-global-logger-session.md)

[跟踪提供](trace-provider.md)程序（如内核模式驱动程序和用户模式应用程序）可以记录到全局记录器跟踪会话中。 这使您可以在系统启动期间跟踪驱动程序或其他跟踪提供程序。 有关信息，请参阅 [日志记录到全局记录器会话](logging-to-the-global-logger-session.md)

## <a name="limitations-of-the-global-logger-trace-session"></a>全局记录器跟踪会话的限制

全局记录器跟踪会话非常有用，但请务必注意其局限性：

一次只能运行一个全局记录器会话。

全局记录器会话不会将启用通知发送到提供程序。

全局记录器注册表项保留在注册表中并且有效，直到您手动重置或删除它们，或使用 **tracelog** 命令。 在重置它们之前，每次启动系统时都会启动全局记录器会话。

为全局记录器跟踪会话永久启用 Windows ACPI 记录器。 此记录器中的跟踪消息显示在跟踪日志中。

如果在将驱动程序日志记录到全局记录器会话时启动标准跟踪会话，驱动程序将切换并开始记录到标准跟踪会话。

## <a name="global-logger-registry-entries"></a>全局记录器注册表项

下表显示了配置全局记录器会话的注册表项。 这些条目位于 **HKLM \\ SYSTEM \\ CurrentControlSet \\ Control \\ WMI \\ GlobalLogger** 子项中。 只有 **开始** 项是必需的。

除了此表中的注册表项，还可以在 **GlobalLogger** 子项下添加 **ControlGUID** 子项，以表示日志记录到全局记录器跟踪会话的跟踪提供程序（如驱动程序）。 有关信息，请参阅 [日志记录到全局记录器会话](logging-to-the-global-logger-session.md)。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">条目</th>
<th align="left">数据类型</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>启动</strong></p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p>如果设置为 () 上的 " <strong>1</strong> "，则在系统下一次启动时，全局记录器会话将启动。</p>
<p><strong>0</strong> = 关闭， <strong>1</strong>= 开</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>BufferSize</strong></p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p>指定每个缓冲区 (大小（KB) ）。 默认值为 0x40 (64 KB) 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ClockType</strong></p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p>指定用于跟踪消息时间戳的计时器。</p>
<p>从 Windows Vista 开始，默认值为 <strong>1</strong>。 在 Windows Vista 之前的操作系统上，默认值为 <strong>2</strong>。</p>
<p><strong>1</strong> = 性能计数器值 (高分辨率) </p>
<p><strong>2</strong> = 系统计时器</p>
<p><strong>3</strong> = CPU 循环时钟</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>EnableKernelFlags</strong></p></td>
<td align="left"><p>REG_BINARY</p></td>
<td align="left"><p>将全局记录器会话转换为 NT 内核记录器跟踪会话，并指定内核跟踪中包含的事件。</p>
<p>有关信息，请参阅 <a href="boot-time-global-logger-session.md" data-raw-source="[Boot-time Global Logger Session](boot-time-global-logger-session.md)">启动时全局记录器会话</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileCounter</strong></p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p>存储由全局记录器会话生成的事件跟踪日志文件数。</p>
<p>系统会递增此值，直到达到 <strong>FileMax</strong>的值。 然后，将该值重置为0。</p>
<p>此计数器阻止系统覆盖全局记录器跟踪日志文件。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileMax</strong></p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p>指定系统允许的事件跟踪日志文件的最大数目。</p>
<p>当跟踪日志的数目达到指定的最大值时，系统会开始覆盖最旧的日志。</p>
<p>默认值为0，表示没有最大值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileName</strong></p></td>
<td align="left"><p>REG_SZ</p></td>
<td align="left"><p>路径 (事件跟踪日志文件的可选) 和文件名。 默认值为%SystemRoot%\System32\LogFiles\WMI\trace.log。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FlushTimer</strong></p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p>指定强制刷新跟踪缓冲区)  (的频率（以秒为单位）。 此强制刷新是除了当缓冲区已满时和跟踪会话停止时发生的自动刷新之外的。</p>
<p>默认值为 0。 默认情况下，仅当缓冲区已满时才对其进行刷新。</p>
<p>最小刷新时间为1秒。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>LogFileMode</strong></p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p>指定日志会话选项。</p>
<p>仅在 windows Vista 和更高版本的 Windows 中受支持。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MaximumBuffers</strong></p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p>指定可为会话分配的最大缓冲区数。 默认值为 0x19 (25) 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MaximumFileSize</strong></p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p>指定事件跟踪日志文件的最大大小。 默认情况下，没有最大文件大小。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MinimumBuffers</strong></p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p>指定在会话启动时所分配的缓冲区数。 默认值为0x3。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>状态</strong></p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p>存储尝试启动全局记录器跟踪会话的返回代码。</p>
<p>如果会话无法启动，则此项的值为 Win32 错误代码。 如果会话已启动，则 ERROR_SUCCESS 此项的值。</p></td>
</tr>
</tbody>
</table>

 

你创建的这些注册表项将保留在注册表中，并在删除它们或更改其值之前有效。 因此，在全局记录器会话运行之后，使用 **tracelog-Remove GlobalLogger** 命令将 **Start** 条目的值设置为0，并删除其他全局记录器注册表项。 否则，每次重新启动计算机时都将运行全局记录器会话，并且生成的日志文件可能会变得非常大。

## <a name="logging-mode-constants"></a>记录模式常量

下表显示 **HKLM \\ System \\ CurrentControlSet \\ Control \\ WMI \\ GlobalLogger** 子项中的 **LogFileMode** 注册表项的有效值。 此条目用于设置全局记录器跟踪会话的选项，其中包括用于实时跟踪会话、专用跟踪会话、循环日志记录和缓冲 (没有日志) 的选项。 只有 Windows Vista 和更高版本的 Windows 支持此注册表项。

此注册表项与事件 **LogFileMode** \_ 跟踪属性结构的 LogFileMode 成员相对应 \_ 。 其值对应于日志记录模式常量。 \_ \_ Microsoft Windows SDK 文档中介绍了事件跟踪属性结构和日志记录模式常量。

此处显示了此表，显示常量的十六进制值。 使用这些值或这些值的和，在 **LogFileMode** 注册表项中表示常量。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">“值”</th>
<th align="left">返回的常量</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x0</p></td>
<td align="left"><p>EVENT_TRACE_FILE_MODE_NONE</p></td>
<td align="left"><p>不创建任何事件跟踪日志文件。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1</p></td>
<td align="left"><p>EVENT_TRACE_FILE_MODE_SEQUENTIAL</p></td>
<td align="left"><p>事件跟踪日志文件是连续的。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2</p></td>
<td align="left"><p>EVENT_TRACE_FILE_MODE_CIRCULAR</p></td>
<td align="left"><p>事件跟踪日志文件是循环的。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x4</p></td>
<td align="left"><p>EVENT_TRACE_FILE_MODE_APPEND</p></td>
<td align="left"><p>将跟踪消息追加到现有日志文件。 此模式仅对顺序文件有效。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x8</p></td>
<td align="left"><p>EVENT_TRACE_FILE_MODE_NEWFILE</p></td>
<td align="left"><p>每当现有文件达到 <strong>MaximumFileSize</strong> 项的值时创建新的事件跟踪日志文件 (参阅上表) 。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x20</p></td>
<td align="left"><p>EVENT_TRACE_FILE_MODE_PREALLOCATE</p></td>
<td align="left"><p>为事件跟踪日志文件保留空间。</p>
<p>仅对 EVENT_TRACE_FILE_MODE_SEQUENTIAL 或 EVENT_TRACE_FILE_MODE_CIRCULAR 有效，对 EVENT_TRACE_FILE_MODE_NEWFILE 无效。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x40</p></td>
<td align="left"><p>EVENT_TRACE_NONSTOPPABLE_MODE</p></td>
<td align="left"><p>对 <strong>StopTrace</strong> 的调用不会停止跟踪会话。</p>
<p>此功能可防止用户停止系统需要进行诊断和优化的跟踪会话。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x100</p></td>
<td align="left"><p>EVENT_TRACE_REAL_TIME_MODE</p></td>
<td align="left"><p>指定实时跟踪会话。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x200</p></td>
<td align="left"><p>EVENT_TRACE_DELAY_OPEN_FILE_MODE</p></td>
<td align="left"><p>仅限内部使用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x400</p></td>
<td align="left"><p>EVENT_TRACE_BUFFERING_MODE</p></td>
<td align="left"><p>事件保留在缓冲区中。 它们永远不会写入日志文件或传递给跟踪使用者。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x800</p></td>
<td align="left"><p>EVENT_TRACE_PRIVATE_LOGGER_MODE</p></td>
<td align="left"><p>指定专用跟踪会话。 此标志对于全局记录器跟踪会话无效。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1000</p></td>
<td align="left"><p>EVENT_TRACE_ADD_HEADER_MODE</p></td>
<td align="left"><p>仅限内部使用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2000</p></td>
<td align="left"><p>EVENT_TRACE_USE_KBYTES_FOR_SIZE</p></td>
<td align="left"><p>解释 <strong>MaximumFileSize</strong> 的值（以 KB 为单位），而不是以 MB 为单位。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x4000</p></td>
<td align="left"><p>EVENT_TRACE_USE_GLOBAL_SEQUENCE</p></td>
<td align="left"><p>为跟踪消息生成全局序列号。 这些数字对于计算机上的所有跟踪会话都是唯一的。</p>
<p>默认情况下，跟踪消息不具有任何序列号。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x8000</p></td>
<td align="left"><p>EVENT_TRACE_USE_LOCAL_SEQUENCE</p></td>
<td align="left"><p>为跟踪消息生成本地序列号。 这些数字在跟踪会话中是唯一的。</p>
<p>默认情况下，跟踪消息不具有任何序列号。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10000</p></td>
<td align="left"><p>EVENT_TRACE_RELOG_MODE</p></td>
<td align="left"><p>仅限内部使用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x80000</p></td>
<td align="left"><p>EVENT_TRACE_KD_FILTER_MODE</p></td>
<td align="left"><p>将跟踪消息重定向到内核调试器，并将跟踪缓冲区大小设置为 3 KB，即调试器的最大缓冲区大小。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1000000</p></td>
<td align="left"><p>EVENT_TRACE_MODE_RESERVED</p></td>
<td align="left"><p>对于全局记录器跟踪会话无效。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x01000000</p></td>
<td align="left"><p>EVENT_TRACE_USE_PAGED_MEMORY</p></td>
<td align="left"><p>从可分页内存中分配跟踪会话缓冲区。 默认情况下，从不可分页内存分配缓冲区。</p></td>
</tr>
</tbody>
</table>
 





