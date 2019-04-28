---
title: 软件跟踪工具调查
description: 软件跟踪工具调查
ms.assetid: d6b5d131-ed03-4961-9680-1c4ded35de96
keywords:
- 软件跟踪 WDK，列出工具
- 跟踪 WDK，列出工具
- 将跟踪添加
- 软件跟踪 WDK，添加
- 跟踪 WDK，添加
- 软件跟踪 WDK，控制会话
- 跟踪 WDK，控制会话
- 软件跟踪 WDK，TMF 文件
- 跟踪 WDK，TMF 文件
- 软件跟踪 WDK、 设置消息格式
- 跟踪 WDK，设置消息格式
- 软件跟踪 WDK、 显示消息
- 跟踪 WDK，显示消息
- 软件跟踪 WDK、 查看事件
- 跟踪 WDK、 查看事件
- 跟踪使用者 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b61d157a36319926691e98acba80ca3e2bb05e74
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347614"
---
# <a name="survey-of-software-tracing-tools"></a>软件跟踪工具调查


## <span id="ddk_survey_of_software_tracing_tools_tools"></span><span id="DDK_SURVEY_OF_SOFTWARE_TRACING_TOOLS_TOOLS"></span>


Windows Driver Kit (WDK) 或 Windows 操作系统中包含以下软件跟踪工具。

### <a name="span-idenablingwpptracinginatraceproducerspanspan-idenablingwpptracinginatraceproducerspanenabling-wpp-tracing-in-a-trace-producer"></a><span id="enabling_wpp__tracing_in_a_trace_producer"></span><span id="ENABLING_WPP__TRACING_IN_A_TRACE_PRODUCER"></span>启用 WPP 跟踪中跟踪生成者

-   TraceWPP (TraceWPP.exe) 是一个命令行工具，运行 Windows 软件跟踪预处理器 (WPP) 上的源文件[跟踪提供程序](trace-provider.md)，如内核模式驱动程序或用户模式应用程序。

    TraceWPP 提供驱动程序或应用程序使用 WDK 和 Visual Studio 生成时设置 WPP 选项的替代方法。 此工具进程跟踪在源文件中的宏和创建标头文件，以启用 WPP 跟踪。

    TraceWPP 的命令行选项都相同时使用的那些[TraceWPP 任务](tracewpp-task.md)传递到 MSBuild。 有关这些选项的详细信息，请参阅[WPP 预处理器](wpp-preprocessor.md)。

    TraceWPP 位于 bin\\&lt;*平台*&gt; WDK 的目录。

### <a name="span-idcontrollingtracesessionstracecontrollersspanspan-idcontrollingtracesessionstracecontrollersspancontrolling-trace-sessions-trace-controllers"></a><span id="controlling_trace_sessions__trace_controllers_"></span><span id="CONTROLLING_TRACE_SESSIONS__TRACE_CONTROLLERS_"></span>控制跟踪会话 （跟踪控制器）

-   [TraceView](traceview.md) (TraceView.exe) 是基于 GUI[跟踪控制器](trace-controller.md)并[跟踪使用者](trace-consumer.md)，并专门设计用于实时显示跟踪消息。 它可以启用、 配置、 启动、 更新，并停止[跟踪会话](trace-session.md)。 此工具还设置格式、 筛选器，并显示从实时跟踪会话的跟踪消息和[跟踪日志](trace-log.md)。

    TraceView 组合，并将扩展的功能[Tracepdb](tracepdb.md)， [Tracelog](tracelog.md)，并[Tracefmt](tracefmt.md)。 有关信息，启动 TraceView 和从**帮助**菜单中，选择**帮助主题**。

    TraceView 位于工具\\&lt;*平台*&gt;子目录 WDK，其中&lt;*平台*&gt;是 x86 或 x64。

-   [Tracelog](tracelog.md) (Tracelog.exe) 是一个命令行[跟踪控制器](trace-controller.md)启用、 配置、 启动、 更新，以及停止实时和日志会话。 Tracelog 支持用户模式和内核模式跟踪会话，以及[NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)并[全局记录器 （引导） 跟踪会话](global-logger-trace-session.md)。 此工具还支持跟踪来测量时间花在延缓过程调用 (Dpc) 和中断服务例程 (Isr)。

    跟踪日志工具位于\\&lt;*平台*&gt;子目录 WDK，其中&lt;*平台*&gt;是 x86 或 x64。

-   Logman (Logman.exe) 是一个功能齐备，基于 GUI 的[跟踪控制器](trace-controller.md)设计，尤其是，若要控制的性能计数器和事件跟踪日志记录。

    Logman 包含在 Windows XP 和更高版本的 Windows。 有关如何使用此工具的详细信息，请参阅[Logman](https://go.microsoft.com/fwlink/p/?linkid=179385) TechNet 网站上的主题。

### <a name="span-idcreatingtmffilesspanspan-idcreatingtmffilesspancreating-tmf-files"></a><span id="creating_tmf_files"></span><span id="CREATING_TMF_FILES"></span>创建 TMF 文件

-   [Tracepdb](tracepdb.md) (Tracepdb.exe) 是命令行支持工具，用于创建[跟踪消息格式 (TMF) 文件](trace-message-format-file.md)从跟踪消息格式中的说明[PDB 符号文件](pdb-symbol-files.md)。

    显示跟踪消息的工具[Tracefmt](tracefmt.md)(Tracefmt.exe) 和[TraceView](traceview.md)(TraceView.exe)，可以使用从 TMF 文件的格式设置的说明来格式化和显示跟踪消息。

    Tracefmt 还可以创建从 TMF 文件[PDB 符号文件](pdb-symbol-files.md)。

    Tracepdb 和 Tracefmt 工具中的位置\\跟踪\\&lt;*平台*&gt;子目录 WDK，其中&lt;*平台*&gt;是 x86 或 x64。

### <a name="span-idformattinganddisplayingtracemessagestraceconsumersspanspan-idformattinganddisplayingtracemessagestraceconsumersspanformatting-and-displaying-trace-messages-trace-consumers"></a><span id="formatting_and_displaying_trace_messages__trace_consumers_"></span><span id="FORMATTING_AND_DISPLAYING_TRACE_MESSAGES__TRACE_CONSUMERS_"></span>设置格式并显示跟踪消息 （跟踪使用者）

-   [Tracefmt](tracefmt.md)是一个命令行[跟踪使用者](trace-consumer.md)进行格式设置*跟踪消息*(**TraceMessage**) 从实时跟踪会话或跟踪日志和写入到文件或命令提示符窗口中显示它们。

-   Tracerpt (Tracerpt.exe) 是一个命令行[跟踪使用者](trace-consumer.md)进行格式设置*跟踪事件*(**TraceEvent**) 和性能计数器并将其写入到 CSV 或 XML 文件。 它还会分析这些事件，并生成摘要报告。

    Tracerpt 包含在 Windows XP 和更高版本的 Windows。 有关如何使用此工具的详细信息，请参阅[Tracerpt](https://go.microsoft.com/fwlink/p/?linkid=179389) TechNet 网站上的主题。

-   [TraceView](traceview.md)的 GUI 工具，跟踪控制器和跟踪使用者，还设置格式并显示跟踪消息 (**TraceMessage**) 从实时跟踪会话或跟踪日志。 它显示在表格窗体，使其更易于筛选和浏览的跟踪消息。

### <a name="span-idviewingtraceeventsinadebuggerspanspan-idviewingtraceeventsinadebuggerspanviewing-trace-events-in-a-debugger"></a><span id="viewing_trace_events_in_a_debugger"></span><span id="VIEWING_TRACE_EVENTS_IN_A_DEBUGGER"></span>在调试器中查看跟踪事件

-   调试工具的 Windows 包括 **！ wmitrace**，跟踪消息显示在跟踪会话中的专用的调试器扩展缓冲区之前写入的日志文件或显示传递。

-   [Tracelog](tracelog.md)并[TraceView](traceview.md)可以将跟踪消息重定向到 KD 或的 Windbg 中，附加者为准。 有关详细信息，请参阅 Tracelog **-kd**参数和 TraceView **Windbg**选项。

### <a name="span-idanalyzingdpcandisrexecutiontimesspanspan-idanalyzingdpcandisrexecutiontimesspananalyzing-dpc-and-isr-execution-times"></a><span id="analyzing_dpc_and_isr_execution_times"></span><span id="ANALYZING_DPC_AND_ISR_EXECUTION_TIMES"></span>分析 DPC 和 ISR 执行时间

-   在 Windows XP Service Pack 2 (SP2) 和更高版本中，可以使用[Tracelog](tracelog.md)延缓的过程调用 (DPC) 的日志和 NT 内核记录器跟踪会话中会中断服务例程 (ISR) 事件，然后使用 Tracerpt 创建摘要报告从生成的日志。 有关如何使用此工具，其中包括一个示例，请参阅跟踪日志的详细信息。

 

 





