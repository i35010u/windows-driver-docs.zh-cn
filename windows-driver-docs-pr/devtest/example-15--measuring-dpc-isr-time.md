---
title: 例如，如果希望测量 DPC/ISR 时间
description: 例如，如果希望测量 DPC/ISR 时间
ms.assetid: 47936b8b-fd04-44dc-9cd9-77e9d89b4499
keywords:
- 延迟的过程调用 WDK 软件跟踪
- Dpc WDK 软件跟踪
- 中断服务例程 WDK 软件跟踪
- Isr WDK 软件跟踪
- 时间 WDK 软件跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c9469b55a507c14727e566bf610541f4e960308
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555676"
---
# <a name="example-15-measuring-dpcisr-time"></a>例如，如果希望：测量 DPC/ISR 时间


## <span id="ddk_measuring_dpc_isr_time_tools"></span><span id="DDK_MEASURING_DPC_ISR_TIME_TOOLS"></span>


可以度量值的一个驱动程序在延缓的过程调用 (Dpc) 中所花的时间和中断服务例程 (Isr) 通过跟踪 Windows 内核中的这些事件。 此信息将帮助你尽量减小在更高版本于 Irql，从而使该驱动程序和系统效率更高的驱动程序所花费的时间。

Microsoft 建议 Dpc 不应运行时间超过 100 微秒 Isr 不应运行时间超过 25 微秒为单位。 有关最新的要求，请参阅[硬件认证计划]( https://go.microsoft.com/fwlink/p/?linkid=227016)。

本节中所述的过程包括以下步骤：

1.  启动 DPC/ISR 事件的内核跟踪。

2.  监视丢失事件跟踪会话，并且如有必要，增加跟踪缓冲区的大小。

3.  执行测试驱动程序。

4.  停止跟踪会话。

5.  使用 Tracerpt 生成报表，汇总 DPC/ISR 活动。

6.  分析报告

### <a name="span-idstep1startatracesessionspanspan-idstep1startatracesessionspanstep-1-start-a-trace-session"></a><span id="step_1__start_a_trace_session_"></span><span id="STEP_1__START_A_TRACE_SESSION_"></span>步骤 1:启动跟踪会话。

以下命令启动的 NT 内核记录器跟踪会话：

```
tracelog -start -f test01.etl -dpcisr -UsePerfCounter -b 64
```

**Tracelog-启动**命令启动跟踪会话。 由于"NT 内核记录器"是默认会话名称，不需要指定此选项，因此，不能使用**guid**参数来指定提供程序文件。 该命令使用 **-f**参数来指示日志会话，并直接将跟踪消息*test01.etl*事件跟踪日志文件。

该命令包含 **-执行 dpcisr**参数来启用 Dpc、 Isr、 上下文切换和图像加载的跟踪。

在跟踪过程 Dpc 和 Isr 中，始终将添加 **-UsePerfCounter**命令参数。 系统计时器分辨率是过低，以测量这些活动中所用的时间。 此外，Tracerpt，格式 DPC/ISR 事件，该工具需要性能计数器时钟值对于其报表。 （Tracerpt 包含在 Windows XP 和更高版本的 Windows 中）。

最后，该命令使用 **-b**参数增加为 64 KB 的跟踪缓冲区的大小。 因为 DPC/ISR 跟踪生成的快速增长的跟踪消息量很高，务必增加跟踪缓冲区的大小，以便不会丢失事件。

此命令的响应，Tracelog 启动 NT 内核记录器会话，并显示其属性。

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

请注意 DPC、 ISR 和上下文切换事件中不会出现**已启用跟踪**显示的字段。 因为这些事件由监视内部检测，它们不会出现在此列表中甚至当它们启用时。 但是，映像加载事件，也会通过启用 **-执行 dpcisr**参数，就会出现。

### <a name="span-idstep2checkforlosteventsspanspan-idstep2checkforlosteventsspanstep-2-check-for-lost-events"></a><span id="step_2__check_for_lost_events_"></span><span id="STEP_2__CHECK_FOR_LOST_EVENTS_"></span>步骤 2:检查丢失事件。

使用**tracelog-q** （查询） 命令会定期检查丢失事件。 如果您找到它们，使用**tracelog-更新**命令将添加到跟踪会话的更多的缓冲区。

```
tracelog -q
```

**Tracelog-q**命令采用一个会话名称，但无需在这种情况下提供一个，因为是默认的"NT 内核记录器"。

此命令的响应，Tracelog 显示会话的属性。

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

在这种情况下，生成的 544 事件未保存的缓冲区中。 若要避免此再次发生，请使用**tracelog-更新**命令来增加每个缓冲区的大小 (**-b**) 或增加缓冲区的最大数目 (**-最大**)，为示例：

```
tracelog -update -b 128 -max 40
```

### <a name="span-idstep3exercisethedriverspanspan-idstep3exercisethedriverspanstep-3-exercise-the-driver"></a><span id="step_3__exercise_the_driver_"></span><span id="STEP_3__EXERCISE_THE_DRIVER_"></span>步骤 3:执行驱动程序。

使用测试例程，使驱动程序执行其功能。 请考虑运行两个测试、 基本功能和更高级的功能。

### <a name="span-idstep4stopthetracesessionspanspan-idstep4stopthetracesessionspanstep-4-stop-the-trace-session"></a><span id="step_4__stop_the_trace_session_"></span><span id="STEP_4__STOP_THE_TRACE_SESSION_"></span>步骤 4:停止跟踪会话。

使用以下命令来停止跟踪会话：

```
tracelog -stop
```

一个**tracelog-停止**命令通常需要会话名称，但"NT 内核记录器"是默认值，因为会话名称不是必需。

### <a name="span-idstep5createadpcisrreportspanspan-idstep5createadpcisrreportspanstep-5-create-a-dpcisr-report"></a><span id="step_5__create_a_dpc_isr_report_"></span><span id="STEP_5__CREATE_A_DPC_ISR_REPORT_"></span>步骤 5:创建一个 DPC/ISR 报表。

若要汇总的 DPC/ISR 消息事件跟踪日志中，使用 Tracerpt 包含在 Windows XP SP2 和更高版本的 Windows 版本。

以下 Tracerpt 命令格式中的消息*Test01.etl*文件，并在 Windows XP SP2 中创建文本格式的活动报表。

```
tracerpt test01.etl -report dpcisr.txt -df
```

在此命令中， **-报表**参数指定的分析方法，并输出文件的名称。 **-Df**正确地设置消息格式仅在 Windows XP SP2 中所需的参数。

创建此报表时在 Windows Server 2003 SP1 和更高版本的 Windows 中，您可以通过使用以下命令创建 HTML 格式的报告。

```
tracerpt test01.etl -report dpcisr.html -f HTML
```

在此命令中， **-报表**参数指定输出文件的名称和 **-f**参数指定的报表格式。

### <a name="span-idstep6analyzethereportspanspan-idstep6analyzethereportspanstep-6-analyze-the-report"></a><span id="step_6__analyze_the_report_"></span><span id="STEP_6__ANALYZE_THE_REPORT_"></span>步骤 6:分析报告。

"Windows 事件跟踪会话报表"具有以下各节：

-   **映像的统计信息。** 显示在跟踪期间的计算机上运行的进程有关的数据。

-   **磁盘总数。** 显示有关磁盘 I/O 的每个进程在跟踪期间运行的数据。

-   **整个跟踪的 DPC 处理器使用率：** 显示每个驱动程序的处理器时所用服务 DPC 例程的百分比。

-   **为整个跟踪所有 DPC 执行时间的分布**。 以微秒为单位的时间范围的表。 表显示在每个时间范围内的 DPC 例程的百分比。

-   **分发 DriverName (DPCRoutineAddress) DPC 整个跟踪的执行时间。** 以微秒为单位的时间范围的表。 表显示在每个时间范围内的此 DPC 例程实例的百分比。 对每个 DPC 例程在跟踪中显示部分与此类似。

-   **整个跟踪 ISR 处理器使用率。** 显示的处理器时间百分比用于服务中断服务例程在跟踪中的每个驱动程序。

-   **为整个跟踪所有 ISR 执行时间的分布。** 以微秒为单位的时间范围的表。 表显示在每个时间范围内的 ISR 例程的百分比。

-   **分发 DriverName (ISRAddress) ISR 整个跟踪的执行时间。** 以微秒为单位的时间范围的表。 表显示在每个时间范围内的 ISR 实例的百分比。 在跟踪中的每个 ISR 会出现此类部分。

-   **TracingPeriodInMs 两个微秒时间窗口的 DPC 和 ISR 处理器使用率的分布。** 在跟踪过程中显示的 Dpc 和 Isr 的总的处理器使用率。

-   **分发 DriverName (ISRAddress) 到 DriverName (DPCRoutineAddress) DPC ISR 整个跟踪的延迟。** 显示 ISR 末尾和关联 DPC 的开头之间的延迟时间间隔的分布。

以下内容摘自示例报表演示 Ipsec.sys DPC 执行时间的分布。 一般情况下，不建议使用 DPC 例程持续时间长达 100 个以上的微秒数。 此报表显示有超过一半的此驱动程序的 DPC 例程超出了阈值。

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

 

 





