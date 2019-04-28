---
title: 全局记录器跟踪会话
description: 全局记录器跟踪会话
ms.assetid: d78ce5d8-a9f3-47d6-be7a-eeaeacd7b872
keywords:
- 跟踪会话 WDK，全局记录器
- 有关全局记录器会话全局记录器跟踪会话 WDK，
- 全局记录器跟踪会话 WDK，注册表项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c256324de636d8cb467d88b02b89972da967a1a6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329697"
---
# <a name="global-logger-trace-session"></a>全局记录器跟踪会话

一个*全局记录器跟踪会话*记录之前的系统是完全可操作，如事件生成的设备驱动程序在启动过程中发生的事件。 它是内置于 Windows 的保留的跟踪会话。

始终全局记录器跟踪会话将消息写入跟踪日志。 全局记录器不支持实时跟踪会话或缓冲跟踪会话。

全局记录器必须提前在操作系统启动过程中可用，因为它已启动并使用注册表项配置 (在**HKLM\\系统\\CurrentControlSet\\控件\\WMI\\GlobalLogger**子项)，而不是函数调用。 启动后，全局记录器的行为类似于常规的事件跟踪会话。

全局记录器跟踪会话使用保留的会话名称，"GlobalLogger。" [控制 GUID](control-guid.md)常量，表示**GlobalLoggerGuid**。 创建全局记录器跟踪会话，重启计算机以启动跟踪会话。 只有一个全局记录器跟踪会话一次在计算机上运行。

若要创建全局记录器跟踪会话，请使用[Tracelog](tracelog.md)。 它会自动创建的注册表子项和存储跟踪会话选项的条目。 全局记录器跟踪会话启动时重新启动计算机。 有关详细信息，请参阅[ **Tracelog 命令语法**](tracelog-command-syntax.md)。

若要设置格式从全局记录器跟踪会话的跟踪消息，请使用[Tracefmt](tracefmt.md) system.tmf，与[跟踪消息格式文件](trace-message-format-file.md)WDK 中包含。

全局记录器会话由注册表项触发，因为它运行每个项在注册表中的显示的时间。 若要防止全局记录器会话启动每次系统启动时，将设置的值**启动**条目为 0 或删除所有注册表项。

您可以将转换全局记录器跟踪会话到 NT 内核记录器跟踪会话，从而在启动过程期间跟踪内核。 有关信息，请参阅[启动时全局记录器会话](boot-time-global-logger-session.md)

[跟踪提供程序](trace-provider.md)，如内核模式驱动程序和用户模式应用程序，可以将记录到全局记录器跟踪会话。 这使您可以在系统启动期间跟踪驱动程序或其他跟踪提供程序。 有关信息，请参阅[到全局记录器会话日志记录](logging-to-the-global-logger-session.md)

## <a name="limitations-of-the-global-logger-trace-session"></a>全局记录器跟踪会话的限制

全局记录器跟踪会话是非常有用，但务必要了解其限制：

你可以一次运行只有一个全局记录器会话。

全局记录器会话不会发送启用提供程序的通知。

全局记录器注册表项保留在注册表中，将生效，直到你将重置或手动，将其删除或使用**tracelog-删除**命令。 重置密码，直到全局记录器会话每次启动启动系统。

全局记录器跟踪会话永久启用 Windows ACPI 记录器。 来自此记录器的跟踪消息显示在跟踪日志。

如果标准跟踪会话启动时驱动程序记录到全局记录器会话，则驱动程序将切换，并启动到标准跟踪会话的日志记录。

## <a name="global-logger-registry-entries"></a>全局记录器注册表项

下表显示了配置全局记录器会话的注册表项。 这些条目位于**HKLM\\系统\\CurrentControlSet\\控制\\WMI\\GlobalLogger**子项。 仅**启动**项是必需的。

除了此表中的注册表条目，还可以添加**ControlGUID**子项下**GlobalLogger**子项来表示跟踪提供程序，如驱动程序，在日志中记录为全局记录器跟踪会话。 有关信息，请参阅[记录到全局记录器会话](logging-to-the-global-logger-session.md)。

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
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>开始</strong></p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p>如果设置为<strong>1</strong> （开），在全局记录器会话启动在下次系统启动的时。</p>
<p><strong>0</strong> = 关闭; <strong>1</strong>= on</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>BufferSize</strong></p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p>指定的大小 （以 kb 为单位） 的每个缓冲区。 默认值为 0x40 (64 KB)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ClockType</strong></p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p>指定用于跟踪消息时间戳的计时器。</p>
<p>从 Windows Vista 开始，默认值是<strong>1</strong>。 在 Windows Vista 之前的操作系统，默认值是<strong>2</strong>。</p>
<p><strong>1</strong> = 性能计数器的值 （高分辨率）</p>
<p><strong>2</strong> = 系统计时器</p>
<p><strong>3</strong> = CPU 周期时钟</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>EnableKernelFlags</strong></p></td>
<td align="left"><p>REG_BINARY</p></td>
<td align="left"><p>将全局记录器会话转换为 NT 内核记录器跟踪会话，并指定内核跟踪中包含的事件。</p>
<p>有关信息，请参阅<a href="boot-time-global-logger-session.md" data-raw-source="[Boot-time Global Logger Session](boot-time-global-logger-session.md)">启动时全局记录器会话</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileCounter</strong></p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p>存储由全局记录器会话生成的事件跟踪日志文件数。</p>
<p>系统增加此值，直到它达到的值<strong>FileMax</strong>。 然后，它将重置值为 0。</p>
<p>此计数器可阻止系统覆盖全局记录器跟踪日志文件。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileMax</strong></p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p>指定的最大允许在系统上的事件跟踪日志文件数。</p>
<p>当跟踪日志的数量达到指定的最大值时，系统将开始覆盖从最旧的日志。</p>
<p>默认值为 0，这意味着没有最大值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileName</strong></p></td>
<td align="left"><p>REG_SZ</p></td>
<td align="left"><p>（可选） 的路径和事件跟踪日志文件的文件名。 默认值为 %systemroot%\system32\logfiles\wmi\trace.log。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FlushTimer</strong></p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p>指定频率 （以秒为单位） 强制刷新缓冲区的跟踪。 强制刷新其中不包括缓冲区已满时，停止跟踪会话时就会发生自动刷新。</p>
<p>默认值为 0。 默认情况下，仅当他们已满时刷新缓冲区。</p>
<p>最小的刷新时间为 1 秒。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>LogFileMode</strong></p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p>指定日志会话选项。</p>
<p>仅在 Windows Vista 和更高版本的 Windows 中支持。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MaximumBuffers</strong></p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p>指定可分配给会话的缓冲区的最大数目。 默认值为 0x19 (25)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MaximumFileSize</strong></p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p>指定事件跟踪日志文件的最大大小。 默认情况下，没有最大文件大小。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MinimumBuffers</strong></p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p>指定在会话启动时分配的缓冲区数。 默认值为 0x3。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>状态</strong></p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p>将存储在尝试启动全局记录器跟踪会话的返回代码。</p>
<p>如果在会话启动失败，则此项的值是 Win32 错误代码。 如果在会话启动，则此项的值为 ERROR_SUCCESS。</p></td>
</tr>
</tbody>
</table>

 

创建这些注册表项保留在注册表中，生效之前将其删除或更改它们的值。 因此，运行全局记录器会话后，使用**tracelog-删除 GlobalLogger**命令设置的值**启动**为 0 的条目和删除其他全局记录器的注册表项。 否则，全局记录器会话运行每次重新启动计算机，并生成的日志文件可以变得很大。

## <a name="logging-mode-constants"></a>日志记录模式常量

下表显示的有效值**LogFileMode**中的注册表条目**HKLM\\系统\\CurrentControlSet\\控制\\WMI\\GlobalLogger**子项。 此项用于设置全局记录器跟踪会话，其中包含用于实时跟踪会话、 专用跟踪会话、 循环日志记录和缓冲 （无日志） 选项。 仅在 Windows Vista 和更高版本的 Windows 中支持此注册表项。

此注册表项对应于**LogFileMode**的事件成员\_跟踪\_属性结构。 其值对应于日志记录模式常量。 事件\_跟踪\_Microsoft Windows SDK 文档中所述属性结构和日志记录模式常量。

此处显示此表以显示十六进制常量的值。 使用这些值或这些值的总和来表示中的常量**LogFileMode**注册表项。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">值</th>
<th align="left">Constant</th>
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
<td align="left"><p>将跟踪消息添加到现有日志文件。 此模式是仅对于顺序文件有效。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x8</p></td>
<td align="left"><p>EVENT_TRACE_FILE_MODE_NEWFILE</p></td>
<td align="left"><p>每当在现有文件达到的值都要创建新的事件跟踪日志文件<strong>MaximumFileSize</strong>条目 （请参阅上表）。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x20</p></td>
<td align="left"><p>EVENT_TRACE_FILE_MODE_PREALLOCATE</p></td>
<td align="left"><p>事件跟踪日志文件的保留空间。</p>
<p>仅对于 EVENT_TRACE_FILE_MODE_SEQUENTIAL 或 EVENT_TRACE_FILE_MODE_CIRCULAR，有效和无效 EVENT_TRACE_FILE_MODE_NEWFILE 使用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x40</p></td>
<td align="left"><p>EVENT_TRACE_NONSTOPPABLE_MODE</p></td>
<td align="left"><p>调用<strong>StopTrace</strong>不会停止跟踪会话。</p>
<p>此功能可阻止用户停止跟踪会话的系统要求以进行诊断和优化。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x100</p></td>
<td align="left"><p>EVENT_TRACE_REAL_TIME_MODE</p></td>
<td align="left"><p>指定实时跟踪会话。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x200</p></td>
<td align="left"><p>EVENT_TRACE_DELAY_OPEN_FILE_MODE</p></td>
<td align="left"><p>仅供内部使用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x400</p></td>
<td align="left"><p>EVENT_TRACE_BUFFERING_MODE</p></td>
<td align="left"><p>事件保留在缓冲区中。 它们永远不会写入日志文件或传递到跟踪使用者。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x800</p></td>
<td align="left"><p>EVENT_TRACE_PRIVATE_LOGGER_MODE</p></td>
<td align="left"><p>指定的专用跟踪会话。 此标志不是有效的全局记录器跟踪会话。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1000</p></td>
<td align="left"><p>EVENT_TRACE_ADD_HEADER_MODE</p></td>
<td align="left"><p>仅供内部使用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2000</p></td>
<td align="left"><p>EVENT_TRACE_USE_KBYTES_FOR_SIZE</p></td>
<td align="left"><p>将的值解释<strong>MaximumFileSize</strong>以 kb 为单位，而不是 MB。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x4000</p></td>
<td align="left"><p>EVENT_TRACE_USE_GLOBAL_SEQUENCE</p></td>
<td align="left"><p>生成跟踪消息的全局序列的号。 在计算机上的所有跟踪会话，这些数字都是唯一的。</p>
<p>默认情况下，跟踪消息不具有任何序列号。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x8000</p></td>
<td align="left"><p>EVENT_TRACE_USE_LOCAL_SEQUENCE</p></td>
<td align="left"><p>生成跟踪消息的本地序列的号。 这些数字跟踪会话中是唯一的。</p>
<p>默认情况下，跟踪消息不具有任何序列号。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10000</p></td>
<td align="left"><p>EVENT_TRACE_RELOG_MODE</p></td>
<td align="left"><p>仅供内部使用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x80000</p></td>
<td align="left"><p>EVENT_TRACE_KD_FILTER_MODE</p></td>
<td align="left"><p>将跟踪消息重定向到内核调试程序并设置跟踪缓冲区大小为 3KB，调试程序的最大缓冲区大小。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1000000</p></td>
<td align="left"><p>EVENT_TRACE_MODE_RESERVED</p></td>
<td align="left"><p>对全局记录器跟踪会话无效。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x01000000</p></td>
<td align="left"><p>EVENT_TRACE_USE_PAGED_MEMORY</p></td>
<td align="left"><p>从可分页内存的会话缓冲区分配跟踪。 默认情况下，是从不可分页的内存中分配缓冲区。</p></td>
</tr>
</tbody>
</table>
 





