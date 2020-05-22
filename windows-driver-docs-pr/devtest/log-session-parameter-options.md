---
title: 日志会话参数选项
description: 日志会话参数选项
ms.assetid: 5398dfa7-abeb-443b-ab64-73b6599c8e73
keywords:
- 跟踪会话 WDK，高级选项
- 跟踪会话 WDK，日志会话参数选项
- 日志会话参数选项 WDK
- 跟踪标志 WDK
- 标志 WDK 软件跟踪
- 刷新时间 WDK 软件跟踪
- 缓冲 WDK 软件跟踪
- 衰减时间 WDK 软件跟踪
- 循环缓冲 WDK 软件跟踪
- 全局序列号 WDK 软件跟踪
- 跟踪级别 WDK
- 级别 WDK 软件跟踪
- WinDbg WDK 软件跟踪
- 虚拟文件 WDK 软件跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2eca69ddc8790136bc9c26e996dbf989afe25f6
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769637"
---
# <a name="log-session-parameter-options"></a>日志会话参数选项


在 "**日志会话参数选项**" 选项卡中，您可以指定跟踪会话的可变功能的值。

创建跟踪会话时，可以设置和更改以下选项的值。 在运行跟踪会话时，可以更改多个选项。 在 "**日志会话参数选项**" 对话框中，无法更改的选项将显示为灰色（"灰显"）。

<span id="Flags"></span><span id="flags"></span><span id="FLAGS"></span>**随意**  
指定跟踪提供程序的[跟踪标志](trace-flags.md)。 跟踪标志确定提供程序生成的跟踪消息。 标志的含义由每个提供程序单独确定。

如果 TraceView 可以找到提供程序的[跟踪消息控制（tmc）文件](trace-message-control-file.md)，则可以从 "**跟踪标志和级别选择**" 对话框中显示的列表中选择 "标志" 和 "级别"。 若要打开**跟踪标志和级别选择**对话框，请在 "**日志会话参数选项**" 对话框中单击 "**标志**" 或 "**级别**" 选项的**设置**值。

<span id="Flush_Time__S_"></span><span id="flush_time__s_"></span><span id="FLUSH_TIME__S_"></span>**刷新时间**  
指定将跟踪会话缓冲区刷新到跟踪日志或 TraceView 显示的频率（以秒为单位）。 默认值为1（秒）。

除了在缓冲区已满时自动执行的刷新，还会发生这些强制刷新。 值0表示无强制刷新。

若要刷新频率高于每秒一次，请使用 "**缓冲区大小**" 选项来减小每个缓冲区的大小。

可以在运行跟踪会话时更改**刷新时间**值。

<span id="Maximum_Buffers"></span><span id="maximum_buffers"></span><span id="MAXIMUM_BUFFERS"></span>**最大缓冲区**  
指定为跟踪会话分配的最大缓冲区数。

默认值由处理器的数量、物理内存量和你使用的操作系统决定。 可以在运行跟踪会话时更改此值。

<span id="Minimum_Buffers"></span><span id="minimum_buffers"></span><span id="MINIMUM_BUFFERS"></span>**最小缓冲区**  
指定最初为存储跟踪消息分配的缓冲区数。

当缓冲区已满时，将分配更多的缓冲区，直到缓冲区数达到**最大缓冲区**选项中指定的值。 默认值由处理器数量、物理内存量和使用中的操作系统决定。 当跟踪会话正在运行时，不能更改此值。

<span id="Buffer_Size"></span><span id="buffer_size"></span><span id="BUFFER_SIZE"></span>**缓冲区大小**  
指定为跟踪会话分配的每个缓冲区的大小（以 kb 为单位）。 默认值由处理器数量、物理内存量和使用中的操作系统决定。 当跟踪会话正在运行时，不能更改此值。

<span id="Decay_Time__Minutes_"></span><span id="decay_time__minutes_"></span><span id="DECAY_TIME__MINUTES_"></span>**衰减时间（分钟）**  
指定在释放未使用的跟踪缓冲区之前保留多长时间（以分钟为单位）。 默认值为 15。 此选项的值将显示在 "[跟踪会话" 列表](trace-session-list.md)的 " **Age** " 列中。

此参数仅在 Windows 2000 上有效。 当跟踪会话正在运行时，不能更改此值。

<span id="Circular_Buffer_Size__MB_"></span><span id="circular_buffer_size__mb_"></span><span id="CIRCULAR_BUFFER_SIZE__MB_"></span>**循环缓冲区大小（MB）**  
指定跟踪缓冲区为循环，并指定每个缓冲区的最大大小（以 MB 为单位）。

当循环缓冲区已满时，会将新的跟踪消息写入缓冲区的开头，并覆盖最早的跟踪消息。 默认情况下，跟踪缓冲区是连续的，而不是循环的。

当跟踪会话正在运行时，不能更改此值。

<span id="Sequential_Buffer_Size__MB_"></span><span id="sequential_buffer_size__mb_"></span><span id="SEQUENTIAL_BUFFER_SIZE__MB_"></span>**顺序缓冲区大小（MB）**  
指定跟踪缓冲区是否是连续的，并指定每个缓冲区的最大大小（以 MB 为单位）。

当顺序缓冲区已满时，跟踪消息将写入另一个缓冲区或丢失。 默认情况下，跟踪缓冲区是连续的，不是循环的，每个都是 200 MB。

当跟踪会话正在运行时，不能更改此值。

<span id="Start_New_File_After_Buffer_Size__MB_"></span><span id="start_new_file_after_buffer_size__mb_"></span><span id="START_NEW_FILE_AFTER_BUFFER_SIZE__MB_"></span>**在缓冲区大小（MB）后启动新文件**  
只要现有日志达到指定的值，就会创建一个新的跟踪日志文件（.etl）。 该值指定每个日志文件的最大大小（MB）。

此选项的值将显示在 "[跟踪会话" 列表](trace-session-list.md)的 "**新建文件**" 列中。

此选项仅在以下情况下有效：提供程序正在生成跟踪日志，即，在 "**日志会话选项**" 页上选择了 "[日志跟踪事件数据到文件" 选项](basic-trace-session-options.md)。 此选项对来自[NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)的循环缓冲区或日志不起作用。 Windows 2000 不支持此方法。

<span id="Use_Global_Sequence_Numbers"></span><span id="use_global_sequence_numbers"></span><span id="USE_GLOBAL_SEQUENCE_NUMBERS"></span>**使用全局序列号**  
为每个跟踪消息生成全局序列号。

全局序列号对于计算机上的所有跟踪会话都是唯一的。 此选项的默认值为**FALSE**。

Windows 2000 不支持此选项，并且不会影响[NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)中的日志。

<span id="Use_Local_Sequence_Number"></span><span id="use_local_sequence_number"></span><span id="USE_LOCAL_SEQUENCE_NUMBER"></span>**使用本地序列号**  
为每个跟踪消息生成本地序列号。 默认值为**TRUE**。

本地序列号在跟踪会话中是唯一的。

Windows 2000 不支持此选项，并且不会影响[NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)中的日志。

<span id="Level"></span><span id="level"></span><span id="LEVEL"></span>**调配**  
指定跟踪提供程序的[跟踪级别](trace-level.md)。 跟踪级别确定提供程序生成的跟踪消息。 级别值的含义由每个提供程序单独确定。 通常，它表示详细的详细信息级别。

如果 TraceView 可以找到提供程序的[跟踪消息控制（tmc）文件](trace-message-control-file.md)，则可以从 "**跟踪标志和级别选择**" 对话框中显示的列表中选择 "标志" 和 "级别"。 若要打开**跟踪标志和级别选择**对话框，请在 "**日志会话参数选项**" 对话框中单击 "**标志**" 或 "**级别**" 选项的**设置**值。

有关跟踪级别的详细信息，请参阅 Microsoft Windows SDK 中**EnableTrace**函数的*EnableLevel*参数说明。

<span id="WinDbg"></span><span id="windbg"></span><span id="WINDBG"></span>**WinDbg**  
除了在 TraceView 窗口中显示跟踪消息以外，还将跟踪消息重定向到 KD 或 WinDbg。 此选项还会将缓冲区大小设置为 3 KB，即 WinDbg 允许的最大大小。 为 "**缓冲区大小**" 选项显示的值将被忽略。

若要在调试器中显示跟踪消息，wmitrace 和 traceprt 必须在主计算机上的调试器搜索路径中。 这些 Dll 也包含在[Windows 调试工具](https://developer.microsoft.com/windows/hardware/)中，若要使调试器能够查找跟踪消息的[跟踪消息格式（tmf）文件](trace-message-format-file.md)，则 tmf 文件必须在主计算机上的调试器搜索路径中。 若要设置调试器的搜索路径，请使用！ searchpath 专用调试程序扩展或设置% 跟踪 \_ 格式 \_ 搜索 \_ 路径% 环境变量的值。 有关 WinDbg 和 WMI 跟踪扩展的信息，请参阅 Windows 调试工具。

<span id="Ignore_TraceView"></span><span id="ignore_traceview"></span><span id="IGNORE_TRACEVIEW"></span>**忽略 TraceView**  
禁止 TraceView 操作导致的跟踪消息。

<span id="Virtual_File_Size"></span><span id="virtual_file_size"></span><span id="VIRTUAL_FILE_SIZE"></span>**虚拟文件大小**  
指示 TraceView 在开始覆盖最旧的消息之前存储的跟踪消息的最大数目，以便为较新的消息腾出空间。

值**0**表示没有最大值。 TraceView 保留所有消息，并且永远不会覆盖它们。 此选项的默认值**65536**是建议用于大多数系统的值。 较大的值可能导致明显的延迟。

此值出现在 "[跟踪会话" 列表](trace-session-list.md)的 "**最大跟踪记录**" 列中。

 

 





