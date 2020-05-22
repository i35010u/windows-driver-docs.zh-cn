---
title: 示例15度量 DPC/ISR 时间
description: 示例15度量 DPC/ISR 时间
ms.assetid: 47936b8b-fd04-44dc-9cd9-77e9d89b4499
keywords:
- 延迟的过程调用 WDK 软件跟踪
- Dpc WDK 软件跟踪
- 中断服务例程 WDK 软件跟踪
- Isr WDK 软件跟踪
- 时间 WDK 软件跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f16f61a0648175bb53390e8b482f9d71da4821a
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769679"
---
# <a name="example-15-measuring-dpcisr-time"></a>示例15：测量 DPC/ISR 时间


## <span id="ddk_measuring_dpc_isr_time_tools"></span><span id="DDK_MEASURING_DPC_ISR_TIME_TOOLS"></span>


你可以通过在 Windows 内核中跟踪这些事件来度量驱动程序在延迟的过程调用（Dpc）和中断服务例程（Isr）中花费的时间。 此信息将帮助你最大程度地减少驱动程序在更高 IRQLs 上所花费的时间，使驱动程序和系统更高效。

Microsoft 建议 Dpc 运行时间不能超过100微秒，Isr 不应超过25微秒。 有关最新的要求，请参阅[硬件实验室工具包](https://docs.microsoft.com/windows-hardware/test/hlk/)。

本节中描述的过程包括以下步骤：

1.  启动 DPC/ISR 事件的内核跟踪。

2.  监视跟踪会话中丢失的事件，并在必要时增大跟踪缓冲区的大小。

3.  试验测试驱动程序。

4.  停止跟踪会话。

5.  使用 Tracerpt 生成汇总 DPC/ISR 活动的报告。

6.  分析报告

### <a name="span-idstep_1__start_a_trace_session_spanspan-idstep_1__start_a_trace_session_spanstep-1-start-a-trace-session"></a><span id="step_1__start_a_trace_session_"></span><span id="STEP_1__START_A_TRACE_SESSION_"></span>步骤1：启动跟踪会话。

下面的命令启动 NT 内核记录器跟踪会话：

```
tracelog -start -f test01.etl -dpcisr -UsePerfCounter -b 64
```

**Tracelog**命令启动跟踪会话。 由于 "NT 内核记录器" 是默认的会话名称，因此您不需要指定它，并且您不能使用 **-guid**参数来指定提供程序文件。 该命令使用 **-f**参数指示日志会话，并将跟踪消息定向到*test01*事件跟踪日志文件。

此命令包含 **-dpcisr**参数，用于启用对 Dpc、isr、上下文切换和图像加载的跟踪。

跟踪 Dpc 和 Isr 时，请始终将 **-UsePerfCounter**参数添加到命令中。 系统计时器分辨率太小，无法测量这些活动所花费的时间。 另外，Tracerpt 是设置 DPC/ISR 事件格式的工具，它要求其报表的性能计数器时钟值。 （Tracerpt 包含在 Windows XP 和更高版本的 Windows 中。）

最后，此命令使用 **-b**参数将跟踪缓冲区的大小增加到 64 KB。 由于 DPC/ISR 跟踪会快速生成大量跟踪消息，因此增加跟踪缓冲区的大小时，不会丢失事件，这一点很重要。

对于此命令，Tracelog 启动 NT 内核记录器会话并显示其属性。

```
Logger Started...
Operation Status:       0L      The operation completed successfully.

Logger Name:            NT Kernel Logger
Logger Id:              ffff
Logger Thread Id:       00000C18
Buffer Size:            64 Kb
Maximum Buffers:        25
Minimum Buffers:        3
Number of Buffers:      5
Free Buffers:           4
Buffers Written:        14
Events Lost:            0
Log Buffers Lost:       0
Real Time Buffers Lost: 0
AgeLimit:               15
Log File Mode:          Sequential
Enabled tracing:        Process Thread Disk File ImageLoad
Log Filename:           c:\Tracelog\test01.etl
```

请注意，DPC、ISR 和上下文切换事件不会出现在显示的 "**已启用跟踪**" 字段中。 由于这些事件由内部检测来监视，因此即使启用了这些事件，也不会在此列表中显示。 不过，还会显示通过 **-dpcisr**参数启用的图像加载事件。

### <a name="span-idstep_2__check_for_lost_events_spanspan-idstep_2__check_for_lost_events_spanstep-2-check-for-lost-events"></a><span id="step_2__check_for_lost_events_"></span><span id="STEP_2__CHECK_FOR_LOST_EVENTS_"></span>步骤2：检查丢失的事件。

定期使用**tracelog** （查询）命令检查丢失的事件。 如果找到它们，请使用**tracelog**命令向跟踪会话添加更多的缓冲区。

```
tracelog -q
```

**Tracelog**命令采用会话名称，但在这种情况下不需要提供此项，因为 "NT 内核记录器" 是默认值。

对于此命令，Tracelog 将显示会话的属性。

```
Operation Status:       0L      The operation completed successfully.

Logger Name:            NT Kernel Logger
Logger Id:              ffff
Logger Thread Id:       00000BC4
Buffer Size:            64 Kb
Maximum Buffers:        25
Minimum Buffers:        3
Number of Buffers:      25
Free Buffers:           23
Buffers Written:        571
Events Lost:            544
Log Buffers Lost:       0
Real Time Buffers Lost: 0
AgeLimit:               15
Log File Mode:          Sequential
Enabled tracing:        Process Thread Disk File ImageLoad
Log Filename:           c:\Tracelog\test.etl
```

在这种情况下，生成的544事件未保存到缓冲区中。 若要防止此情况重复发生，请使用**tracelog**命令增加每个缓冲区的大小（**-b**）或增加缓冲区的最大数目（**-max**），例如：

```
tracelog -update -b 128 -max 40
```

### <a name="span-idstep_3__exercise_the_driver_spanspan-idstep_3__exercise_the_driver_spanstep-3-exercise-the-driver"></a><span id="step_3__exercise_the_driver_"></span><span id="STEP_3__EXERCISE_THE_DRIVER_"></span>步骤3：测试驱动程序。

使用测试例程来使驱动程序执行其功能。 请考虑运行两个测试，一个用于基本功能，另一个用于更高级的函数。

### <a name="span-idstep_4__stop_the_trace_session_spanspan-idstep_4__stop_the_trace_session_spanstep-4-stop-the-trace-session"></a><span id="step_4__stop_the_trace_session_"></span><span id="STEP_4__STOP_THE_TRACE_SESSION_"></span>步骤4：停止跟踪会话。

使用以下命令停止跟踪会话：

```
tracelog -stop
```

**Tracelog**命令通常需要会话名称，但是因为 "NT 内核记录器" 是默认值，所以会话名称不是必需的。

### <a name="span-idstep_5__create_a_dpc_isr_report_spanspan-idstep_5__create_a_dpc_isr_report_spanstep-5-create-a-dpcisr-report"></a><span id="step_5__create_a_dpc_isr_report_"></span><span id="STEP_5__CREATE_A_DPC_ISR_REPORT_"></span>步骤5：创建 DPC/ISR 报表。

若要在事件跟踪日志中汇总 DPC/ISR 消息，请使用 Windows XP SP2 和更高版本的 Windows 中包含的 Tracerpt 版本。

以下 Tracerpt 命令将设置*Test01*文件中的消息的格式，并在带有 SP2 的 Windows XP 中创建活动的文本格式的报表。

```
tracerpt test01.etl -report dpcisr.txt -df
```

在此命令中， **-report**参数指定分析方法以及输出文件的名称。 仅在具有 SP2 的 Windows XP 中正确格式化消息时，才需要 **-df**参数。

在 Windows Server 2003 SP1 及更高版本的 Windows 中创建此报表时，可以使用以下命令创建一个 HTML 格式的报表。

```
tracerpt test01.etl -report dpcisr.html -f HTML
```

在此命令中， **-report**参数指定输出文件的名称， **-f**参数指定报表格式。

### <a name="span-idstep_6__analyze_the_report_spanspan-idstep_6__analyze_the_report_spanstep-6-analyze-the-report"></a><span id="step_6__analyze_the_report_"></span><span id="STEP_6__ANALYZE_THE_REPORT_"></span>步骤6：分析报表。

"Windows 事件跟踪会话报告" 包含以下部分：

-   **映像统计信息。** 显示在跟踪过程中在计算机上运行的进程的数据。

-   **磁盘总数。** 显示在跟踪过程中运行的每个进程的磁盘 i/o 数据。

-   **整个跟踪的 DPC 处理器利用率：** 显示处理每个驱动程序的 DPC 例程所用的处理器时间百分比。

-   **整个跟踪的所有 DPC 执行时间的分布**。 以微秒为单位的时间范围表。 该表显示每个时间范围内 DPC 例程的百分比。

-   **整个跟踪的 DriverName （DPCRoutineAddress） DPC 执行时间。** 以微秒为单位的时间范围表。 该表显示此 DPC 例程的每个时间范围内的实例的百分比。 跟踪中的每个 DPC 例程都会显示此类节。

-   **整个跟踪的 ISR 处理器利用率。** 显示处理跟踪中每个驱动程序的中断服务例程所用的处理器时间百分比。

-   **整个跟踪的所有 ISR 执行时间的分布。** 以微秒为单位的时间范围表。 该表显示每个时间范围内的 ISR 例程的百分比。

-   **为整个跟踪的 DriverName （ISRAddress） ISR 的执行时间。** 以微秒为单位的时间范围表。 该表显示每个时间范围内的 ISR 实例的百分比。 跟踪中的每个 ISR 都将显示此类节。

-   **TracingPeriodInMs 两微秒时间窗口的 DPC 和 ISR 处理器利用率的分布。** 在跟踪过程中，按 Dpc 和 Isr 显示组合的处理器使用率。

-   **将 DriverName （ISRAddress） ISR 分配给整个跟踪的 DriverName （DPCRoutineAddress） DPC 延迟。** 显示 ISR 结束与关联 DPC 开头之间的延迟间隔分布。

下面的示例报表摘录显示了 DPC 执行时间。 通常，不建议在不超过100微秒的 DPC 例程。 此报告显示，此驱动程序的这一半 DPC 例程超出了阈值。

```
+------------------------------------------------------------------------------+
| Distribution of ipsec.sys (F7AA7449) DPC execution times for the whole trace |
+------------------------------------------------------------------------------+
| Lower Bound         Upper Bound            Count             Percent         |
+------------------------------------------------------------------------------+
|           0                   1                0                0.00%        |
|           1                   2                0                0.00%        |
|           2                   3                8               42.11%        |
|           3                   4                1                5.26%        |
|           4                   5                0                0.00%        |
|           5                  10                0                0.00%        |
|          10                  25                0                0.00%        |
|          25                  50                0                0.00%        |
|          50                 100                0                0.00%        |
|         100                 250               10               52.63%        |
+------------------------------------------------------------------------------+
|                                               19              100.00%        |
+------------------------------------------------------------------------------+
```

 

 





