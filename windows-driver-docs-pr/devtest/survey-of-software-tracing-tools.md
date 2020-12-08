---
title: 软件跟踪工具调查
description: 软件跟踪工具调查
keywords:
- 软件跟踪 WDK，列出的工具
- 跟踪 WDK，列出的工具
- 添加跟踪
- 软件跟踪 WDK，添加
- 跟踪 WDK，添加
- 软件跟踪 WDK，控制会话
- 跟踪 WDK，控制会话
- 软件跟踪 WDK，TMF 文件
- 跟踪 WDK，TMF 文件
- 软件跟踪 WDK，设置消息格式
- 跟踪 WDK，设置消息格式
- 软件跟踪 WDK，显示消息
- 跟踪 WDK，显示消息
- 软件跟踪 WDK，查看事件
- 跟踪 WDK，查看事件
- 跟踪使用者 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a24a1c7c071df9b3b5c5b4b109a9bf0448b5312f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791901"
---
# <a name="survey-of-software-tracing-tools"></a>软件跟踪工具调查

以下软件跟踪工具包含在 Windows 驱动程序工具包 (WDK) 或 Windows 操作系统中。

## <a name="span-idenabling_wpp__tracing_in_a_trace_producerspanspan-idenabling_wpp__tracing_in_a_trace_producerspanenabling-wpp-tracing-in-a-trace-producer"></a><span id="enabling_wpp__tracing_in_a_trace_producer"></span><span id="ENABLING_WPP__TRACING_IN_A_TRACE_PRODUCER"></span>在跟踪生成方中启用 WPP 跟踪

-   TraceWPP ( # A0) 是一个命令行工具，可在 [跟踪提供](trace-provider.md)程序的源文件（如内核模式驱动程序或用户模式应用程序）上运行 Windows 软件跟踪预处理器 (WPP) 。

    使用 WDK 和 Visual Studio 构建驱动程序或应用程序时，TraceWPP 提供了一种替代方法，用于设置 WPP 选项。 此工具可处理源文件中的跟踪宏，并创建标头文件以启用 WPP 跟踪。

    TraceWPP 的命令行选项与将 [TraceWPP 任务](tracewpp-task.md) 传递到 MSBuild 时使用的选项相同。 有关这些选项的详细信息，请参阅 [WPP 预处理器](wpp-preprocessor.md)。

    TraceWPP 位于 WDK 的 bin \\ &lt; *平台* &gt; 目录中。

## <a name="span-idcontrolling_trace_sessions__trace_controllers_spanspan-idcontrolling_trace_sessions__trace_controllers_spancontrolling-trace-sessions-trace-controllers"></a><span id="controlling_trace_sessions__trace_controllers_"></span><span id="CONTROLLING_TRACE_SESSIONS__TRACE_CONTROLLERS_"></span>控制跟踪会话 (跟踪控制器) 

-   [TraceView](traceview.md) ( # A0) 是基于 GUI 的 [跟踪控制器](trace-controller.md) 和 [跟踪使用者](trace-consumer.md)，专为跟踪消息的实时显示而设计。 它启用、配置、启动、更新和停止 [跟踪会话](trace-session.md)。 此工具还会设置、筛选和显示实时跟踪会话和 [跟踪日志](trace-log.md)中的跟踪消息。

    TraceView 结合和扩展了 [Tracepdb](tracepdb.md)、 [Tracelog](tracelog.md)和 [Tracefmt](tracefmt.md)的功能。 有关信息，请启动 TraceView，然后在 " **帮助** " 菜单中选择 " **帮助主题**"。

    TraceView 位于 WDK 的工具 \\ &lt; *平台* &gt; 子目录中，其中 &lt; *平台* &gt; 为 x86 或 x64。

-   [Tracelog](tracelog.md) ( # A0) 是一个命令行 [跟踪控制器](trace-controller.md) ，用于启用、配置、启动、更新和停止实时和日志会话。 Tracelog 支持用户模式和内核模式跟踪会话，以及 [NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md) 和 [全局记录器 (boot) trace 会话](global-logger-trace-session.md)。 此工具还支持跟踪，以测量 (Dpc) 和中断服务例程 (Isr) 的延迟过程调用所用的时间。

    Tracelog 位于 WDK 的工具 \\ &lt; *平台* &gt; 子目录中，其中 &lt; *平台* &gt; 为 x86 或 x64。

-   Logman ( # A0) 是一个功能齐全的、基于 GUI 的 [跟踪控制器](trace-controller.md) ，专用于控制性能计数器和事件跟踪的日志记录。

    Logman 包含在 Windows XP 和更高版本的 Windows 中。 有关如何使用此工具的详细信息，请参阅 [Logman](/windows-server/administration/windows-commands/logman)。

## <a name="span-idcreating_tmf_filesspanspan-idcreating_tmf_filesspancreating-tmf-files"></a><span id="creating_tmf_files"></span><span id="CREATING_TMF_FILES"></span>创建 TMF 文件

-   [Tracepdb](tracepdb.md) ( # A0) 是一种命令行支持工具，可从[PDB 符号文件](pdb-symbol-files.md)中的跟踪消息格式设置指令[ (TMF) 文件创建跟踪消息格式](trace-message-format-file.md)。

    显示跟踪消息 [Tracefmt](tracefmt.md) ( # A0) 和 [TraceView](traceview.md) ( # A1) 的工具可以使用 TMF 文件中的格式设置指令来格式化和显示跟踪消息。

    Tracefmt 还可以从 [PDB 符号文件](pdb-symbol-files.md)创建 TMF 文件。

    Tracepdb 和 Tracefmt 位于 WDK 的 tools \\ 跟踪 \\ &lt; *平台* &gt; 子目录中，其中 &lt; *平台* &gt; 为 x86 或 x64。

## <a name="span-idformatting_and_displaying_trace_messages__trace_consumers_spanspan-idformatting_and_displaying_trace_messages__trace_consumers_spanformatting-and-displaying-trace-messages-trace-consumers"></a><span id="formatting_and_displaying_trace_messages__trace_consumers_"></span><span id="FORMATTING_AND_DISPLAYING_TRACE_MESSAGES__TRACE_CONSUMERS_"></span>格式设置和显示跟踪消息 (跟踪使用者) 

-   [Tracefmt](tracefmt.md) 是一个命令行 [跟踪使用者](trace-consumer.md) ，它将 *跟踪消息* (**TraceMessage**) 设置为实时跟踪会话或跟踪日志，并将它们写入文件或在命令提示符窗口中显示它们。

-   Tracerpt ( # A0) 是一个命令行 [跟踪使用者](trace-consumer.md) ，它将 *跟踪事件* 的格式设置 (**TraceEvent**) 和性能计数器，并将这些事件写入 CSV 或 XML 文件。 它还分析事件并生成摘要报告。

    Tracerpt 包含在 Windows XP 和更高版本的 Windows 中。 有关如何使用此工具的详细信息，请参阅 [Tracerpt](/windows-server/administration/windows-commands/tracerpt_1)。

-   [TraceView](traceview.md)是一种 GUI 工具，它是跟踪控制器和跟踪使用者，还会设置和显示跟踪消息 (**TraceMessage**) 从实时跟踪会话或跟踪日志。 它以表格形式显示跟踪消息，使其更易于筛选和浏览。

## <a name="span-idviewing_trace_events_in_a_debuggerspanspan-idviewing_trace_events_in_a_debuggerspanviewing-trace-events-in-a-debugger"></a><span id="viewing_trace_events_in_a_debugger"></span><span id="VIEWING_TRACE_EVENTS_IN_A_DEBUGGER"></span>在调试器中查看跟踪事件

-   适用于 Windows 的调试工具包含 **！ wmitrace**，这是一个专用的调试器扩展，它在将跟踪消息写入日志文件或传递以供显示之前，在跟踪会话缓冲区中显示跟踪消息。

-   [Tracelog](tracelog.md) 和 [TraceView](traceview.md) 可将跟踪消息重定向到 KD 或 Windbg，无论附加哪个。 有关详细信息，请参阅 Tracelog **-kd** 参数和 TraceView **Windbg** 选项。

## <a name="span-idanalyzing_dpc_and_isr_execution_timesspanspan-idanalyzing_dpc_and_isr_execution_timesspananalyzing-dpc-and-isr-execution-times"></a><span id="analyzing_dpc_and_isr_execution_times"></span><span id="ANALYZING_DPC_AND_ISR_EXECUTION_TIMES"></span>分析 DPC 和 ISR 执行时间

-   在 Windows XP Service Pack 2 (SP2) 和更高版本中，你可以使用 [Tracelog](tracelog.md) 在 NT 内核记录器跟踪会话中记录延迟的过程调用 (DPC) 和中断服务例程 (ISR) 事件，然后使用 Tracerpt 从日志创建汇总报表。 有关如何使用此工具的详细信息（包括示例），请参阅 Tracelog。

 

